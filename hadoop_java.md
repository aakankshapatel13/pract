 Java Hadoop MapReduce version.
This is the classic WordCount practical everyone gets in viva.
Folder Structure
Create folder:
WordCount
Inside keep:
Mapper.java
Reducer.java
Driver.java
input.txt
________________________________________
Step 1 — input.txt
input.txt
hello world
hello hadoop
world hello
________________________________________
Step 2 — Mapper.java
Mapper.java
import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;

import org.apache.hadoop.mapreduce.Mapper;

public class MapperClass extends Mapper<Object, Text, Text, IntWritable> {

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context)
            throws IOException, InterruptedException {

        StringTokenizer itr = new StringTokenizer(value.toString());

        while (itr.hasMoreTokens()) {
            word.set(itr.nextToken());
            context.write(word, one);
        }
    }
}
________________________________________
Step 3 — Reducer.java
Reducer.java
import java.io.IOException;

import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;

import org.apache.hadoop.mapreduce.Reducer;

public class ReducerClass extends Reducer<Text, IntWritable, Text, IntWritable> {

    public void reduce(Text key, Iterable<IntWritable> values, Context context)
            throws IOException, InterruptedException {

        int sum = 0;

        for (IntWritable val : values) {
            sum += val.get();
        }

        context.write(key, new IntWritable(sum));
    }
}
________________________________________
Step 4 — Driver.java
Driver.java
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;

import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;

import org.apache.hadoop.mapreduce.Job;

import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;

public class Driver {

    public static void main(String[] args) throws Exception {

        Configuration conf = new Configuration();

        Job job = Job.getInstance(conf, "word count");

        job.setJarByClass(Driver.class);

        job.setMapperClass(MapperClass.class);
        job.setReducerClass(ReducerClass.class);

        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);

        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));

        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
________________________________________
Step 5 — Open CMD in Folder
cd Desktop\WordCount
________________________________________
Step 6 — Compile Java Files
VERY IMPORTANT ⚠
javac -classpath %HADOOP_HOME%\share\hadoop\common\*;%HADOOP_HOME%\share\hadoop\mapreduce\* -d . *.java
If successful → .class files created.
________________________________________
Step 7 — Create JAR File
jar cf wordcount.jar *.class
Creates:
wordcount.jar
________________________________________
Step 8 — Run Hadoop Job
hadoop jar wordcount.jar Driver input.txt output
________________________________________
Step 9 — View Output
type output\part-r-00000
Output:
hadoop 1
hello 3
world 2
________________________________________
MOST IMPORTANT VIVA QUESTIONS 🎤
What Mapper does?
Converts input into key-value pairs.
Example:
hello world
becomes:
hello 1
world 1
________________________________________
What Reducer does?
Combines values of same key.
Example:
hello 1
hello 1
hello 1
becomes:
hello 3
________________________________________
Driver role?
Connects mapper + reducer and configures job.
________________________________________
Why jar file?
Hadoop executes jar file across cluster.
________________________________________
Common Errors 💀
ClassNotFoundException
Wrong class name in command.
________________________________________
Output exists
Delete output folder:
rmdir /s output
________________________________________
Hadoop package not found
Classpath command wrong OR Hadoop not installed correctly.

