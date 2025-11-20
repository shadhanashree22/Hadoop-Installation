# Hadoop Installation on Windows (Single Node Setup)
```
Name : S V SHADHANASHREE
Reg No : 212223230202
```

> **Prerequisite:** Hadoop requires **Java 1.8** installed on your system.

## 1. Check Java Version
```bash
java -version
```
If Java is not installed, download JDK 1.8:
https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html

Install to:
C:\Java\jdk1.8.0_181

## 2. Download Hadoop
Download Hadoop 3.1.x:
https://hadoop.apache.org/releases.html

Extract to:
C:\hadoop-3.1.3  
Rename to:
C:\hadoop

## 3. Set Environment Variables
Add user variable:
HADOOP_HOME = C:\hadoop

Add to PATH:
%HADOOP_HOME%\bin  
C:\Java\jdk1.8.0_181\bin

## 4. Configure Hadoop
Edit files in:
C:\hadoop\etc\hadoop

### core-site.xml
```xml
<configuration>
   <property>
       <name>fs.defaultFS</name>
       <value>hdfs://localhost:9000</value>
   </property>
</configuration>
```

### mapred-site.xml
```xml
<configuration>
   <property>
       <name>mapreduce.framework.name</name>
       <value>yarn</value>
   </property>
</configuration>
```

### Create Data Folders
```
C:\hadoop\data\namenode
C:\hadoop\data\datanode
```

### hdfs-site.xml
```xml
<configuration>
   <property>
       <name>dfs.replication</name>
       <value>1</value>
   </property>
   <property>
       <name>dfs.namenode.name.dir</name>
       <value>C:\hadoop\data\namenode</value>
   </property>
   <property>
       <name>dfs.datanode.data.dir</name>
       <value>C:\hadoop\data\datanode</value>
   </property>
</configuration>
```

### yarn-site.xml
```xml
<configuration>
   <property>
       <name>yarn.nodemanager.aux-services</name>
       <value>mapreduce_shuffle</value>
   </property>
   <property>
       <name>yarn.nodemanager.auxservices.mapreduce.shuffle.class</name>
       <value>org.apache.hadoop.mapred.ShuffleHandler</value>
   </property>
</configuration>
```

### hadoop-env.cmd
```
set JAVA_HOME=C:\Java\jdk1.8.0_181
```

## 5. Add Windows Hadoop Binaries
Download winutils:
https://github.com/s911415/apache-hadoop-3.1.3-winutils

Replace:
C:\hadoop\bin

## 6. Verify Installation
```bash
hadoop version
```

## 7. Format NameNode
```bash
hdfs namenode -format
```

## 8. Start Hadoop Services
### Start HDFS
```bash
cd C:\hadoop\sbin
start-dfs.cmd
```

### Start YARN
```bash
cd C:\hadoop\sbin
start-yarn.cmd
```

## 9. Access Web UIs
Resource Manager:
http://localhost:8088/cluster

NameNode:
http://localhost:9870/dfshealth.html#tab-overview

## ✔ Hadoop Installed Successfully
