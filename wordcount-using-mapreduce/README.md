Project Overview

This project implements the classic WordCount example using Hadoop MapReduce.
The goal is to read a text file from HDFS, process it with a custom Mapper and Reducer, and output the frequency of each word back into HDFS.

Approach and Implementation
Mapper

Input: A line of text.

Processing:

Split the line into words (using whitespace as delimiter).

Emit each word as (word, 1).

Output: Key-value pairs of the form (word, 1).

Reducer

Input: All values corresponding to the same key (word).

Processing:

Sum the counts for each word.

Output: (word, total_count).

Execution Steps
1. Compile the project into a JAR

From project root:

mvn clean package


The output JAR will be in target/.

2. Start Hadoop cluster (via Docker Compose)
docker compose up -d

3. Copy input data into HDFS
hadoop fs -mkdir -p /input/data
hadoop fs -put input.txt /input/data

4. Run WordCount job
hadoop jar hadoop-mapreduce-examples-3.2.1.jar wordcount /input/data /output/wordcount

5. View output
hadoop fs -ls /output/wordcount
hadoop fs -cat /output/wordcount/part-r-00000

Challenges Faced & Solutions


Multiple JDK locations caused confusion

Issue: At first, %JAVA_HOME% was set to C:\Users\ram_w\Downloads (not a JDK).

Solution: Located the proper JDK installation under C:\Program Files\Eclipse Adoptium\jdk-21.0.8.9-hotspot and reset the environment variables.

Docker Engine not running

Issue: open //./pipe/dockerDesktopLinuxEngine: The system cannot find the file specified.

Solution: Ensure Docker Desktop was running and restart Docker service.

Confusion using docker exec inside container

Issue: Tried running docker exec inside container → bash: docker: command not found.

Solution: Realized docker exec is host-only; used Linux commands directly once inside.

Input.txt

# Create your own input dataset
I am Vasudha Carolina
Vasudha is studying at UNCC
UNCC is located in Charlotte
Charlotte is located in North Carolina

Output obtained

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
