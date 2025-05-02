======== EX 1 ===========

- sudo apt update
- sudo apt upgrade
- sudo apt install openjdk-8-jdk
- java -version
- mkdir -p ~/hadoop
- cd ~/hadoop
- wget https://dlcdn.apache.org/hadoop/common/hadoop-3.4.1/hadoop-3.4.1.tar.gz
- tar -xvzf hadoop-3.4.1.tar.gz
- sudo mv hadoop-3.4.1 /usr/local/hadoop
- nano ~/.bashrc
- - At the end add :
export HADOOP_HOME=/usr/local/hadoop
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_YARN_HOME=$HADOOP_HOME
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

- source ~/.bashrc
- cd /usr/local/hadoop/etc/hadoop
- nano core-site.xml
- - edit as
<configuration>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://localhost:9000</value>
  </property>
</configuration>

- nano hdfs-site.xml
- - edit as
<configuration>
  <property>
    <name>dfs.replication</name>
    <value>1</value>
  </property>
  <property>
    <name>dfs.name.dir</name>
    <value>file:///usr/local/hadoop/hdfs/namenode</value>
  </property>
  <property>
    <name>dfs.data.dir</name>
    <value>file:///usr/local/hadoop/hdfs/datanode</value>
  </property>
</configuration>

- sudo mkdir -p /usr/local/hadoop/hdfs/namenode
- sudo mkdir -p /usr/local/hadoop/hdfs/datanode
- sudo chown -R $USER:$USER /usr/local/hadoop/hdfs
- sudo nano mapred-site.xml
- - edit as
<configuration>
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
  </property>
</configuration>

- nano yarn-site.xml
- - edit as
<configuration>
  <property>
    <name>yarn.resourcemanager.hostname</name>
    <value>localhost</value>
  </property>
</configuration>

- readlink -f $(which java)
- - copy the path it give until amd64

- nano /usr/local/hadoop/etc/hadoop/hadoop-env.sh
- - Add Line
export JAVA_HOME={copied path}

- source ~/.bashrc
- hdfs namenode -format

- sudo apt install openssh-server
- sudo systemctl start ssh
- sudo systemctl enable ssh
- sudo systemctl status ssh
- ssh-keygen -t rsa -P ""
- cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
- chmod 600 ~/.ssh/authorized_keys
- ssh localhost

- start-dfs.sh
- start-yarn.sh
- jps
- stop-yarn.sh
- stop-dfs.sh

============ EX 2 =============

- start-all.sh
- jps
- ----
lorem@csbs-HP-Elite-Tower-600-G9-Desktop-PC:~$ hdfs dfs -ls /
lorem@csbs-HP-Elite-Tower-600-G9-Desktop-PC:~$ hdfs dfs -mkdir /csbs
lorem@csbs-HP-Elite-Tower-600-G9-Desktop-PC:~$ hdfs dfs -ls /
Found 1 items
drwxr-xr-x   - lorem supergroup          0 2025-04-25 12:51 /csbs
lorem@csbs-HP-Elite-Tower-600-G9-Desktop-PC:~$ hdfs dfs -rmdir /csbs
lorem@csbs-HP-Elite-Tower-600-G9-Desktop-PC:~$ nano example.txt
lorem@csbs-HP-Elite-Tower-600-G9-Desktop-PC:~$ hdfs dfs -mkdir /folder
lorem@csbs-HP-Elite-Tower-600-G9-Desktop-PC:~$ hdfs dfs -put example.txt /folder
lorem@csbs-HP-Elite-Tower-600-G9-Desktop-PC:~$ hdfs dfs -cat /folder/example.txt
hello
lorem@csbs-HP-Elite-Tower-600-G9-Desktop-PC:~$ hdfs dfs -ls /folder
Found 1 items
-rw-r--r--   1 lorem supergroup          6 2025-04-25 12:53 /folder/example.txt
lorem@csbs-HP-Elite-Tower-600-G9-Desktop-PC:~$ hdfs dfs -rm /folder/example.txt
Deleted /folder/example.txt
lorem@csbs-HP-Elite-Tower-600-G9-Desktop-PC:~$ hdfs dfs -ls /folder

- ----------
- stop-all.sh
