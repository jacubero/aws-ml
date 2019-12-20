The Data Science and ML workflow
################################


Typical ML workflow

Image: MLworkflow.png

El de arriba es Data Augmentation y el de abajo Feature Augmentation.

Phase 1: Discovery
******************

1.1 Learning the Business Domain
================================

In this phase, I start learning the domain area of the problem. 

Domain knowledge:

* Understand how the domain works, important dynamics and relationships, constraints, how data is generated, etc.

* Better understading of domain leads to better features, better debugging, better metrics, better business value to create, etc.

When domain is outside expertise then:

Consult domain experts:

* AWS ML Specialist SAs

* AWS Professional services

* AWS ML solutions lab: Developing machine learning skills through collaboration and education: Brainstorming sessions, custom modeling, training, on-site with Amazon experts

Seek other resources: AWs Partner Network

1.2 Resources
=============

I assess the resources available to perform the analysis: tools, data. 

1.3 Framing the problem
=======================

I frame the problem in order to state the analytics problem to be solved and establish the success criteria. Understand the business problem you're trying to solve. Be sure machine learning will provide the best solution.

What is the problem you need to solve?
--------------------------------------

Precisely describe the business problem that you are trying to solve. Example: Create a way to classify whether the customer credit card transaction is fraudulent.

What is the business metric?
----------------------------

Determine appropriate metrics to measure: Quality and Impact of the solution. Link financial impact with analytics metrics. Example: rate at which customers are misclassified.

Is ML the appropriate approach?
-------------------------------

Can the problem be solved with rules or standard coding? Are the patterns too difficult to capture algorithmically? Is there a lot of data available from which to induce patterns?

What data is available?
----------------------- 

Summarize the data available. Determine the gap between the data you want and the actual data that is available. Is there a way to add more data? What are the data sources?

What type of ML problem is it?
------------------------------

Characterize the ML problem according to dimensions. Decompose the business problem into a few models.

What are your goals?
--------------------

Establish technical ML goals. Define the criteria for success ful outcome of the project.

1.4 Developing Initial Hypotheses
=================================

I develop a set of Initial Hypotheses (IH), that is, form ideas that I can test with data. As a best practice, it is best to come up with a few primary hypotheses to test and then develop several more. These IHs form the basis of the analytical tests I will use in later phases and serve as the foundation for the findings in *Communicate Results*. 

1.5 Identify potential data sources
===================================

Finally, I identify potential data sources to solve the problem performing 5 main activities:

* Identify data sources: I will make a list of candidate data sources I may need to test the initial hypothesis. 

* Capture aggregate data sources: This is for previewing the data and providing high-level understanding. It enables me to gain a quick overview of the data and perform further exploration on specific areas. I also points me to possible areas of interest within the data.

* Review the raw data: Obtain preliminary data from initial data feeds. Begin understanding the interdependencies among the data attributes, and become familiar with the contents of the data, its quality, and its limitations.

* Evaluate the data structures and tools needed.

* Scope the sort of data infrastructure needed for this type of problem.

I can move to next phase when I have enough information to draft an analytics plan and share it for peer review.

Data sources:

Image: sources.png

*************************
Phase 2: Data Preparation
*************************

This phase includes the steps to explore, preprocess, and condition data prior modeling and analysis. 

2.1 Preparing the analytics sandbox
===================================

The first subphase will be to obtain an analytic sandbox or workspace in which we can explore the data. 

2.2 Performing ELT
==================

Secondly, in other to learn and become familiar with the data, I will use some tool to perform ELT (extract, load and transform data from the data sources). 

The importance of being unbiased. Issues to watch for with sampling. Labeling components and tools. Managing labelers.

Data collection: the process of acquiring training and/or test data

Motivation: Initial datasets for training models and measuring success. Additional data for tuning. Replacements for flawed or outdated sets. Data and model maintenance post-production.

Sources: Logs, Datasets, Web sites (crawling and scraping), Data providers (public or private)

Open data:

AWS provides a comprehensive toolkit for sharing and analyzing data at any scale. When organizations make data open on AWS, the public can analyze it quickly and easily with AWS scalable computing and analytics services.

Registry of open data on AWS. This registry exists to help people discover and share datasets that are available via AWS resources.

Sampling
--------

Sampling= selecting a subset of instances for training and testing. Instance = example = data point

Labeling= Obtaining gold-standard answers for supervised learning. => Key for successful machine learning algorithm

2 strategies: random and stratified. The choice depends on the business problem you are trying to solve.

The sample must be a good representation of the population.

Representativity: Sample needs to be representative of the expected production population; i.e. unbiased

 * Especially important for testing and measurement sets

 * It's also important for training sets to get good generalization

Random sampling: Sampling so that each source data point has equal probability of being selected

