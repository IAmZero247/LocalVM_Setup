# Oracle Installation - JDK / Java 8 

- Ref -> https://phoenixnap.com/kb/install-hive-on-ubuntu
  
- Apache Hive is based on Hadoop and requires a fully functional Hadoop framework

- Additional Step: Installing My SQL
  metastore : Derby / MySql*
  
  Reference: For above steps: you can refer https://www.sqlshack.com/how-to-install-mysql-on-ubuntu-18-04/

	 '''
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
	 '''  
  

  Execute below 
  
  '''
  CREATE USER 'hiveuser'@'%' IDENTIFIED BY 'Hive@123456';
  
  GRANT ALL PRIVILEGES ON *.* TO 'hiveuser'@'%' WITH GRANT OPTION;

  FLUSH PRIVILEGES;
  
  CREATE DATABASE metastore_db;
  '''

- https://hive.apache.org/downloads.html	
  https://dlcdn.apache.org/hive/hive-3.1.2/
	


 

   
	