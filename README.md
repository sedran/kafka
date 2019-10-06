Kafka in Docker
===

Copied from spotify/kafka because currently (06 October 2019) 
the original repository does not work to build an image
for kafka version 1.1.0.

Also, docker hub does not contain a public image for kafka 1.1.0
which is built from this repository.

For the reference, here is the original repository:

https://github.com/spotify/docker-kafka

Why?
---
The main hurdle of running Kafka in Docker is that it depends on Zookeeper.
Compared to other Kafka docker images, this one runs both Zookeeper and Kafka
in the same container. This means:

* No dependency on an external Zookeeper host, or linking to another container
* Zookeeper and Kafka are configured to work together out of the box

Run
---

```bash
docker run \
  -p 2181:2181 \
  -p 9092:9092 \
  --env ADVERTISED_HOST=`docker-machine ip \`docker-machine active\`` \
  --env ADVERTISED_PORT=9092 \
  "sedran/kafka:1.1.0_2.11"
```


Public Builds
---

https://hub.docker.com/r/sedran/kafka


Build from Source
---

    docker build \
      --build-arg "SCALA_VERSION=2.11" \
      --build-arg "KAFKA_VERSION=1.1.0" \
      -t "sedran/kafka:1.1.0_2.11" .



