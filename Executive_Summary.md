# Project 3: Web APIs & NLP & Classification

#### Goal: 
1. Using [Pushshift's](https://github.com/pushshift/api) API,  collect posts from two subreddits of your choosing.
2. Use NLP to train a classifier on which subreddit a given post came from. This is a binary classification problem.


### Contents

1. Problem Statement
2. Overview
3. Data Gathering
4. NLP Methodology
5. Classification Models and Predictions
6. Executive Summary


### 1. Problem Statement

A startup gaming company interested to learn how the current posts can be merged with reddit community to improve marketing on their new upcoming game. Any post or comment posted need to be targeted properly into the channel category.


### 2. Overview

Reddit is a home to 100K+ communities, with 52M+ daily active users and 50B+ monthly views (updated Jan 2020) and provide human connections to converation, posts, comments on variety of interests. Some of the interests I observed are in breaking news, sports, TV fan theories, gaming, products for skin etc. and much more.

We will leverage Reddit posts on Gaming community posts to understand interests, likes and dislikes on features and create a model to predict based on user posts using NLP methodologies. 

To determine some of the features and interests on how users use the gaming apps, products and tools - we will use 3 different sub-reddit categories - boardgames, Fallout and RockerLeagues games to build a model with the user posts and predict the sub-reddit category using NLP and Machine Language models. Ensure the models have good accuracy and precision scores to present to the executive leadership.

### 3. Data Gathering

Followed the process below to perform the data gathering:
1. Pushshift API provides reddit posts from their submissions and comments area. There is lot of information within the reddit submissions. We will use 3 categories from gaming section of submissions.
2. Tested the API to pull first 100 posts and title and created a model to understand the underlying data on the submissions.
3. Created a function to gather more data in the size of 100 rows each for every sub reddit, introduced a timer in between the calls to ensure the API does not get overloaded.
4. Brought in 3 different categories - boardgames, Fallout, and RocketLeague totalling to 4500 rows.
5. Added 4th category to see if the model performs any better or breaks. But not going to use for final modeling.
6. Concatenate all the dataframes capturing selftext, title and subreddit as our features needed. We will be using only selftext and title for our models classification.

### 4. NLP 

Here we focus on looking at the content our data gathered, perform EDA and NLP steps.

1. At a glance look for null data, Only found nulls in self text but not in title.
2. Checked the value counts for target value - subreddit showed near balanced classification.
**Fallout         0.355556**
**RocketLeague    0.333333**
**boardgames      0.311111**
3. Total dataset was 4500 rows
4. For all nulls in selftext - added a stop word "do" since it will be removed as part of our NLP processing, so that we can merge the self text and title data to combine and get the completed submission_text
5. We now have submission_text and subreddit to work with
6. While exploring data in submission_text, figured the data needs to be cleaned for urls, special punctuations, [removed] etc. Created a function to tokenize and bring words and lemmatize the words in the submission_text.
7. Now we have clean words that can be used for NLP vectorizers and classification models. Save that to csv - datasets/redditready.csv

### 5. Classification Models and Predictions

** The 2 models used in our classification problem are: **

1. Naive Bayes - Multinomial Classifier
   
   ** I have used MultinomialNB as it works well with positive integers and great aat predicting multi classification problems. As I chose 3 classifier's in the dataset, MultinomialNB with CountVectorizer using GridSearchCV and hyperparameter tuning with Pipelines.
   The best parameters used:
    - max_df = 0.85
    - max_features = 4000
    - min_df = 2
    - ngram_range = (1, 1)
    
    The classification report generated from Multinomial NB is as follows:
    
    ![Screenshot](./assets/precisionMNB.png)
    
    
2. SVM - Support Vecotor Classifier
  
  ** SVC is from Support Vector Machines algorith provides regularization as part of the hyper parameter tuning. Used kernel and C to tune the model and get the best parameters to work with. Used GridSearchCV with the Pipelines.
  The best parameters used:
    - C value = 0.4737368421052632
    - kernel = linear
    - degree = 2
    - gamma = scale
    
    The classification report generated from Multinomial NB is as follows:
    
    ![Screenshot](./assets/precisionSVM.png)
    
3. Random Forest Classifier

### 6. Executive Summary

Reddit community posts contains a lot of useful data that can help predicting on the subreddit based on the post information. Created models on the NLP 

**Data Collection**
- Was enough data gathered to generate a significant result?
- Was data collected that was useful and relevant to the project?
- Was data collection and storage optimized through custom functions, pipelines, and/or automation?
- Was thought given to the server receiving the requests such as considering number of requests per second?

**Data Cleaning and EDA**
- Are missing values imputed/handled appropriately?
- Are distributions examined and described?
- Are outliers identified and addressed?
- Are appropriate summary statistics provided?
- Are steps taken during data cleaning and EDA framed appropriately?
- Does the student address whether or not they are likely to be able to answer their problem statement with the provided data given what they've discovered during EDA?

**Preprocessing and Modeling**
- Is text data successfully converted to a matrix representation?
- Are methods such as stop words, stemming, and lemmatization explored?
- Does the student properly split and/or sample the data for validation/training purposes?
- Does the student test and evaluate a variety of models to identify a production algorithm (**AT MINIMUM:** two classification models, **BONUS:** try a Naive Bayes)?
- Does the student defend their choice of production model relevant to the data at hand and the problem?
- Does the student explain how the model works and evaluate its performance successes/downfalls?

**Evaluation and Conceptual Understanding**
- Does the student accurately identify and explain the baseline score?
- Does the student select and use metrics relevant to the problem objective?
- Does the student interpret the results of their model for purposes of inference?
- Is domain knowledge demonstrated when interpreting results?
- Does the student provide appropriate interpretation with regards to descriptive and inferential statistics?

**Conclusion and Recommendations**
- Does the student provide appropriate context to connect individual steps back to the overall project?
- Is it clear how the final recommendations were reached?
- Are the conclusions/recommendations clearly stated?
- Does the conclusion answer the original problem statement?
- Does the student address how findings of this research can be applied for the benefit of stakeholders?
- Are future steps to move the project forward identified?




