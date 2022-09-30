# BDTProject
1. cd /usr/lib/Kafka/kafka_2.13-2.8.0

2. Start Kafka broker  
    bin/kafka-server-start.sh config/server.properties

3. create Kafka topic
    bin/kafka-topics.sh --zookeeper localhost:2181 --create --topic TwitterTopic --partitions 2 --replication-factor 1

4. Open Producer console 
    bin/kafka-console-producer.sh --broker-list localhost:9092 --topic TwitterTopic

5. Open Consumer console 
    bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TwitterTopic

6. Create a hive table to store the twitter logs
    CREATE EXTERNAL TABLE IF NOT EXISTS TwitterData(
        createdAt STRING, 
        UsertName STRING,
		ScreenName STRING,
        FollowersCount STRING,
		FriendsCount STRING,
		FavouritesCount STRING,
        Location STRING,
		RetweetCount STRING,
		FavoriteCount STRING,
        Lang STRING,
		Source STRING)
    COMMENT 'Twitter Live Data'
    ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
    WITH SERDEPROPERTIES (
    "separatorChar" = ",",
    "quoteChar" = "\"" )
     LOCATION '/user/cloudera/twitterImport1';

7. Run KafkaProducerTwitter.java class

8. Run KafkaConsumerSparkStream class

9. Retrieve the data from Hive
    SELECT * FROM default.twitterdata 
    where twitterdata.followerscount > 100000
    LIMIT 100;
