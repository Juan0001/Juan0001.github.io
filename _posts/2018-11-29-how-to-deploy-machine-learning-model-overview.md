---
layout: post
title: How to deploy your machine learning models in production (1)?
date: 2018-11-29 12:27:20 -0500
img: launch_model.png
tags: [deploy model, python, R]
---
<h1><center> How to deploy your machine learning models in production (1)?</center></h1>
<h2><center>Overview</center></h2>

### Table of contents
- [How will the models been used?](#model_usage)   
    - [Be an application or part of an application](#application)   
    - [Be called as an API or web service](#API)    
- [Background of web service](#background)    
    - [SOAP (Simple Object Access Protocol) web services](#SOAP)   
    - [RESTful web services](#REST)   
- [Methods to build a web service](#methods)   
    - [Build web services from scratch by yourself](#scratch)   
    - [Use pre-built web service platforms](#pre-built)   
- [Examples of how to deploy your machine learning models in production](#example)   




Most of the time, when we talk about what the Data Scientists do for their job, the most you hear are data retrieval, data cleaning, data wrangling, data exploratory analysis, data visualization, model building, fine-tuning etc. However, the ultimate object of a Data Scientist's job is to deploy the models you built in production, so your company and your company's customers or clients can actually benefit from them.    

Here comes the question:    
<span style="color:red">**How to deploy your machine learning models in production?**</span>

Theoretically, this is the Software Engineer's job to help you deploy your models. For those who work in large companies like Google, or Apple, you will not have to worry about that, there are plenty of Software Engineers that do the job for you. For those work in smaller companies or startups, you might need to delpoy the models yourselves.       

## How will the models been used? <a name="model_usage"></a>
Before you start deploy your models, the first thing you will need to know is: How will the models been used? There are two main ways that your models can be use in production:
1. be an application or part of an application
2. be called as an API or web service.

### Be an application or part of an application <a name="application"></a>

A machine learning model can be as part of an application and be loaded within the application or be an application itself for end users to use directly.

In this instance, if the model is part of an applicaiton, it should be written in the same programming language as the whole application. And you will need to add all the dependencies that you need to build the model, like packages to preprocess the data, create features and build models, into setup/config files.     

Usually the models can be loaded very smoothly in this way and it works well on devices that don't have internet connection. However, if you are not using Python, there are a lot of limitation of what kind of models you will be able to use. For example, there's no good way for Java to load PyTorch or Caffe. If you decide to develop your own package, it will be complicated and time-consuming. Moreover, the usage of the models are limited in the application you built and the scalibility is poor.    

Because of the limitations I mentioned above, it's not that common to deploy models as an application or part of an application.

### Be called as an API or web service <a name="API"></a>

The other way to use the models is to build an API or web service, then you can call the API or web service from your application. This method is the most used way to deploy machine leanring models in production. It overcomes the limitations mentioned above. You don't have to use the same programming language to train your model and build your application. Applications built in all programming languages can call the model API to predict their data. And by calling the API or web service, one model can be loaded into multiple applications which make the best use of the model.   

I will show you several ways we can use to build an model API or web service in the next section.




## Background of web service <a name="background"></a>
As a Data Scientist, you might have been using APIs from Twitter, Facebook or lot of other social media platforms to retrieve data for a long time. However, you might never checked what does API mean. API stands for Application Programming Interface, which based on wikipedia<sup>[1](https://en.wikipedia.org/wiki/Application_programming_interface)</sup> is "is a set of subroutine definitions, communication protocols, and tools for building software or in general terms, it is a set of clearly defined methods of communication among various components.". There are different uses for API. The APIs we used to retrieve data from Twitter is called Web API. Web API<sup>[2](https://en.wikipedia.org/wiki/Web_API)</sup> also known as web service is an application programming interface for either a web server or a web browser, with the most common use case being data retrieval. In the following post, I will mainly use the term **web services** to describe the Web API.    

There are two main types of web services<sup>[3](https://www.guru99.com/web-service-architecture.html#7)</sup>:
1. SOAP web services
2. RESTful web services   

### SOAP (Simple Object Access Protocol) web services <a name="SOAP"></a>
SOAP<sup>[4](https://en.wikipedia.org/wiki/SOAP)</sup> is a standards-based Web services access protocol that was developed by Microsoft, which relies exclusively on XML to provide messaging services.   

Sometimes developers found SOAP cumbersome and hard to use. For example, working with SOAP in JavaScript means writing a ton of code to perform extremely simple tasks because you must create the required XML structure absolutely every time. REST provides a lighter weight alternative.     

### RESTful web services <a name="REST"></a>
REST<sup>[5](https://en.wikipedia.org/wiki/Representational_state_transfer)</sup> stands for REpresentational State Transfer which is used to build Web services that are lightweight, maintainable, and scalable in nature. A service built on the REST architecture is called a RESTful service. The underlying protocol for REST is HTTP - the basic web protocol. REST can use four different HTTP 1.1 verbs (GET, POST, PUT, and DELETE) to perform tasks. While SOAP only allows XML, REST allows different messaging formats, such as HTML, JSON, XML, and plain text.   

In nowadays, most of the public web services are RESTful web services that transfer data in the compact and easy-to-use JSON data-interchange format.    

**Hense, RESTful web service is very good choice to deploy machine learning models.**

## Methods to build a web service <a name="methods"></a>
You can create your own web service from scratch or use a pre-built web service platform to deploy the machine learning models.
### Build web services from scratch by yourself <a name="scratch"></a>
For different programming languages, there are different packages that you can use to build a web service. As R and Python are the two main programming languages used by Data Scientist, I will only introduce the packages in these two languanges that can be used to build web services. To give you a general idea of what these packages can do, I simply copied the descriptions from their websites.    

#### R packages for building web servicess:
- [OpenCPU](https://www.opencpu.org/):    
  OpenCPU is a system for embedded scientific computing and reproducible research. The OpenCPU server provides a reliable and interoperable HTTP API for data analysis based on R. It’s designed to allow seamless integration between JavaScript and R. Web services must be written as R packages.  

- [plumber](https://www.rplumber.io/):   
  Plumber an R package that decorates your ordinary R functions with special comments to expose them as REST web service calls.   
- [jug](https://cran.r-project.org/web/packages/jug/index.html):  
  Jug is a small web development framework for R which relies heavily upon the httpuv package. It’s main focus is to make building APIs for your code as easy as possible. It is not supposed to be either an especially performant nor an uber stable web framework. Other tools (and languages) might be more suited for that. It’s main focus is to easily allow you to create APIs for your R code. However, the flexibility of Jug means that, in theory, you could built an extensive web framework with it.    


#### Phthon packages for building web services:
- [Flask](http://flask.pocoo.org/):      
  Flask is a lightweight WSGI web application framework. It is designed to make getting started quick and easy, with the ability to scale up to complex applications. It makes the process of designing a web application simpler.    

- [Django](https://www.djangoproject.com/):   
  Django is a high-level Python Web framework that encourages rapid development and clean pragmatic design. Django’s primary goal is to ease the creation of complex database-driven websites.



### Use pre-built web service platforms <a name="pre-built"></a>
If you are not familiar with web service, don't worry, there are also pre-built web service platform that you can use to deploy you model. Most of the platforms are cloud-based and provide interface for different programming languages. The most famous examples of the pre-built web service platforms are:
- [Google's CLOUD MACHINE LEARNING ENGINE](https://cloud.google.com/ml-engine/):    
  Google Cloud Machine Learning (ML) Engine is a managed service that enables developers and data scientists to build and bring superior machine learning models to production. Cloud ML Engine offers training and prediction services, which can be used together or individually.  
- [Microsoft Azure](https://azure.microsoft.com/en-us/):   
  Microsoft Azure is a cloud computing service created by Microsoft for building, testing, deploying, and managing applications and services through a global network of Microsoft-managed data centers.
- [Amazon Machine Learning](https://aws.amazon.com/aml/):   
  Amazon Machine Learning is a managed service for building ML models and generating predictions, enabling the development of robust, scalable smart applications.
- [Oracle's GraphPipe](https://oracle.github.io/graphpipe/#/):   
  GraphPipe is a protocol and collection of software designed to simplify machine learning model deployment and decouple it from framework-specific model implementations.

## Examples of how to deploy your machine learning models in production <a name="example"></a>
I will put out several examples of how to deploy your machine learning models in production in the next sections.

**NOTE**: Please let me know if you have any questions, spot any mistakes or if you have other opinions. My email is juanluo2008@gmail.com. Thank you very much!
