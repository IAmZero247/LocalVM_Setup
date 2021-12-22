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
	export HIVE_HOME=/usr/local/hive/hive-2.3.6
	export HIVE_CONF_DIR=${HIVE_HOME}/conf
	export PATH=$PATH:$HIVE_HOME/bin
	export CLASSPATH= $CLASSPATH:${HADOOP_HOME}/lib/*:.
	export CLASSPATH=$CLASSPATH:${HIVE_HOME}/lib/*:.
	```
	
 2. To set path, either restart the VM or run below

    source ~/.bashrc	
	
	
- HIVE_HOME/bin/schematool -initSchema -dbType mysql	


 

   
	