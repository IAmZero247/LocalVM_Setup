# Squoop  

- Ref1: https://prwatech.in/blog/hadoop-admin-2/sqoop-installation-in-manual-cluster/

- Ref2: https://sqoop.apache.org/docs/1.4.7/SqoopUserGuide.html
  
- https://sqoop.apache.org/	

- Download -> http://archive.apache.org/dist/sqoop/1.4.7/

- tar  -xvf sqoop-1.4.7.bin_hadoop-2.6.0.tar.gz

- Copy it to /usr/local/sqoop

- Edit the .bashrc file

    ```
	export SQOOP_HOME=/usr/local/sqoop/sqoop-1.4.7
	export PATH=$PATH:$SQOOP_HOME/bin
	
	
	source ~/.bashrc

	```
	
- Use the sqoop-env-template.sh to create the sqoop-env.sh file:

  ```
  cp sqoop-env-template.sh sqoop-env.sh
  
  Add below to sqoop-env 
  export HADOOP_HOME=/usr/local/hadoop/hadoop-3.2.2
  export HADOOP_INSTALL=$HADOOP_HOME
  export HADOOP_MAPRED_HOME=$HADOOP_HOME
  export HADOOP_COMMON_HOME=$HADOOP_HOME
  ``` 

- Download MySql Jar [Refer Hive installation to get same jar]
 
  ```
   wget  http://ftp.ntu.edu.tw/MySQL/Downloads/Connector-J/mysql-connector-java-8.0.22.tar.gz
   
   tar -xvf mysql-connector-java-8.0.22.tar
   
   mv mysql-connector-java-8.0.22/mysql-connector-java-8.0.22.jar /usr/local/sqoop/sqoop-1.4.7/lib
  ``` 
  
- Check the version whether it is installed and Verify. 

   ```
     sqoop version
     sqoop help
   ```   
	
- Try : https://www.hdfstutorial.com/blog/how-to-import-data-from-mysql-to-hive-using-sqoop/
 

   
	