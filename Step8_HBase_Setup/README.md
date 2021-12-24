# HBase - Pseudo Distributed Mode

- Ref1: https://prwatech.in/blog/hadoop-admin-2/sqoop-installation-in-manual-cluster/

- Ref2: https://www.guru99.com/hbase-installation-guide.html
  
- https://hbase.apache.org/

- Download -> https://archive.apache.org/dist/hbase/2.4.6/

- tar  -xvf hbase-2.4.6-bin.tar.gz

- Copy it to /usr/local/hbase

- Update cat for all 127.0.0.1 /etc/hosts
    
	```
	127.0.0.1	localhost
	127.0.0.1	osboxes
	http://localhost:16010/master-status
	http://localhost:16030/rs-status
    
	```
- Edit the .bashrc file

    ```
	export HBASE_HOME=/usr/local/hbase/hbase-2.4.8
	export PATH=$PATH:$HBASE_HOME/bin
	
	
	source ~/.bashrc

	```
	
- Update  conf/hbase-env.sh

  ```
  Add below to hbase-env 
  export JAVA_HOME=/usr/local/java/jdk1.8.0_261
  ``` 
  
  
- Update conf/hbase-site.xml for temp directory [Standalone Mode]

    1. Create folder and give permission
	   
		```
		sudo mkdir -p /usr/local/hbase/standalone/tmp
		sudo chmod 777 -R  /usr/local/hbase/standalone/tmp
		sudo mkdir -p /usr/local/hbase/standalone/files
		sudo chmod 777 -R  /usr/local/hbase/standalone/files
		sudo mkdir -p /usr/local/hbase/standalone/zookeeper                 /*optional*/
		sudo chmod 777 -R  /usr/local/hbase/standalone/zookeeper            /*optional*/
		```
		
    2.  Update 
		```xml
		<configuration>
		  <property>
			<name>hbase.tmp.dir</name>
			<value>/var/hbase</value>
		  </property>
		  <property>
			<name>hbase.rootdir</name>
			<value>file:///usr/local/hbase/standalone/files</value>
          </property>
		  <property>
			<name>hbase.zookeeper.property.dataDir</name>  /*optional*/
			<value>/usr/local/hbase/standalone/zookeeper</value>
		  </property>
		</configuration>
		```
		
- Start HBase daemons  [Standalone Mode]

   ```
   sudo ./bin/start-hbase.sh
   
   After a few minutes HBase should have started, you can test this by connecting to it using the HBase shell

   ./bin/hbase shell
   
   ```		

- Update conf/hbase-site.xml for temp directory [Pseudo Distributed Mode]

  ```xml
    <configuration>
		<property>
			<name>hbase.rootdir</name>
			<value>hdfs://localhost:9000/hbase</value>
		</property>
		  
		<property>
			<name>hbase.cluster.distributed</name>
			<value>true</value>
		</property>
		
		<property>
			<name>hbase.zookeeper.quorum</name>  /*optional*/
			<value>localhost</value>
		</property>
		
		<property>
			<name>dfs.replication</name>
			<value>1</value>
		</property>


		<property>                          
			<name>hbase.zookeeper.property.dataDir</name>   /*optional - create in hdfs and give g+w permission */
			<value>/home/osboxes/hbase/zookeeper</value>
		</property>
	</configuration> 
  ```
  
- Start Hadoop daemons first and after that start HBase daemons [Pseudo Distributed Mode]

   ```
   sudo ./bin/start-hbase.sh
   
   jps
        12211 DataNode
		18263 HMaster
		12823 NodeManager
		12071 NameNode
		15271 JarBootstrapMain
		18152 HQuorumPeer
		12664 ResourceManager
		18968 Jps
		12426 SecondaryNameNode
		18447 HRegionServer

   
   After a few minutes HBase should have started, you can test this by connecting to it using the HBase shell

   ./bin/hbase shell
   
   ```

- UI

  ```
   master -> http://localhost:16010/master-status
   region server -> http://localhost:16030/rs-status
   
   
   
   To get info of ports refer -> https://blog.cloudera.com/guide-to-using-apache-hbase-ports/
   
   To list any process listening to the port 60000
   lsof -i:60000
   
   To kill process violently 
   kill -9 $(lsof -t -i:60000)
   kill -9 $(lsof -t -i:60010)
   
   sudo netstat -plten |grep java
  ```  
   
	