---
id: 979
title: "Big Data 101 with Apache Spark and Python"
date: '2022-01-21T13:01:24+11:00'
author: 'Suvansh Vaid'
layout: post
guid: 'https://azuretar.com/?p=979'
permalink: /big-data-101-with-apache-spark-and-python/
categories:
    - '- Blogs In English'
    - Data
tags:
    - data
---

---

Hi there, this is my first blog at azuretar and I’m pretty excited to share my knowledge of big data analytics using python and spark, with all of you. Hope this lesson can help people get started with big data. Happy reading.

### **Introduction to Big Data**

Big Data is one of the biggest buzzwords that you should have heard of by now and if you haven’t, you are at the right place. You can find plenty of fancy definitions of Big data on the internet, however, I like this one from Wikipedia.

> ‘Big data usually includes data sets with sizes beyond the ability of commonly used software tools to capture, curate, manage, and process data within a tolerable elapsed time’

Big Data is changing the world for better and to know how, I would recommend you to go through this [article](https://builtin.com/big-data/big-data-examples-applications). While it is easy to talk about Big Data and it’s applications, it’s equally harder to get to know how to effecitvely manage Big Data. In this article, I would try my best to cover all important Big Data concepts and demonstrate how we can use **Apache Spark** for big data processing.

First of all, let us see the 5 main **V’s** that characterize Big Data (p.s. there are many other V’s that you could hunt for!).

<figure class="wp-block-image">![](https://cdn-images-1.medium.com/max/1600/1*HZnK9Wy1imKVQ-QoarmfkA.png)<figcaption>Image Source: <https://searchcloudcomputing.techtarget.com/tip/Cost-implications-of-the-5-Vs-of-big-data></figcaption></figure>---

### Apache Spark

Now that we have a general idea about the V’s that characterize the big data, let’s see how Apache Spark provides a big data processing framework and helps us deal with the above ‘V’s. But first, what is Apache Spark?

**Apache Spark** is a fast and general engine for large-scale data processing designed to write applications quickly in Java, Scala, or Python. There are numerous applications of Spark such as streaming data manipulation (**Spark streaming**), machine learning (**Spark MLlib**), and batch processing (**Hadoop integration**).

One of Apache Spark’s appeals to developers has been its easy-to-use APIs (**RDD** and **DataFrames**), for operating on large datasets.

#### Resilient Distributed Dataset (RDD)

RDD was the primary user-facing API in Spark since its inception. It is an immutable distributed collection of elements of your data, partitioned across nodes in your cluster that can be operated in parallel with a low-level API that offers ***transformations*** and ***actions***.

*Transformations* are operations on RDDs that return a new RDD, such as *map()* and *filter()*.

*Actions, on the other hand,* are operations that return a result to the driver program or write it to storage and kick off a computation, such as *count()* and *first()*.

#### DataFrames

Like an RDD, a DataFrame is also an immutable distributed collection of data. However, unlike an RDD, data is organized into named columns, like a table in a relational database. DataFrames are designed to make large data set processing even easier and allow developers to impose a structure onto a distributed collection of data, allowing higher-level abstraction. It also makes Spark accessible to a wider audience, beyond specialized data engineers.

#### Which one to use: RDDs or DataFrames ?

While RDD offers you low-level functionality and control, DataFrame allows custom view and structure, offers high-level and domain-specific operations, saves space, and executes at superior speeds. So choose your API wisely! To know more about the differences between RDDs and DataFrames, you can check out this [blog](https://databricks.com/blog/2016/07/14/a-tale-of-three-apache-spark-apis-rdds-dataframes-and-datasets.html).

---

### Time to get your hands dirty!

Let’s dive into some code to see how you can set up Spark on your own machine. First things first, you need to make sure you have **Java** and **pyspark** installed on your machine. This [tutorial](https://www.datacamp.com/community/tutorials/installation-of-pyspark) shows you how to do that. Once you are done with this, the next step (which is not mandatory but I certainly recommend) is to install **Jupyter** **notebook** for python (follow this [link](https://test-jupyter.readthedocs.io/en/latest/install.html)). Okay, now you just need to open a jupyter notebook with Python 3 kernel and follow the steps below.

#### 1. Spark Configuration

To run a Spark application on the local/cluster, a few configurations and parameters need to be set, for this, ***SparkConf*** provides configurations to run a Spark application.

<figure class="wp-block-image">![](https://cdn-images-1.medium.com/max/1600/1*LfFvTS_ppXJe2A6FL-pv2g.png)<figcaption>Setting up configuration parameters for Spark</figcaption></figure>#### 2. SparkContext and SparkSession

Using *pyspark*, we can initialise Spark, create RDD from the data, sort, filter, and sample the data. Especially, we will use and import ***SparkContext*** from *pyspark*, which is the main entry point for Spark Core functionality. The ***SparkSession*** object provides methods used to create DataFrames from various input sources. There are two ways to create a SparkContext instance; one using *SparkContext* directly and the other using a *SparkSession* object. Below, I’ve shown both the ways (commented one of them) to do so.

<figure class="wp-block-image">![](https://cdn-images-1.medium.com/max/1600/1*IwsJX8qWBF6sk5PLuYxVgQ.png)<figcaption>Creating SparkContext instance</figcaption></figure>#### 3. Playing with RDDs

Now that we have set up SparkContext instance, we can play around with RDDs to see why they are effective in parallelizing data operations. Here, another thing to notice is that we instantiated SparkContext rather than using SparkSession because we will be playing with RDDs. In the upcoming section, we would use SparkSession when dealing with DataFrames.

There are many ways to parallelize data using RDDs, two of which I have shown below. One way is to use the ***parallelize*** function to convert an iterable such as set, list, tuple to an RDD.

<figure class="wp-block-image">![](https://cdn-images-1.medium.com/max/1600/1*nHW1xasymd6hc-kolMHrmQ.png)<figcaption>Creating RDD from an iterable (can be list/tuple/set)</figcaption></figure>Another way is to use the ***textFile*** function to read a text file and convert the contents to an RDD.

<figure class="wp-block-image">![](https://cdn-images-1.medium.com/max/1600/1*cC_t_3SFNi_bQUC59Toa8Q.png)</figure><figure class="wp-block-image">![](https://cdn-images-1.medium.com/max/1600/1*yhQ8uCwrH1DLB_E9czhtFw.png)<figcaption>Creating an RDD from a text file</figcaption></figure>For more on RDDs, I would recommend you this [exercise](https://datascience-enthusiast.com/Python/cs110_lab3a_word_count_rdd.html) to get a hands-on practice. This [cheatsheet](https://s3.amazonaws.com/assets.datacamp.com/blog_assets/PySpark_Cheat_Sheet_Python.pdf) on RDDs in Python would also help you in the long run (trust me).

#### **4. Playing with DataFrames**

To work with Data Frames in Spark, we need to instantiate the Spark Context using ***SparkSession***. So, in the above snippet where we created a SparkContext instance, we need to use **Method 1** instead of Method 2. Once we are done with that, we now have *SparkSessio*n up and running, which provides two methods for creating Data Frames, as shown below.

One way to create DataFrames is to use the method ***createDataFrame,*** *as shown below.*

<figure class="wp-block-image">![](https://cdn-images-1.medium.com/max/1600/1*qZI4lGEewrfiJTPVJd_Elg.png)<figcaption>Using `createDataFrame` to create a DataFrame</figcaption></figure>Another way to create a DataFrame is to use the ***read.csv*** method to load the data from csv to a DataFrame, as shown below.

<figure class="wp-block-image">![](https://cdn-images-1.medium.com/max/1600/1*nVpKtxriM6dmxYGcytPapQ.png)<figcaption>Creating a CSV file and reading it using `read.csv`</figcaption></figure>There are a lot of partitioning strategies used in pyspark to partition a DataFrame/RDD but I would skip that part because the important thing you need to know is that the default strategy used by pyspark is the most effecient one. Also, Spark has a special feature called **Catalyst Optimizer** which optimizes structural queries expressed in SQL, or via the DataFrame/Dataset APIs, which can reduce the runtime of programs and save costs.

Now, that we have a DataFrame to work on, we can make use of a large number of methods, such as columns, select, count, describe, filter, etc, which I would try to demonstrate through the following Machine Learning use case.

---

### Machine Learning in Spark using MLlib

As discussed earlier, **MLlib** is Apache Spark’s scalable machine learning library and it’s goal is to make practical machine learning scalable and easy. MLlib allows for preprocessing, munging, training of models, and making predictions at scale on data. In the following section, we are going to use Spark for Machine Learning on an **Adult Income** dataset taken from the UCI [repository](http://archive.ics.uci.edu/ml/datasets/Adult).

The following image shows a sample flow of the ML approach to be followed.

<figure class="wp-block-image">![](https://cdn-images-1.medium.com/max/1600/1*J_2eUJQmyO65ENieNGBG2w.png)<figcaption>ML approach in MLlib for Adult Income Dataset</figcaption></figure>Leaving aside the first four stages in the above image, we are mainly interested in the pipeline API. MLlib standardizes APIs for machine learning algorithms to make it easier to combine multiple algorithms into a single **pipeline**, or workflow. Before we dive deep into pipelines, it is fair to discuss the components of a pipeline namely **Transformers** and **Estimators**. A Transformer is an abstraction that includes feature transformers and learned models whereas an Estimator abstracts the concept of a learning algorithm or any algorithm that fits or trains on data. In the pipeline shown above, StringIndexer, OneHotEncoder and VectorAssembler are transformers while the ML Algorithm is an estimator.

Now, in the classification task, after data preprocessing, we first declare the 4 stages of the pipeline and then plugin these stages into a pipeline API and create an ML model for Logistic Regression. You can find the code for this in the following [github repository](https://github.com/SuvanshVaid27/Big-Data/blob/main/Adult-Income%20classification/adult-income-classification.ipynb).

---

### Summary

This article discussed a high-level overview of Big Data and the power of Apache Spark in handling the big data. Some big data terminologies were also discussed with hands-on coding. Congrats on reading through this article and this is just the tip of the iceberg as you shouldn’t expect a term like **Big Data** to be covered in such a small article! There are many other things that I shall cover in the coming days such as Spark Streaming, Apache Kafka and many more, so stay tuned!

### References

1. <https://spark.apache.org/docs/latest/ml-pipeline.html#transformers>
2. <https://databricks.com/glossary/what-is-machine-learning-library>
3. [https://en.wikipedia.org/wiki/Big\_data](https://en.wikipedia.org/wiki/Big_data)
4. <https://searchcloudcomputing.techtarget.com/tip/Cost-implications-of-the-5-Vs-of-big-data>
5. <https://spark.apache.org/docs/0.9.1/python-programming-guide.html>

<div class="wp-block-image is-style-rounded"><figure class="aligncenter size-full is-resized">![](https://azuretar.com/wp-content/uploads/2022/01/headshot.jpg)<figcaption>Suvansh Vaid</figcaption></figure></div>- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M19.7,3H4.3C3.582,3,3,3.582,3,4.3v15.4C3,20.418,3.582,21,4.3,21h15.4c0.718,0,1.3-0.582,1.3-1.3V4.3 C21,3.582,20.418,3,19.7,3z M8.339,18.338H5.667v-8.59h2.672V18.338z M7.004,8.574c-0.857,0-1.549-0.694-1.549-1.548 c0-0.855,0.691-1.548,1.549-1.548c0.854,0,1.547,0.694,1.547,1.548C8.551,7.881,7.858,8.574,7.004,8.574z M18.339,18.338h-2.669 v-4.177c0-0.996-0.017-2.278-1.387-2.278c-1.389,0-1.601,1.086-1.601,2.206v4.249h-2.667v-8.59h2.559v1.174h0.037 c0.356-0.675,1.227-1.387,2.526-1.387c2.703,0,3.203,1.779,3.203,4.092V18.338z"></path></svg><span class="wp-block-social-link-label screen-reader-text">LinkedIn</span>](https://www.linkedin.com/in/suvanshvaid27/)
- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12,2C6.477,2,2,6.477,2,12c0,4.419,2.865,8.166,6.839,9.489c0.5,0.09,0.682-0.218,0.682-0.484 c0-0.236-0.009-0.866-0.014-1.699c-2.782,0.602-3.369-1.34-3.369-1.34c-0.455-1.157-1.11-1.465-1.11-1.465 c-0.909-0.62,0.069-0.608,0.069-0.608c1.004,0.071,1.532,1.03,1.532,1.03c0.891,1.529,2.341,1.089,2.91,0.833 c0.091-0.647,0.349-1.086,0.635-1.337c-2.22-0.251-4.555-1.111-4.555-4.943c0-1.091,0.39-1.984,1.03-2.682 C6.546,8.54,6.202,7.524,6.746,6.148c0,0,0.84-0.269,2.75,1.025C10.295,6.95,11.15,6.84,12,6.836 c0.85,0.004,1.705,0.114,2.504,0.336c1.909-1.294,2.748-1.025,2.748-1.025c0.546,1.376,0.202,2.394,0.1,2.646 c0.64,0.699,1.026,1.591,1.026,2.682c0,3.841-2.337,4.687-4.565,4.935c0.359,0.307,0.679,0.917,0.679,1.852 c0,1.335-0.012,2.415-0.012,2.741c0,0.269,0.18,0.579,0.688,0.481C19.138,20.161,22,16.416,22,12C22,6.477,17.523,2,12,2z"></path></svg><span class="wp-block-social-link-label screen-reader-text">GitHub</span>](https://github.com/SuvanshVaid27?tab=repositories)