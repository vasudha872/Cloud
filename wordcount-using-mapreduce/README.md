WordCount using Hadoop MapReduce
** Project Overview**

This project implements the classic WordCount example using Hadoop MapReduce.
The goal is to read a text file from HDFS, process it with a custom Mapper and Reducer, and output the frequency of each word back into HDFS.

Approach and Implementation
Mapper

Input: A line of text

**Processing**:

Split the line into words (using whitespace as delimiter).

Emit each word as (word, 1).

Output: Key-value pairs of the form (word, 1)

**Reducer**

Input: All values corresponding to the same key (word)

Processing:

Sum the counts for each word.

Output: (word, total_count)

**1.Start Hadoop Cluster**

docker compose up -d

**2.Build the Project with Maven**

mvn clean package

**3.This creates the JAR at**: target/WordCountUsingHadoop-0.0.1-SNAPSHOT.jar

**4.Copy JAR and Input File to Container**

docker cp target/WordCountUsingHadoop-0.0.1-SNAPSHOT.jar resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/ docker cp shared-folder/input/data/input.txt resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/

**5.Enter the ResourceManager Container**

docker exec -it resourcemanager /bin/bash cd /opt/hadoop-3.2.1/share/hadoop/mapreduce/

**6.Load Input into HDFS**

hadoop fs -mkdir -p /input/data hadoop fs -put -f ./input.txt /input/data

**7.Run the MapReduce Job**

hadoop jar WordCountUsingHadoop-0.0.1-SNAPSHOT.jar com.example.controller.Controller /input/data/input.txt /output1

**Challenges Faced & Solutions**

JAVA_HOME not set correctly

Issue:

The JAVA_HOME environment variable is not defined correctly


Cause: JAVA_HOME was pointing to the bin folder instead of the JDK root.

Solution: Updated the environment variable to the JDK installation root (e.g.,
C:\Program Files\Eclipse Adoptium\jdk-21.0.8.9-hotspot) and verified with:

echo %JAVA_HOME%
java -version
mvn -version


Multiple JDK locations caused confusion

Issue: At first, %JAVA_HOME% was set to:

C:\Users\ram_w\Downloads


which is not a valid JDK path.

Solution: Located the proper JDK installation under

C:\Program Files\Eclipse Adoptium\jdk-21.0.8.9-hotspot


and reset the environment variables.

Docker Engine not running

Issue:

open //./pipe/dockerDesktopLinuxEngine: The system cannot find the file specified.


Solution: Started Docker Desktop and restarted the Docker service to ensure the engine was available.

Confusion using docker exec inside container

Issue: Tried to run docker exec while already inside a container:

bash: docker: command not found


Solution: Realized docker exec must be run from the host; once inside the container, only Linux commands are needed.

**Input and Obtained Output**
Input (sample input.txt)
I am Vasudha Carolina
Vasudha is studying at UNCC
UNCC is located in Charlotte
Charlotte is located in North Carolina

**Output (part-r-00000)**
Vasudha	2
Carolina	2
Charlotte	2
located	2
UNCC	2
North	1
dataset	1
your	1
studying	1
own	1
input	1
Create	1
