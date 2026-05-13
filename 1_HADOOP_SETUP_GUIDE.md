# Ultimate Hadoop Setup Guide (Ubuntu & Windows)

This guide provides copy-pasteable steps to set up a Single-Node Hadoop Cluster.

---

## Part 1: Hadoop Setup on Ubuntu (Recommended)

### 1. Update System & Install Java
```bash
sudo apt update
sudo apt install openjdk-8-jdk -y
java -version
```

### 2. Configure SSH (Passwordless Login)
Hadoop needs to communicate with nodes via SSH.
```bash
sudo apt install ssh -y
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
ssh localhost # Type 'yes' and then 'exit'
```

### 3. Download & Install Hadoop
```bash
wget https://downloads.apache.org/hadoop/common/hadoop-3.3.6/hadoop-3.3.6.tar.gz
tar -xzvf hadoop-3.3.6.tar.gz
sudo mv hadoop-3.3.6 /usr/local/hadoop
```

### 4. Setup Environment Variables
Edit your `~/.bashrc`:
```bash
nano ~/.bashrc
```
Add these lines at the end:
```bash
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export HADOOP_HOME=/usr/local/hadoop
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
```
Save (Ctrl+O, Enter) and Exit (Ctrl+X). Then run:
```bash
source ~/.bashrc
```

### 5. Configure Hadoop XML Files
Go to `$HADOOP_HOME/etc/hadoop/` and edit these:

**core-site.xml**:
```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
```

**hdfs-site.xml**:
```xml
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```

### 6. Format & Start
```bash
hdfs namenode -format
start-dfs.sh
start-yarn.sh
jps
```

---

## Part 2: Hadoop Setup on Windows

### 1. Prerequisites
- **Java 8**: Install JDK 1.8 (Hadoop is very picky on Windows).
- **Winutils**: Download `winutils.exe` and `hadoop.dll` for your Hadoop version (e.g., from [cdarlint/winutils](https://github.com/cdarlint/winutils)).

### 2. Set Environment Variables
Open "Edit the system environment variables":
- `JAVA_HOME`: `C:\Program Files\Java\jdk1.8.0_xxx`
- `HADOOP_HOME`: `C:\hadoop-3.3.6`
- Add `%HADOOP_HOME%\bin` and `%JAVA_HOME%\bin` to your **Path**.

### 3. Fix Hadoop Bin Folder
1. Extract Hadoop to `C:\hadoop-3.3.6`.
2. Copy the downloaded `winutils.exe` and `hadoop.dll` into `C:\hadoop-3.3.6\bin`.

### 4. Configure XML Files
Edit the files in `C:\hadoop-3.3.6\etc\hadoop\`. 
*Note: Use forward slashes `/` in paths.*

**core-site.xml**:
```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
```

**hdfs-site.xml**:
```xml
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>/C:/hadoop-3.3.6/data/namenode</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>/C:/hadoop-3.3.6/data/datanode</value>
    </property>
</configuration>
```

### 5. Format & Start
Open Command Prompt as **Administrator**:
```cmd
hdfs namenode -format
%HADOOP_HOME%\sbin\start-dfs.cmd
%HADOOP_HOME%\sbin\start-yarn.cmd
jps
```

---

## Part 3: Verification (Common for both)
- **NameNode UI**: `http://localhost:50070` (or `9870` for Hadoop 3.x)
- **DataNode UI**: `http://localhost:50075`
- **YARN Resource Manager**: `http://localhost:8088`