Issue: with random sampling, rare subpopulations can be underrepresented (or not presented at all). A subpopulation is usually defined as examples within the same label.

Stratified sampling: Apply random sampling to each subpopulation separately. Usually, the sampling probability is the same for each stratum. If not, weights can be used in metrics and/or directly in training.

Common issues in sampling
^^^^^^^^^^^^^^^^^^^^^^^^^

**Seasonality**: Time of day, day of week, time of year (e.g. seasons), holidays, special events, etc.

* Stratified sampling across these can miminize bias

* Visualization can help

**Trends**: Patterns can shift over time and new patterns can emerge

* To detect, try comparing models trained over different time periods

* Visualization can help

Consider using validation data that was gathered after your training data was gathered

**Leakage**

Train/test bleed: Inadvertent overlap of training and test data when sampling to create datasets.

* Sample from fresh data

* Filter out already selected instances

* Partition source data along some dimension (but avoid bias)

* Be especially careful with time-series data and data with duplicate entries

Leakage: Using information during training or validation that is not available in production

* Kaufman, Shachar, et al. Leakage in data mining: Formulation, detection and avoidance. ACM Transactions on Knowledge Discovery from Data (2012): 15

Labeling
--------

Motivation: Often labels are readily available in sampled data.

Examples

* Search: The results a customer wanted to receive

* Music categorization: The genre of a pice

* Sentiment analysis: The overall attitude of the writer.

* Digitization: The transcription of handwriting

* Object detection: The localization of objects in images

Sometimes labels can be inferred (for example, from click-through data)

Human labels can be preferable to minimize bias, capture subtleties, etc.

When using human labeling you have the following components:

* **Labeling guidelines**: Instructions to labelers. Critical to get right. Minimize ambiguity.

* **Labeling tools**: Technology: Excel spreadsheets, Amazon Mechanical Turk, custom-built tools. Questions: Human intelligence Tasks (HITs) should be simple and unambiguous

Poor design of either can:

1. Impact labeler productivity

2. Introduce bias

Amazon Mechanical Turk
^^^^^^^^^^^^^^^^^^^^^^

Obtain human intelligence on demand. Access a global, on-demand, 24x7 workforce. Pay only for what you use. Use for labeling.

Managing labelers: 

* Motivation

* Plurality: Assign each HIT to multiple labelers to identify difficult or ambiguous cases or problematic labelers (lazy, confused, biased, etc.)

* Gold standard HITs: Hits with known labels mixed in to identify problematic labelers.

* Auditors: experts that adjudicate labeler disagreements and/or sample results for quality

* Labeler incentives: compensation, rewards, voluntary, gamification

* Quality and productivity metrics: can help detect problems with labelers.

Sampling and Treatment assigment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Image: treatment.png

2.3 Learning about the data
===========================

Exploratory data analysis: Important to understand data as much as possible. Informs subsequent steps in the ML process

I spend time to become familiar with the data itself in order to highlight gaps by identifying datasets that may be useful but have not been identified till now. 

Data schema
-----------

View structure of the dataset.

Image: schema.png

Types: categorical, ordinal, numeral, date, vector, text, image, unstructured, etc.

Use pandas DataFrame merge/join to join two datasets

Image: join.png

Data statistics
---------------

Descriptive statistics
^^^^^^^^^^^^^^^^^^^^^^

Overall statistics

* Number of instances (i.e. number of rows)

* Number of attributes (i.e. number of columns)

Attribute statistics (univariate)

* Statistics for numeric attributes (mean, variance, etc.) -- df. describe()

* Statistics for categorical attributes (histogram, mode, most/least frequent values, percentage, number of unique values, etc.) 

  * Histogram of values: E.g. df[<attribute>].value_counts() or seaborn's displot()

* Target statistics

  * Class distribution: E.g. df[<target>].value_counts() or np.bincount(y). You have some idea if data is balanced or not

Multivariate statistics

  * Correlations

  * Contingency Tables / Cross Tabulation

Image: cancer1.png, cancer2.png, cancer3.png, cancer4.png

Correlations
^^^^^^^^^^^^
Scatterplot matrices visualize attribute-target and attribute-attribute pairwise relationships.

Correlation matrices measure the linear dependence between features, can be visualized with heatmaps.

Correlation matrix heatmap

Image:heatmap1.png, heatmap2.png

**Formulas for correlations**

Pearson Correlation:

