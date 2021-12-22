# Scala Installation  

- Ref : https://www.scala-lang.org/download/scala2.html 


    Download the Scala binaries for linux	
	
- Install Scala (2.13.7)

1. Download tar.gz file for scala 2.13.7
2. Untar it - tar -xzvf scala-2.13.7.tar.gz
3. Copy it to /usr/local/scala
4. Set up the path. Open command line and wrote "gedit ~/.bashrc"

	1. Copy below at the end of file.
    
	```
	export SCALA_HOME=/usr/local/scala/scala-2.13.7/
	export PATH=$PATH:$SCALA_HOME/bin
    ```
	
    2. To set path, either restart the VM or run below

    
	source ~/.bashrc
	
	
	3. Verify 
	
	  ```
	  scala -version 
	  
	  
	  scala 
	  
	  scala>  1+2
	  ```


 

   
	