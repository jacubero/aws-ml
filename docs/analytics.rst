Analytics Services
##################

Amazon Athena
*************


Amazon Elasticsearch
********************

.. _secEMR:

Amazon EMR
**********

AWS Glue
********

`What is AWS Glue? <https://www.youtube.com/watch?v=qgWMfNSN9f4&feature=emb_logo>`_

Amazon Kinesis streaming data platform
**************************************

Amazon Kinesis streaming data platform consists of Kinesis Data Firehose, Kinesis Data Streams, Kinesis Video Streams, and Amazon Kinesis Data Analytics.

Amazon Kinesis Data Firehose
============================

Amazon Kinesis Data Firehose is the easiest way to load streaming data into data stores and analytics tools. It can capture, transform, and load streaming data into Amazon S3, Amazon Redshift, Amazon Elasticsearch Service (Amazon ES), and Splunk, enabling near real-time analytics with existing business intelligence tools and dashboards you’re already using today.

It is a fully managed service that automatically scales to match the throughput of your data and requires no ongoing administration. It can also batch, compress, and encrypt the data before loading it, minimizing the amount of storage used at the destination and increasing security.

For Amazon ES destinations, streaming data is delivered to your Amazon ES cluster, and it can optionally be backed up to your S3 bucket concurrently.

.. figure:: /analytics_d/fh-flow-es.png
   	:align: center

	Amazon Kinesis Data Firehose with Amazon ES destination

Kinesis Data Streams
====================

The vocabulary for data streaming is putting records into a data stream and reading the stream back. You can have multiple shards that provide throughtput. You can create as many shards as you need with a data stream, they are not created dynamically.

Let's image a producer want to send a record, then in order to Kinesis Data Streams what shard to use, you tag the record with the partition key. This partition key is very similar to the message group identifier in a SQS FIFO queue. The process is the following:

1. The producer calls put record.

2. The Kinesis Data Streams service needs to decide to which shard this record is going to be appended. This decision is done through hashing. Each shard owns a subset of hashes. Kinesis calculates the hash for the message partition value and finds out to which shard it belongs. 

3. Amazon Kinesis Data Streams stores the record and synchronously replicates data across three availability zones, providing high availability and data durability.

4. It is return an OK back to the producer.

Image an scenario where:

1. A producer sends a record to the appropriate shard in terms of its shard.

2. The stream stores the record durably to its correspondent shard.

3. There is a networking problem when the producer was calling send message.

4. The producer gets a timeout. It doesn't know if Kinesis got the record or it didn't.

5. The producer retry the send.

6. Kinesis calculate again the record hash and sends it to the same shard as the previous version. There is going to be a duplicate.

When you need more throughput and you have already data in your data stream, you can do a shard split. You select one of the shards and split it into two: you divide the hash space of one the shards into two hash subspaces. You can scale the throughput as much as you want by adding as many shards as you want. Resharding means that it does not influence existing data, the records get appended to the new shards if applicable. You do not have to decide which shards are needed to be splitted, it is done automatically by Kinesis.

A consumer is responsible for deciding from which shard is going to consume and which record to consume. The first action that the consumer should do is to ask Kinesis what shards are available. Then it will a pick a shard and start reading from an iterator. As a consequence, with Kinesis Data Streams there is consumer affinity: a consumer read all the records from a shard. It is easy to perform analysis of consecutive entries.

When you consume from a data stream, you are not deleting any record. This means that you can start multiple applications consuming from the same stream, like a fanout pattern, doing some analysis on the data stream.

If the number of shards increases, the complexity of the code of the consumers increases as well. The consumer is responsible for keeping track who is reading, from which shard, check the progress of reading, ... Because of that, instead of using directly Kinesis API for consuming, it is recommend to use existing client-side libraries called Kinesis Client Library (KCL). This library does the complex management of shards: electing who is reading from each shard, of tracking progress of your reads, and allows to focus on the code needed to process the data in the records.

Amazon QuickSight
*****************