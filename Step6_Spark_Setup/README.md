# Spark Setup  

- Ref: -> https://phoenixnap.com/kb/install-spark-on-ubuntu
  
- Install Spark (3.1.2)

  https://spark.apache.org/downloads.html
  
  ```
	  1. Choose a Spark release:  ->3.1.2 (Jun 01 2021)
	  
	  2. Choose a package type: ->Pre-built for Apache Hadoop 2.7
	  
	  3. Download Spark: spark-3.1.2-bin-hadoop2.7.tgz
  ``` 

- Download tar.gz file for spark-3.1.2-bin-hadoop2.7.tgz

- Untar it - tar -xzvf park-3.1.2-bin-hadoop2.7.tgz

- Copy it to /usr/local/spark

- Set up the path. Open command line and wrote "gedit ~/.bashrc"

  1. Copy below at the end of file.

  ```
  export SPARK_HOME=/usr/local/spark/spark-3.1.2-bin-hadoop2.7/
  export PATH=$PATH:$SPARK_HOME/bin
  export PATH=$PATH:$SPARK_HOME/sbin
  export PYSPARK_PYTHON=/usr/bin/python3
  ```

  2. To set path, either restart the VM or run below

     source ~/.bashrc
	 
- Start Standalone Spark Master Server

  ```
  start-master.sh
  
  To view the Spark Web user interface, 
  
  http://127.0.0.1:8080/
  
  From UI - MASTER IS RUNNING AT 7070
  ```  
  
  
- Start Spark Slave Server (Start a Worker Process)

  ```
   start-slave.sh spark://master:port
   
   start-slave.sh spark://ubuntu1:7077
   
   The default setting when starting a worker on a machine is to use all available CPU cores. 
   For example, to start a worker and assign only one CPU core to it, enter this command.:
   start-slave.sh -c 1 spark://ubuntu1:7077
   
   Similarly, you can assign a specific amount of memory when starting a worker. The default setting 
   is to use whatever amount of RAM your machine has, minus 1GB.:
   start-slave.sh -m 512M spark://ubuntu1:7077
  ``` 

- Test Spark Shell 

  ```
  spark-shell
  Type :q and press Enter to exit Scala
  
  
  py-spark 
  To exit this shell, type quit() and hit Enter.
  ```  

- Basic Commands to Start and Stop Master Server and Workers

  ```
  start-master.sh
  stop-master.sh
  
  start-slave.sh
  stop-slave.sh
  
  start-worker.sh
  stop-worker.sh 
  
  $SPARK_HOME/sbin/start-all.sh
  $SPARK_HOME/sbin/stop-all.sh
  ```  
  

 

   
	