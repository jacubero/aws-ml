ML Building Blocks: Services and Terminology
############################################

Introduction to AWS Machine Learning Services
*********************************************

`AWS Machine Learning Services <https://aws.amazon.com/amazon-ai/>`_

The machine learning stack has 3 key layers:

* Frameworks and Infrastructure.

* Machine Learning platforms.

* API-driven services

The bottom layer provides the framework and infrastructure for machine learning experts who are comfortable building deep learning models, training them, doing inference, and getting the data from their models into production applications. For this group, the vast majority of machine learning and deep learning that's done in the cloud is running on AWS.

The optimized GPU-based instances and the Deep Learning AMI are specifically designed to help expert practitioners get started quickly using their preferred framework. Choice is important, which is why the Deep Learning AMI has all the major frameworks installed, including:

* *Apache MXNet*, which is great for recommendation engines.

* *Caffe* and *Caffe 2*, which are popular for computing vision projects.

* *Tensorflow*.

The second layer of the stack is for customers who want a fully managed platform for building models using their own data. Examples are:

* Apache Spark on Amazon EMR.

* SparkML.

The top layer of this stack is for developers and organizations who want to add intelligence to their applications using an API call rather than developing and training their own models. API based tools are the following:

* *Amazon Rekognition* allows developers to build image analysis directly into their applications, helping them extract rich meta data from visual content. This can be used to perform facial recognition, which allows companies to automatically tag their video content, and it works whether content is archived or freshly ingested.

* *Amazon Polly* allows customers to easily turn text into lifelike speech across many different voices and many different languages.

* *Amazon Lex* which helps developers build intelligent conversational interfaces for existing and new applications. Lex uses the same automated speech recognition and natural language understanding technology that fuels Amazon Alexa. Alexa is often deployed to save cost by automating high frequency interactions with customers and employees, while preserving a high quality user experience.

It's important to remember that machine learning is not an isolated capability but part of an application architecture that builds on the quality of the underlying data. To be good at machine learning, you need a data store that is scalable, available, secure, and flexible. This data lake must handle extremely large data sets, and Amazon S3 is the AWS storage option that hosts the vast majority of data that is stored in the cloud. Once data is in S3, it becomes available for analysis, and AWS provides a broad range of options for data analytics, with services like Amazon Athena, Amazon Redshift, and Redshift Spectrum. Amazon EMR provides access to frameworks like Apache Spark, Presto, Hive, and Pig. 

Machine Learning terminology and process
****************************************

Terminology
===========

**Training** refers to how the machine learning use historical datasets to build their predictions algorithms. This algorithms make up the **model**, which is the core of the machine learning process. It is what your machine creates after it has been trained and refines over time as it learns. It is what enable the machine to determine output variable from input data, which is then used to generate a **prediction**. A prediction is the machine best estimate for what would be the outcome of a given input or set of inputs would be. It is sometimes called the **inference** of your model.

In a typical traning process, the historical data is used to build the model is splitted into 2 datasets: most of data is used as the training dataset and the remainder is used as the test dataset. The training dataset is inputted into the machine, evaluated by it, and used by the machine to create the first model. The test dataset is then used to test the model for accuracy: It is inputted into the model and the output the model produces from their input is compared with the actual output stored in the test dataset. The close the model predictions are to the real world results in the test dataset the more accurate the model likely is. It is important to understand that training is one of the more important parts of the machine learning process but it is not the whole picture.

Process
=======

Machine learning starts with a business problem and results in a prediction. The goal of machine learning is to address a business problem and this happens by providing accurate predictions. If predictions are not accurate, the machine learning has to get better by providing feedback that improves the way it handles input data and the way to identify features in the data. The key stages of the machine learning process are the following:

ML Problem Framing from the business problem 
--------------------------------------------

