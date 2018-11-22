---
layout: post
title: What is a good model?
date: 2018-11-21 12:27:20 -0500
img: good_model.png
tags: [machine learning model, evaluation metrics, good model]
---

# What is a good model?

In the last tutorial, I mentioned a lot about good models.   

<span style="font-size:1.2em;">***But what is a good model?***</span>

It depends. For different situations, we might have different answers. Here, I will show you how to decide if a model is good or not in three situations   

## 1. On data science competition platforms

If you compete on the data science competition platforms, like [Kaggle](www.kaggle.com), it's actually very straight forward. They usually will provide you the evaluation metrics for their competitions. Just follow their guidence, either reach a highest score or a lowest score, which depends on their evaluation metrics.

### Commonly used evaluation metrics

<span style="font-size:1.2em;">***What is evaluation metrics?***  </span>


**Evaluation metrics** for a machine learning model is the standard that is used to measure the performance of a model. For different types of models, there are different ways to tell if the performance is good or not. As you may know that supervised learning and unsupervised learning are two major machine learning tasks. For supervised learning, there are regression models to solve regression problems, like the sales of a store, and classification models to solve classification problems, like if an email is spam or not. In Table 1, I put together some of the evaluation metrics that are used in regression models, classification models, unsupervised models.


<center>Table 1. Evaluation metrics for different types of models</center>


|     Model types    |  Evaluation metrics   |
| :--------------------| :---------------------|
| Regression models  |RMSE, MAE, R square, adjusted R square|
| Classification models |accuracy, precision-recall, F1 score, ROC-AUC, log-loss|   
| Unsupervised models| rand index, mutual information|



I will not go into the details of these evaluation metrics. If you are interesed, you could always google each term. And here I'm going to provide you some of the blogs that I think that have very good explanation of some of these evaluation metrics:

**RMSE:**   
[Choosing the Right Metric for Evaluating Machine Learning Models — Part 1 by Alvira Swalin](https://medium.com/usf-msds/choosing-the-right-metric-for-machine-learning-models-part-1-a99d7d7414e4)   


**accuracy, precision-recall, F1 score:**    

[Accuracy, Precision, Recall or F1? by Koo Ping Shung](https://towardsdatascience.com/accuracy-precision-recall-or-f1-331fb37c5cb9)


**ROC-AUC:**   
[Let’s learn about AUC ROC Curve! by Jocelyn D'Souza](https://medium.com/greyatom/lets-learn-about-auc-roc-curve-4a94b4d88152)

## 2. Models built on your local machine

Usually, before you put your model in production, you will need to build, evaluate and fine-tune your models on your local machine. To decide if a model is good or not, you will need to choose the evaluation metrics by yourself. It's the same as you compete on data science platforms, no matter what evaluation metrics you choose, you will always want to reach the highest performance according to the metrics you use.

In this situation, choose a proper evaluation metrics is very import. For a evaluation metrics that not fit for your purpose and dataset will hurt what you want to reach using a machine learning model. For example, if you want to identify a rare disease using machine learning model. The data you have will be very imbalanced. There might be 999 cases of healthy individuals but only one individual is having the disease. If you use accuracy as your evaluation metrics. When you have 1000 samples, your model might predict everyone be healthy and the accuracy of your model is 99.9%. But you missed out the one that has the disease and will need treatment. So in this instance, you might want to choose recall as your evaluation metrics which gives you the Fasle Positive Rate (FPR). And you don't mind if it's a little high. Because it's better we don't miss diagnose anyone that has disease with no disease.   

Since it's complicated and important, I will open another post to talk about how to choose the evaluation metrics for your models.


## 3. Models used in production

However, to determine if a model is good in production is much more complicated than the two situations mentioned above. There are lots of factors that might influence the performance of your model in production:
1. The environment might be different from your local machine.
2. There might be a lot of error when your model is running in production.
3. Your model might be reacting too slow for real-time prediction.
4. Your model might be too complicated that it's not realistic to use in real life.


A very famous example of the last concern is the models developed by the "BellKor's Pragmatic Chaos" team for Netflix [1]. Although their models reached the best performance on Netflix's dataset, Netflix was not able to use their models in production because they are too complicated.   

That way, a model with best performance in local machine is actually not a good model in production.   

What is a good model in production?   

So to determine if a model is a good model in production, the following criteria can be used:
1. The model can adapt to the environment in production well.
2. The model is ablet to act fast if real-time prediction is needed.
3. The model can produce the highest performance that is allowed when meet the previous criteria.
4. The model can run smoothly without any error.

The concern here about those criteria is we are not able to quantify them using evaluation metrics like we mentioned above. A lot of times, you will have to judge based on your experiences.   

But anyway, I think the simplest way to identify if a model is a good model in production is if it's usefull. If you can use it in production and it's helpful for you to make decisions or for your customers to make decision, it's a good model. It might not be the model that has the best performance on your local machine, but it's the best model in production.

**NOTE:** Please let me know if you notice any mistakes, or if you have other opinions on this topic. My email is juanluo2008@gmail.com.

Thank you very much!

# References:
[1] https://en.wikipedia.org/wiki/Netflix_Prize
