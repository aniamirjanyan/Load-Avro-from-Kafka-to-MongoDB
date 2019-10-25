# Load-Avro-from-Kafka-to-MongoDB

Prerequisites are
-docker
-git

**Start Confluent on Docker**
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
