________________________________________
Check Hadoop
CMD:
hadoop version
If version appears → setup working.
________________________________________
This is the usual college practical setup.
Folder Structure
Create a folder like:
HadoopProject
Inside it keep:
mapper.py
reducer.py
input.txt
________________________________________
Step 1 — Create input.txt
input.txt
hello world
hello hadoop
world hello
________________________________________
Step 2 — Create mapper.py
mapper.py
import sys

for line in sys.stdin:
    words = line.strip().split()

    for word in words:
        print(f"{word}\t1")
Mapper converts:
hello world
into:
hello 1
world 1
________________________________________
Step 3 — Create reducer.py
reducer.py
import sys

current_word = None
count = 0

for line in sys.stdin:
    word, value = line.strip().split("\t")
    value = int(value)

    if word == current_word:
        count += value
    else:
        if current_word:
            print(f"{current_word}\t{count}")

        current_word = word
        count = value

if current_word:
    print(f"{current_word}\t{count}")
Reducer combines counts.
________________________________________
Step 4 — Open CMD in Folder
Go inside project folder.
Example:
cd Desktop\HadoopProject
________________________________________
Step 5 — Test Without Hadoop First (VERY IMPORTANT)
Run mapper:
type input.txt | python mapper.py
Output:
hello   1
world   1
hello   1
hadoop  1
world   1
hello   1
Now test reducer:
type input.txt | python mapper.py | sort | python reducer.py
Output:
hadoop 1
hello 3
world 2
If this works → your mapper/reducer are correct ✅
________________________________________
Step 6 — Run Using Hadoop
Now actual Hadoop command.
hadoop jar %HADOOP_HOME%\share\hadoop\tools\lib\hadoop-streaming*.jar ^
-input input.txt ^
-output output ^
-mapper mapper.py ^
-reducer reducer.py
________________________________________
Step 7 — View Output
type output\part-00000
Output:
hadoop 1
hello 3
world 2
________________________________________
VERY COMMON ERRORS 💀
1. Output already exists
Error:
Output directory already exists
Delete old output:
rmdir /s output
Then rerun.
________________________________________
2. Hadoop not recognized
Need:
•	HADOOP_HOME 
•	PATH variables 
________________________________________
3. Python not recognized
Install Python and enable:
Add Python to PATH
________________________________________
Viva Explanation Short Version 🎤
Mapper
Takes input and converts into key-value pairs.
Example:
hello world
becomes:
hello 1
world 1
________________________________________
Reducer
Combines same keys and gives final count.