This is the point in the project in which we will decide what we will actually use and how to use it. This is the place to ask questions like *Do we have all the data needed to answer the business question? What algorithm do we use to answer this business question?* Depending on the amount of data and whether we have a dataset with previously known answers, we can find which type of learning we can do. There are 3 common types of machine learning algorithms: Supervised, unsupervised and reinforcement. In a supervised learning algorithm we will learn from the historical dataset with the answers already known and we will feed them in the machine learning algorithm to predict the future data points. In unsupervised learning algorithms the outcome isn't kwnown beforehand so we let the machine learning algorithm choose how to quantify the data and give us a result. In reinforcement learning the algorithm is rewarded based on the choices it made while learning.

In classification problems, we categorized object into fixed categories. A binary classification problem is when there are only 2 classes in the data. A multiclass classification problem is when there are more than 2 classes.

To frame the machine learning problem, we need to find the output of the problem to evaluate. To structure that output we can use attributes from our dataset: this are called observations. We can also predict future outcomes and this attribute is called the label. To predict the labels from unseen data we will use all other attributes in the dataset, which are called features.

Develop the dataset
-------------------

If we have that one dataset, we can start integrating the data in one dataset or we can collect all the datasets if there are not in one location, to begin with. We can collect data from multiple sources Amazon S3, Amazon DynamoDB, Amazon Redshift or can be collected simply from the Internet. Wherever the data comes from only it needs to be collected and integrated.

The collected data can be classified into 3 distinct types: 

* *Structured* data is data that is organized and stored in databases in the form of rows and columns. This makes query and analysis easy but structured data only makes a chunk of the total available data.

* *Semi-structured* data is data that is typically organized in one the familiar formats but not in tables. This formats include csv, JSON, and more.

* *Unstructured* data is the data that does not have any structure. It is by far the most common type of data. Examples include logs generated by applications servers, text, video and music content among many others.

Data Preparation
----------------

At this point, we have our data in one place but is not ready to use to train a model. The data found in the real world is dirty and noisy, meaning it has been improperly collected or formated or it is incomplete, irrelevant or misleading. Because of this, data has to go to some steps before it can be used from training. Putting our data through these steps results in better accuracy and predictions. In preparing our data, we also convert it in an appropriate input format for ingestion into a machine learning algorithm. We can aldo add headers to the columns and convert the columns types.

The presence of missing feature values and outlier can hurt our model performance. The model can suffer because of these data points in addition to the possibility of noisy data or attributes that have missing values. We should clean these ones. We can transform data points using various techniques. Here are some strategies to handle missing values and outliers:

* Introduce a new indicator variable that tells us which represent a missing value.

* Remove the rows that has missing values.

* Imputeation to fill up the missing values. This techniques utilizes the best guess of what the data likely is. It replaces a missing value with a value from the dataset which may be a calculated guess for the data point. For example, if the missing attribute is numerical, you can replace it with the mean or the median. When it is done correctly, imputation immproves the model performance dramatically.

We do not want to model to learn anything based on the order of the data presented, so it is common practice to shuffle the training dataset. This generalizes the model, which improves its quality and its predictive performance. It minimizes the risk of cross validation data under representing the model data and model data not learning from all type of data.

.. code-block:: console

	train_data = train_data.sample(frac=1)

The goal of the machine learning model is to generalize a use case based on the training data that it learns from. From this examples, the model has to predict new examples accurately. To do this, we hold out some of the data from the original dataset: this is splitting the data. The split is generally 80% train and 20% test or 70% train and 30% test. Spliting the data is a validation technique called cross-validation. We can further split the training data into even smaller validation test dataset so that we can evaluate how the model is doing while training and tuning the hyperparameters.

The cross-validation technique can consists of 3 different types:

1. *Validation* where the data is split into train and test datasets. It keeps a lot of data as unseen.

2. *Leave-one-out (LOO CV)*. We only use 1 data point as a test sample and we run the training with the other examples. It`s worth noting that this technique is computationally expensive.

3. *K-fold*. We randomly split the cases into K-folds and for each fold we train the model and record the error.

.. _secSageMaker:

Amazon SageMaker
****************


.. _secComprehend:

Amazon Comprehend
*****************
