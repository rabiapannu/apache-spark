# Apache Spark

A guide to download and install Apache Spark on Ubuntu 18.04.6.


## Step 1: Update and Upgrade

Update your system with the following commands:<br/>
sudo apt-get update<br/>
sudo apt-get upgrade -y<br/>

## Step 2: Install Java

Install java with the following command:<br/>
sudo apt install default-jdk<br/>

Check if java has been installed successfully:<br/>
java -version<br/>

## Step 3: Download Apache Spark

Download the latest version of Apache Spark from their [official page](https://spark.apache.org/downloads.html).<br/>
wget https://dlcdn.apache.org/spark/spark-3.4.0/spark-3.4.0-bin-hadoop3.tgz<br/>

Extract the Spark tarball:<br/>
tar xvf spark-3.4.0-bin-hadoop3.tgz<br/>

Move the Spark folder created after extraction to the /opt/ directory.<br/>
sudo mv spark-3.4.0-bin-hadoop3/ /opt/spark<br/>

## Step 3: Configure Spark

Open the bashrc configuration file.<br/>
sudo nano ~/.bashrc<br/>

Add the following lines and close the file:<br/>
export SPARK_HOME=/opt/spark<br/>
export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin<br/>

Activate the changes.<br/>
source ~/.bashrc<br/>

## Step 4: Start a standalone master server

start-master.sh <br/>

The process will be listening on TCP port 8080.<br/>
sudo ss -tunelp | grep 8080<br/>

## Step 5: Starting Spark Worker Process

start-slave.sh spark://ubuntu:7077<br/>

## Step 6: Using Spark shell

Run command:<br/>
spark-shell<br/>

## Step 7: Run a sample wordcount program

While in spark-shell execute the following code:<br/>

val file = sc.textFile("hdfs://localhost:9000/test/data.txt")<br/>
val counts = file.flatMap(line => line.split(" ")).map(word => (word, 1)).reduceByKey(_ + _)<br/>
counts.saveAsTextFile("hdfs://localhost:9000/test/spark_out")<br/>

View the output:<br/>
hadoop fs -ls /test/spark_out/*<br/>

You can also view the output by browsing the file system through your browser.<br/>
