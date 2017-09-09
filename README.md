# Process PeopleSoft Sync Messages into Kafka Topics

[![](https://images.microbadger.com/badges/image/ucalgary/ps-stream.svg)](https://microbadger.com/images/ucalgary/ps-stream) [![Anchore Image Overview](https://anchore.io/service/badges/image/a26f2562a708b063d8bf1e0f685f0b2bc75bde1725a787588d1be531b23f06ff)](https://anchore.io/image/dockerhub/a26f2562a708b063d8bf1e0f685f0b2bc75bde1725a787588d1be531b23f06ff?repo=ucalgary%2Fps-stream&tag=latest)

`ps-stream` is a Python utility that collects and and parses [PeopleSoft rowset-based messages](http://docs.oracle.com/cd/E66686_01/pt855pbr1/eng/pt/tibr/concept_PeopleSoftRowset-BasedMessageFormat-0764fb.html) generated by sync and fullsync services into Kafka messages and topics. PeopleSoft sync processes are normally used to sync data between PeopleSoft applications. However, they can also be used as a way to generate an externalized stream of PeopleSoft objects in streaming data pipelines.

There are two major commands in `ps-stream`.

**`collect`** accepts PeopleSoft rowset-based messages over http or https, and produces a Kafka message for each transaction in the PeopleSoft message, stored in one or more Kafka topics.

**`parse`** consumes transaction messages stored by `collect` and produces Kafka messages in topics with `KTable` semantics. Each record in the resulting stream is oriented to reflect records whose record key is the primary key or identifier of the transaction message.

## Running a ps-stream container

Collect PeopleSoft sync messages.

```
$ docker run -p 8000:8000 -d ucalgary/ps-stream collect
```

## Maintenance

This repository and image are currently maintained by the Research Management Systems project at the [University of Calgary](http://www.ucalgary.ca/).