.. math::

    \rho_{xy} = \frac{\sum_{i=1}^N (x_i - \mu_x) (y_i - \mu_y)}{\sqrt{\sum_{i=1}^N (x_i - \mu_x)^2 \sqrt{\sum_{i=1}^N (y_i - \mu_y)^2 

Variance:

.. math::

    \sigma_x^2 = \frac{1}{n} \sum_{i=1}^n (x_i - \mu_x)^2

Covariance between (x,y):

.. math::

    \sigma_{xy} = \frac{1}{N} \sum_{i=1}^N (x_i - \mu_x)(y_i - \mu_y)

Correlation between (x,y):

.. math::

    \rho_{xy} = \frac{\sigma{xy}}{\sigma_x \sigma_y}

2.4 Data conditioning
=====================

Another important subphase is data conditioning: cleaning data, normalize the datasets abd perform transformations on the data. Part of this data conditioning subphase involves deciding which aspects of particular datasets will be useful to analyze in later steps. Additional questions and considerations for this subphase include the following:

* What are the data sources? What are the target fields (for example, columns of the tables)?

* How clean is the data?

* How consistent are the contents and files? Determine to what degree the data contains missing or inconsistent values and if the data contains values deviating from normal?

* Assess the consistency of the data types. For instance, if certain data is expected to be numeric, confirm it is numeric of if it is mixture of alphanumeric strings and text.

* Review the contents of data columns or other inputs, and check to ensure that make sense. For instance, if the problem involves analyzing income levels, preview the data to confirm that the income values are positive or if it is acceptable to have zeros or negative values.

* Look for any evidence of systematic error. Check for invalid, incorrect, or missing data values. Review the data to gauge if the definition of the data is the same over all measurements.

Data Issues:

* Messy data: Missing data -> imputing

Image: messy.png

* Noisy data: Outliers

* Biased data: Occurs in survey

* Imbalanced data

Image: imbalanced.png

* Correlated data: Highly correlated features can cause collinearity problems and numerical instability.


2.5 Survey and Visualize
========================

Leverage data visualization tools to gain an overview of the data. Seeing high-level patterns in the data enables one to understand characteristics about the data very quickly such as data quality (presence of unexpected values or other indicators of dirty data), skewness (majority of the data is heavily shifted toward one value or end of a continuum). It enables the user to find areas of interest, zoom and filter to find more detailed information about a particular area of the data, and then find the detailed data behind a particular area. I will follow these guidelines and considerations:

* Review the data to ensure that calculations remained consistent within columns or across tables for a given data field. For instance, did customer lifetime value change at some point in the middle of dataset?

* Does the data distribution stay consistent over all the data? If not, what kinds of actions should be taken to address this problem?

* Assess the granularity of the data, the range of values, and the level of aggregation of the data.

* Does the data represent the population of interest? For instance, if problem is focused on targeting customers of child-rearing age, does the data represent that, or is it full of senior citizens and teenagers?

* For time-related variables, are the measurements daily, weekly, monthly? Determine the level of granularity of the data needed for the analysis, and assess whether the current level of timestamps on the data meets that need.

* Is the data standarized/normalized? Are the scales consistent? 

* For geospatial datasets, are state or country abbreviations consistent across the data? Are personal names normalized? English or metric units? 

I can move to next phase when I have enough good quality data to start building the model.

***********************
Phase 3: Model Planning
***********************

In this phase, I identify the candidate models to apply to the data for clustering, classifying, or finding relationships in the data depending on the goal of the problem. Some of the activities to consider in this phase include the following:

* Asses the structure of the datasets, which is one factor that dictates the tools and analytical techniques for the next phase.

* Ensure that the analytical techniques enable to meet the business objectives and accept or reject the working hypotheses.

* Determine if the business situation warrants a single model or a series of techniques as part if a larger analytic workflow.

In addition to the considerations just listed, I research and understand how other analysts have approached the same kind of business situations.

This phase consists of the following subphases:

3.1: Data Exploration and Variable Selection
============================================

I perform a data exploration to understand the relationships among the variables to inform selection of the variables and methods and to understand the business situation. The key to this approach is to aim for capturing the most essential predictors and variables rather than considering every possible variable. 

In regression analyses, it is necessary to create variables that determine outcomes but demonstrate a strong relationship to outcome rather than to other input variables. This includes remaining vigilant for problems, sucha as serial correlation, multicolinearity, and other typical data modeling challenges that interfere with the validity of these models.

You need to designate the independent variables (predictors) and dependent variables (responses) prior to applying your modeling algorithms. 

3.2: Model Selection
====================

I choose an analytical technique or a short list of candidate techniques, based on each of the end goal of the business problem.

I can move to next phase when I have a good idea about the type of model to try.

***********************
Phase 4: Model Building
***********************

In this phase, I develop datasets for training, testing and production purposes. These datasets enable me to develop the analytical model and train it (training data), while holding aside some of the data (test data) for testing the model. The analytical model is developed and fit on the training data and evaluated (scored) against the test data. Questions to consider include these:

* Does the model appear valid and accurate on the test data?

* Does it appear as if the model is giving answers that make sense in this context?

* Analize false positives and false negatives in classification problems.

Once I can evaluate if the model is sufficiently robust to solve the problem, I can move to the next phase which is communicating the results.   