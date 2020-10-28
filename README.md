# spark3_docker
Docker image of Spark 3 with java 1.8, python 3.8.5 and scala 2.13

step 1: install docker
https://www.docker.com/get-started

Step 2: Give docker desktop proper resources.
If you are using Windows 10 or Mac os, please make sure you give at least half of the total ram and processors of your system.
I have eight cores processors and 32 GB of Ram. So I gave six cores and 16 GB ram space to the docker hub.

Step 3: pull the Docker image using
docker pull sandipanghosh/spark3_hadoop3:latest

Step 4: Run the image using 
docker container run -it -v /host_path/docker_data/:/root/docker_data --name spark3 -p 8080:8080 -p4040:4040 spark3_hadoop3:latest /bin/bash

Here we are running the spark3_hadoop3 image and mounting a local dir called 'docer_data' to the container's location /root/docker_data.
We are also mapping the containers port 8080 and 4040 to the host ports.
We need these ports to monitor the spark jobs.

Step 5: Once you login to the container, you need to run the spark master command to create the master node. 

cd $SPARK_HOME
./sbin/start-master.sh
Once the master start running, you can log in to the master node using.
http://localhost:8080
From this page note down the URL. We need this url for creating the worker nodes.
My URL: spark://a913f8caa9b2:7077

Step 6: Create the worker nodes using 

SPARK_WORKER_INSTANCES=4 SPARK_WORKER_CORES=1 SPARK_WORKER_MEMORY=5G ./sbin/start-slave.sh spark://a913f8caa9b2:7077

Here we are creating four worker nodes assigning one core and 5GB memory to each worker node.
Adjust these values based on your system resources.

Step 7: Open the pyspark and spark scala prompt

-- Pyspark prompt
cd $SPARK_HOME
export PYSPARK_PYTHON=python3
$SPARK_HOME/bin/pyspark --master spark://a913f8caa9b2:7077

-- Spark scala prompt
cd $SPARK_HOME
$SPARK_HOME/bin/spark-shell --master spark://a913f8caa9b2:7077

Check the running jobs at
http://localhost:4040/jobs/

Other details

python3 version => python 3.8.5

scala -version
scala code runner version 2.13.3 -- Copyright 2002-2020, LAMP/EPFL and Lightbend, Inc.

which scala
root/scala-2.13.3/bin/scala

java -version
openjdk version "1.8.0_265"
OpenJDK Runtime Environment (build 1.8.0_265-8u265-b01-0ubuntu2~20.04-b01)
OpenJDK 64-Bit Server VM (build 25.265-b01, mixed mode)

which java
/usr/bin/java

pip3 -V      
pip 20.0.2 from /usr/lib/python3/dist-packages/pip (python 3.8)

SPARK_HOME="/root/spark-2.4.7-bin-hadoop2.7"

Mail me: ghoshm21@gmail.com






