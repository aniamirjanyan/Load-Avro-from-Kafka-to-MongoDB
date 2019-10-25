# Load-Avro-from-Kafka-to-MongoDB

Prerequisites are  
- docker  
- git  
- JDK 8

**Start Confluent on Docker** (https://docs.confluent.io/current/quickstart/ce-docker-quickstart.html)  
1. Clone the Confluent Image Git Repository
```
$ git clone https://github.com/confluentinc/examples
$ cd examples
$ git checkout 5.3.1-post
```

2. Navigate to cp-all-in-one directory and build Kafka Connect image
```
$ cd cp-all-in-one/
$ sudo docker-compose up -d --build
```

3. Check if the Images are up and running
```
sudo docker-compose ps
```


**MongoDB Installation**
```
$ sudo apt-get update
$ sudo apt install mongodb
$ sudo systemctl start
```
To enter the mongodb environment type `mongo` in terminal.

**MongoDB-Sink-Connector** (https://github.com/RADAR-base/MongoDb-Sink-Connector)  
For downloading the Sink Connector you need JDK of verison 8.
```
$ git clone https://github.com/RADAR-base/MongoDb-Sink-Connector.git
$ cd MongoDb-Sink-Connector
$ ./gradlew clean build
```
Make sure zookeeper, kafka-server, schema registry and kafka-rest are running.

Move jar file from 


**Generate Avro Data**
You can find the Java files above.   
Before running the Java codes make sure docker containers are running.   






