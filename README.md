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

Add jar files from `build/libs/` and `build/third-party/` directories to Connect plugin path.

Plugin path is specified in connect-standalone.properties file.

`sink.properties` are modified according to the link above.

Run the MongoDB-Sink-Connector in `standalone` mode
```
connect-standalone /etc/schema-registry/connect-avro-standalone.properties ./sink.properties
```

**Generate Avro Data**

You can find the Java files above.   
Before running the Java codes make sure docker containers are running.     
Firstly run the Consumer file, and then the Producer file without stopping it.

--------------------------------------------------------------------------

**Second Option**

1. Install Confluent (https://docs.confluent.io/current/installation/installing_cp/zip-tar.html)  
2. After installation you need to change some configurations in the following locations. 
`/etc/kafka/server.properties`, `/etc/confluent-control-center/control-center-production.properties`, `/etc/kafka/connect-distributed.properties`, `/etc/schema-registry/schema-registry.properties`.    
3. The configurations are shown in the link.  
4. Start Confluent Platform using these commands (remember to use your own paths)  
```
$ <path-to-confluent>/bin/zookeeper-server-start <path-to-confluent>/etc/kafka/zookeeper.properties
$ <path-to-confluent>/bin/kafka-server-start <path-to-confluent>/etc/kafka/server.properties
$ <path-to-confluent>/bin/schema-registry-start <path-to-confluent>/etc/schema-registry/schema-registry.properties
// control center
$ <path-to-confluent>/bin/control-center-start <path-to-confluent>/etc/confluent-control-center/control-center.properties
// kafka connect
$ <path-to-confluent>/bin/connect-distributed <path-to-confluent>/etc/schema-registry/connect-avro-distributed.properties
// rest proxy
$ <path-to-confluent>/bin/kafka-rest-start <path-to-confluent>/etc/kafka-rest/kafka-rest.properties
// ksq
$ <path-to-confluent>/bin/ksql-server-start <path-to-confluent>/etc/ksql/ksql-server.properties
```
