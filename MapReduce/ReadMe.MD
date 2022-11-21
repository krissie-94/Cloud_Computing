Calculate Pi
Pi value calculated using  Hadoop MapReduce 

[Full Project Detail Pi Project](https://docs.google.com/presentation/d/1sqCCx1dvbiASsfoJXN6FnLvUgF7H1oKh75U3DBh0Et8/edit?usp=sharing)


Introduction

![pi_2](https://user-images.githubusercontent.com/81246356/195948468-b1e44913-4402-47d3-b0ad-6bd0b32c0ece.jpg)

Design

Technologies: 
Google Cloud Platform (GCP)
Hadoop
JAVA

![Doc-img1](https://user-images.githubusercontent.com/81246356/195948930-9b22fd98-cc90-4289-840a-479b5b63a728.jpg)
![new-img](https://user-images.githubusercontent.com/81246356/195951502-dc78a5be-b508-4cf5-b330-56984caed19e.jpg)


Implementation Steps


•	Create/ make directory of input fille to store the MapReduce Pi Program
•	Create a Java program to accept inputs for Radius and the number of pairs for x and y values.
•	Run the program and save the value in an output file.
•	Create a MapReduce program to calculate the number of inside and outside darts in and outside the board.
•	Run the MapReduce program
•	Calculate the value of Pi
•	Enable the GCP virtual Machine and connect to SSH on browser

![img-01](https://user-images.githubusercontent.com/81246356/195949239-5513d45f-3cd7-4062-9e26-52847d633b20.jpg)

![img](https://user-images.githubusercontent.com/81246356/195949401-50a372d3-c321-4913-8c07-a313c6942896.jpg)


Create Input Data


$ mkdir PiCalculation
$ cd PiCalculation
$ vi GenerateRandomNumbers.java
$ javac GenerateRandomNumbers.java
$ java -cp . GenerateRandomNumbers

![img3](https://user-images.githubusercontent.com/81246356/195949964-8dd9c45b-b1a4-4358-b194-3c4d6bc21402.jpg)

Format the file System and Setup SSH Connection

Format
$ bin/hdfs namenode -format

Start
$ sbin/start-dfs.sh

Reconnect to SSh if Connection is not working
  $ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
  $ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
  $ chmod 0600 ~/.ssh/authorized_keys


**Confirm Connection**

$ wget http://localhost:9870/


**Make the HDFS Directories**
  $bin/hdfs dfs -mkdir /user
  $ bin/hdfs dfs -mkdir /user/krisvesselee18
  $ bin/hdfs dfs -mkdir /user/krisvesselee18/picalculate
  $ bin/hdfs dfs -mkdir /user/krisvesselee18/picalculate/input
  $ bin/hdfs dfs -put ../PiCalculation/PiCalculationInput /user/krisvesselee18/picalculate/input

**Build PiCalculation java file**
  $ cd /hadoop-3.3.4
  $ vi PiCalculation.java      
	
**Compile PiCalculation.java and create a jar**


  $ bin/hadoop com.sun.tools.javac.Main PiCalculation.java
  $ jar cf wc.jar PiCalculation*class  
![img-7](https://user-images.githubusercontent.com/81246356/195950323-2bdce255-d425-4e06-b8e7-a8f5fc9a3ec6.jpg)

**Execute Mapreduce program in Hadoop and create .jar file**

 bin/hadoop jar wc.jar PiCalculation /user/krisvesselee18/picalculate/input /user/krisvesselee18/picalculate/output5
 
![img-7 1](https://user-images.githubusercontent.com/81246356/195950672-6656ab55-7c7a-43fa-bb0c-c3a46c183035.jpg)


**Run Program and Test Result**

$ bin/hdfs dfs -ls /user/krisvesselee18/picalculate/output4
 $ bin/hdfs dfs -cat /user/krisvesselee18/picalculate/output4/part-r-00000 
  
  
![img-8-1](https://user-images.githubusercontent.com/81246356/195950782-04c754f9-6a81-48eb-95fc-51f69783ee70.jpg)

![img-9](https://user-images.githubusercontent.com/81246356/195950798-5884bf35-5fe1-483d-9aca-f0e63df823a0.jpg)
![img-10](https://user-images.githubusercontent.com/81246356/195950810-dedaedc2-8d02-411f-98f8-2f8a31a6e373.jpg)
