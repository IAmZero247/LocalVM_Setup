# Oracle Installation - jdk / java 8 

- Option 1: sudo apt-get install openjdk-8-jdk {Not recommended}
  
- Option 2: download a tar.gz file, untar it to a location,
	and set the path in .bashrc file {Recommended}

1. Download tar.gz file for jdk 1.8
2. untar it 
3. copy it to /usr/local/java
4. set up the path. Open command line and wrote "gedit .bashrc"
      Note  -> To Locate .bashrc use  
               
			   ls -la ~/ | more


   - Copy below at the end of file.
		a. export JAVA_HOME=/usr/local/java/jdk1.8.0_261
		b. export PATH=$PATH:$JAVA_HOME/bin

   - Note: To set path, either restart the VM or run below

        source ~/.bashrc

5. update alternatives
	- sudo update-alternatives --install "/usr/bin/java" "java" "/usr/local/java/jdk1.8.0_261/bin/java" 1
	- sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/local/java/jdk1.8.0_261/bin/javac" 1
    - sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/local/java/jdk1.8.0_261/bin/javaws" 1


 

   
	