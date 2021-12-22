# Hive Installation 

- Ref -> https://phoenixnap.com/kb/install-hive-on-ubuntu
  
- Apache Hive is based on Hadoop and requires a fully functional Hadoop framework

- Additional Step: Installing My SQL
  metastore : Derby / MySql*
  
  1. Reference: For above steps: you can refer https://www.sqlshack.com/how-to-install-mysql-on-ubuntu-18-04/

	 ```
	 sudo apt-get update
	 sudo apt-get upgrade
	 sudo apt-get install mysql-server
	 sudo mysql_secure_installation
	  
	  [ 
	  user -> root
	  password -> samplepassword
		]

	 sudo "mysql -u root -p " 

	 type password and verify.
	 ```  
  

  2. Execute below 
  
  ```
  CREATE USER 'hiveuser'@'%' IDENTIFIED BY 'Hive@123456';
  
  GRANT ALL PRIVILEGES ON *.* TO 'hiveuser'@'%' WITH GRANT OPTION;

  FLUSH PRIVILEGES;
  
  CREATE DATABASE metastore_db;
  ```

- Installation of Hive - Download With help of below Link 
  
  1. https://hive.apache.org/downloads.html	
    
  2. https://dlcdn.apache.org/hive/hive-3.1.2/
  
- Untar it 
  
  tar -xzvf hive-3.1.2.tar.gz  
  
- Copy it to /usr/local/hive  

- Set up the path. Open command line and wrote "gedit ~/.bashrc"
  
    1. Copy below at the end of file.
    
	```
	export HIVE_HOME=/usr/local/hive/hive-3.1.2
	export HIVE_CONF_DIR=${HIVE_HOME}/conf
	export PATH=$PATH:$HIVE_HOME/bin
	export CLASSPATH= $CLASSPATH:${HADOOP_HOME}/lib/*:.
	export CLASSPATH=$CLASSPATH:${HIVE_HOME}/lib/*:.
	```
	
    2. To set path, either restart the VM or run below

    source ~/.bashrc	

- Edit hive-config.sh file

  Open file -> $HIVE_HOME/bin/hive-config.sh	
  
  Add Below 
  
  export HADOOP_HOME=/usr/local/hadoop/hadoop-3.2.2
  
- Create Hive Directories in HDFS

  1. Create a tmp directory within the HDFS storage layer. This directory is going to store the intermediary data Hive sends to the HDFS:
        
		```
		hdfs dfs -mkdir /tmp
		Add write and execute permissions to tmp group members:

		hdfs dfs -chmod g+w /tmp
		Check if the permissions were added correctly:

		hdfs dfs -ls /  
	    ```
		
  2. Create the warehouse directory within the /user/hive/ parent directory:
        
		```
		hdfs dfs -mkdir -p /user/hive/warehouse
		Add write and execute permissions to warehouse group members:

		hdfs dfs -chmod g+w /user/hive/warehouse
		Check if the permissions were added correctly:

		hdfs dfs -ls /user/hive
        ```
- Configure hive-site.xml File	
     
	1.  Use the hive-default.xml.template to create the hive-site.xml file:

       ```
	   cd $HIVE_HOME/conf
	   cp hive-default.xml.template hive-site.xml
		```	   
		
		
	2. Access the hive-site.xml file using the nano text editor:
      
	  ```
      Using Hive in a stand-alone mode rather than in a real-life Apache Hadoop cluster is a safe option.
	  You can configure the system to use your local storage rather than the HDFS layer by setting the 
	  hive.metastore.warehouse.dir parameter value to the location of your Hive warehouse directory.
	  
	  <property>
		<name>hive.metastore.warehouse.dir</name>
		<value>/user/hive/warehouse</value>
		<description>location of default database for the warehouse</description>
	  </property>
	  ```	


- How to Fix guava Incompatibility Error in Hive

     ```
	  rm $HIVE_HOME/lib/guava-19.0.jar
	  cp $HADOOP_HOME/share/hadoop/hdfs/lib/guava-27.0-jre.jar $HIVE_HOME/lib/
	 ```
	 
- Remove The special Character From hive-site.xml  [Line 3215 #]

    ```
	cat hive-site.xml | grep hive.txn.xlock.iow -n 
   
    remove "&#8" and save
    ```

- HIVE java net URISyntaxException - Update Following in hive-site.xml

   ```xml
   <property>
   <name>hive.exec.scratchdir</name>
   <value>/tmp/hive-${user.name}</value>
   </property>
   <property>   
   <name>hive.exec.local.scratchdir</name>
   <value>/tmp/${user.name}</value>
   </property>
   <property>
   <name>hive.downloaded.resources.dir</name>
   <value>/tmp/${user.name}_resources</value>
   </property>
   <property>
   <name>hive.scratch.dir.permission</name>
   <value>733</value>
   <property>   
   ```   
- Initiate Derby Database and Test 	 
      
      ```
	  $HIVE_HOME/bin/schematool -dbType derby -initSchema	


      cd $HIVE_HOME/bin
      hive
	  
	  show databases;
	  ```	  
		
- Update metastore to MySql

    1. Download jar and copy to 
	   
	     
		 https://dev.mysql.com/downloads/connector/j/
		 
		 choose platform independent , download Compressed TAR Archive. Unzip and copy the jar mysql-connector-java-8.0.27.jar to location 
		 HIVE_HOME/lib directory
		 
		 Ref -> https://www.linkedin.com/pulse/changing-hive-metastore-db-mysql-from-derby-mohamed-k-1
		 

    2. Add Below to hive-site.xml
  

		 ```xml 
			 <property>
			  <name>javax.jdo.option.ConnectionURL</name>
			  <value>jdbc:mysql://localhost/metastore_db?createDatabaseIfNotExist=true</value>
			  <description>JDBC connect string for a JDBC metastore </description>
			 </property>
			 <property>
				<name>javax.jdo.option.ConnectionDriverName</name>
				<value>com.mysql.jdbc.Driver</value>
				<description>Driver class name for a JDBC metastore</description>
			 </property>
			 <property>
			   <name>javax.jdo.option.ConnectionPassword</name>
			   <value>Hive@123456</value>
			   <description>password to use against metastore database</description>
			 </property>
			 <property>
			   <name>javax.jdo.option.ConnectionUserName</name>
			   <value>hiveuser</value>
			   <description>Username to use against metastore database</description>
			 </property>   
		 ```	  

    3.   HIVE_HOME/bin/schematool -initSchema -dbType mysql	
	
	4.   Restart Hadoop/Hive if needed 
	   
			```
			cd $HIVE_HOME/bin
			hive
			show databases;
			 
			 
			Then create a table in it and insert one record.
			 
			hive> create table testm1(id int, name string);
            hive> insert into testm1 values(1, “Helical”);

			Later access your MySQL and open metastore database

			sudo mysql -u root -p
            
			Enter password: samplepassword

            mysql> use metastore;
			mysql> show tables ;
			mysql> select * from TBLS;
			```


 

   
	