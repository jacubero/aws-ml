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

Amazon QuickSight
*****************