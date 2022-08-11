Kafka Fraud Detector

Install
This fraud detection system is fully containerised. You will need Docker and Docker Compose to run it.

You simply need to create a Docker network called kafka-network to enable communication between the Kafka cluster and the apps: docker network create kafka-network

Quickstart
Spin up the local single-node Kafka cluster (will run in the background): docker-compose -f docker-compose.kafka.yml up -d Check the cluster is up and running (wait for "started" to show up): docker-compose -f docker-compose.kafka.yml logs -f broker | grep "started" Start the transaction generator and the fraud detector (will run in the background): docker-compose up -d

Usage Show a stream of transactions in the topic T (optionally add --from-beginning): docker-compose -f docker-compose.kafka.yml exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic streaming.transactions.fraud docker-compose -f docker-compose.kafka.yml exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic streaming.transactions.legit

{"source": "yGfZ1Xa6k1r0", "target": "N5RvY7RO5sQF", "amount": 217.46, "currency": "EUR"}

Teardown
To stop the transaction generator and fraud detector:

$ docker-compose down To stop the Kafka cluster (use down instead to also remove contents of the topics):

$ docker-compose -f docker-compose.kafka.yml stop To remove the Docker network:

$ docker network rm kafka-network