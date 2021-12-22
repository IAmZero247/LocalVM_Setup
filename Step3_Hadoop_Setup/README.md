# Hadoop Setup 

- Ref -> https://phoenixnap.com/kb/install-hadoop-ubuntu
  
- Additional Step required: Install openssh-server and set keys for passwordless login
  1. sudo apt-get update
  2. sudo apt-get upgrade
  3. sudo apt-get install openssh-server

  4. ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
  5. cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

  6. verfiy -> ssh localhost
  
- Download tar.gz file for hadoop-3.2.2

   https://hadoop.apache.org/releases.html
  
   https://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-3.2.2/hadoop-3.2.2.tar.gz


- Untar it 
    
	tar -xzvf hadoop-2.8.5.tar.gz

- copy it to /usr/local/hadoop

- Set up the path. Open command line and wrote "gedit ~/.bashrc" 
  
  1. Add below to .bashrc
  
    - export HADOOP_HOME=/usr/local/hadoop/hadoop-3.2.2
	- export HADOOP_INSTALL=$HADOOP_HOME
	- export HADOOP_MAPRED_HOME=$HADOOP_HOME
	- export HADOOP_COMMON_HOME=$HADOOP_HOME
	- export HADOOP_HDFS_HOME=$HADOOP_HOME
	- export YARN_HOME=$HADOOP_HOME
	- export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
	- export PATH=$PATH:$HADOOP_HOME/bin
	- export PATH=$PATH:$HADOOP_HOME/sbin
	- export HADOOP_CONF_DIR=/usr/local/hadoop/hadoop-3.2.2/etc/hadoop
	- export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
	- export HADOOP_STREAMING=$HADOOP_HOME/share/hadoop/tools/lin/hadoop-streming-2.9.2.jar
	- export HADOOP_LOG_DIR=$HADOOP_HOME/logs  
	
  2. Note: To set path, either restart the VM or run below

		source ~/.bashrc	
		
- Update Configs In hadoop-env.sh
    
	1. Open file -> sudo nano $HADOOP_HOME/etc/hadoop/hadoop-env.sh and add below  
	
	  export JAVA_HOME=/usr/local/java/jdk1.8.0_261
	

    2. If you need help to locate the correct Java path, run the following command in your terminal window:

      a. which javac
     
	  The resulting output provides the path to the Java binary directory.

      /usr/bin/javac
      
	  b. Use the provided path to find the OpenJDK directory with the following command:

      readlink -f /usr/bin/javac
      
	  The section of the path just before the /bin/javac directory needs to be assigned to the $JAVA_HOME variable.
 
      /usr/local/java/jdk1.8.0_261/bin/javac
	