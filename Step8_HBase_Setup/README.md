# HBase  

- Ref1: https://prwatech.in/blog/hadoop-admin-2/sqoop-installation-in-manual-cluster/
  
- https://hbase.apache.org/

- Download -> https://www.apache.org/dyn/closer.lua/hbase/2.4.8/hbase-2.4.8-bin.tar.gz

- tar  -xvf hbase-2.4.8-bin.tar.gz

- Copy it to /usr/local/hbase

- Make a directory for our HBase data
   
   ```
   sudo mkdir -p /usr/local/hbase/hbase-data
   
   Give 777 permissions 
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
  export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre
  ``` 

- Update conf/hbase-site.xml for temp directory

  ```xml
    <configuration>
		  <property>
			<name>hbase.tmp.dir</name>
			<value>/var/hbase</value>
		  </property>
	</configuration>
  ```
  
- Start HBase by running the start-hbase script

   ```
   sudo ./bin/start-hbase.sh
   
   After a few minutes HBase should have started, you can test this by connecting to it using the HBase shell

   ./bin/hbase shell
   
   ```
	