# GUESS MY WEIGHT 

![guess_your_weight.gif](images/guess_your_weight.gif)

## Table of Contents TOC
[Overview](#overview)<br />
[Google Colab Instructions](#instructions-for-google-colab)<br />
[Business Case](#business-case)<br />
[Data Understanding](#data-understanding)<br />
[Data Preparation](#data-preparation)<br />
[Modeling](#modeling)<br />
[Evaluation](#evaluation)<br />
[Github Repository and Resources](#github-repository-and-resources)<br />
[Google Colab](https://colab.research.google.com/github/bennettandrewm/guess_my_weight/blob/master/guess_my_weight_notebook-6-8.ipynb)<br />


## Overview
Health and Wellness is a $142 billion dollar industry designed to help people managed their weight. To aid this goal, our model works as a feature to guide users tracking lifestyle data (diet, exercise, sleep) with recommendations to target weight loss.  A machine learning Decision Tree algorithm analyzed lifestyle data with emphasis on precision and accuracy metrics. The model determined a Carbohydrate threshold, or Carb Number, which corresponded to weight loss or gain at the next day's morning weigh-in. At under 221g (for this user) nearly 74 percent of the weigh-ins the following day showed a loss. This increased to nearly 82% when acheiving a minimum fiber intake around 14.5 grams, in addition to being under the Carbohydrate threshold. Conversely, at over 221g, nearly 66 percent of the  weigh-ins the following day showed a gain. This increased to 79 percent when less than 6.9hrs of sleep was recorded in addition to going over the carb threshold. Based on these findings, it's recommended that these analytics continue to be developed to prompt/guide users through out the day to course correct on encourage certain habits. <br />
[return to TOC](#table-of-contents-TOC)

## Instructions for Google Colab
To run this notebook, you'll need a Kaggle log-in and web access to Google Colab. Google Colab is a free, user-friendly platform to run software, specifically data models. Kaggle is a website popular with data industry that hosts databases and runs data analytics competition. To access the database for this model, you will need to create a Kaggle account and follow the instructions to download your 'token' and 'key'. This model will prompt you to have that information. <br /> 
[return to TOC](#table-of-contents-TOC)

## Business Case
According to a CDC study, the obesity prevalence rate in the US was 42 percent in 2020. The Health and Wellness industry has a plethora of systems, apps, and protocols to address this, yet it's still a problem. On a human level, we all know that managing our weight is both critical to health and happiness but also incredible challenging. The average person has dieted over 6 times in their life, according to a survey by the Mayo Clinic. There's a demand among users as well as a basic human instict to feel in control of our health. Creating additional, more intuitive tools to manage weight loss will serve this need.

In this model, we focus on small, short term goals to determine if daily diet, exercise, and sleep goals can impact your weigh-in the next day. To simplify this task, we'll utilize binary prediction, either weight loss or weight gain, to determine if the sum of these daily habits to determine how they predicted this binary outcome. For instance, let's say you weigh 180 lbs on Monday morning. If you weigh 181 lbs on Tuesday morning, that's conisdered one weight gain day.<br />
[return to TOC](#table-of-contents-TOC)

## Data Understanding
The data source for this analysis is my personal health information. Over the course of 6 months, I lost approximately 20 lbs. Tracking my calories and logging my weight was a big part of it, as was passsive data captured from my devices (Iphone, Apple Watch) including sleep and metabolism data. You can see the data the weight tracked below over time.

![daily_weigh_in.png](images/daily_weigh_in.png)

Prior to Kaggle upload, the data from the phone was condensed into daily sums. The totals (exercise, sleep, diet) from the day were used as the feature data for prediction <br />
[return to TOC](#table-of-contents-TOC)

## Data Preparation
The model aims to predict whether a user will lose weight the next day. This difference in weight was used to verify stationality to ensure there was no correlation with time (beyond the previous day). This difference from day to day was used to classify weight loss vs weight gain. To understand the data in terms of weight loss/gain days, see the below graph.

![weight_days.png](images/weight_days.png)<br />

Prior to modeling, there were concerns regarding correlation. PCA and Correlations were studied. Due to these concerns over correlation and high variance among the variables, the feature data we divided into segments based on a data heirarchy. A schematic can be seen below.

![data_hierarchy.png](images/data_heirarchy.png)<br />

[return to TOC](#table-of-contents-TOC)

## Modeling
In order to select the best model, we surveyed a variety of traditional algorithms and use different feature segments (level 1, level 2, and level 3). KNN, Logistic Regression, Decision Tree, Naive Bayes, SVM, and Neural Network models were scored in a table using evaluation metrics. Of all of the metrics, precision was given the highest preference, second was accuracy. Because we want to predict weight loss, we have a strong emphasis on getting True Positives correct! We want to provide the best recommendations for users to lose weight, first and foremost. Accuracy is secondary metric, but still important, because we are interested in True Negatives, namely, predicting weight gain accurately as well. We care less about False Negatives and False Positives. See results below sorted for Precision, as well as Accuracy.

![precision_table.png](images/precision_table.png)<br />

![accuracy_table.png](images/accuracy_table.png)<br />

Based on these results, a Decision Tree model score the highest in these tables.<br />
[return to TOC](#table-of-contents-TOC)

## Evaluation
Once the Decision Tree model was selected, fine tuning and evaluation of this model occured. The Decision Tree models from our survey scored 80% and 78% precision, respectively. Upon inspection of the model, it was clear that feature_2, expressing the Total Carbohydrates consumed, was the strongest indicator of any single variable. To reflect this, the model was fine tuned, combining elements from feature_2 and feature_3 segments, with Total Carbohydrates always providing the first split. This tuning yielded key findings in the section shown below, while sacrificing some Precision on the test data (75% from 80%). Because the test data was small, this was a difference of one prediction, which was minor to the impact of key findings. The confusion matrix for the model's test results are shown below.<br />

![confusion_matrix.png](images/confusion_matrix.png)<br />

[return to TOC](#table-of-contents-TOC)

## Key Findings
From the model emerged three key findings:

#### 1. Carbs
The strongest indicator in the model for potential weight loss was Total Carbohydrates. When under the carbohydrate threshold (223 g) the user experienced weight-loss on 74% of their next day weigh-ins. Vice-Versa, when the user was over the threshold (223g), 67% of the next day weigh-ins showed a gain.

![rec1_pic1.png](images/rec1_pic1.png)<br />
![rec1_pic2.png](images/rec1_pic2.png)<br />

#### 2. Lack of Sleep
Lack of sleep may contribute to weight gain as well. In instances when the user was over the carbohydrate threshold, and slept less than 6.9hrs, almost 80% of the weigh-ins showed a gain. That's a 12% increase.

![rec2.png](images/rec_2.png)<br />

#### 3. Fiber
Having a minimum intake of Fiber could help with weight loss. In instances when the user was under the carbohydrate threshold, and consumed more than 15.75 grams of Fiber, almost 82% of their next day weigh-ins showed a loss. That's an 8% increase over just the carbs.

![rec3.png](images/rec_3.png)<br />

##  Summary
To aid in the struggle to lose weight, this model was able to analyze data and create 3 key finding that could be used to help people reach their goals. Through lifestyle analytics, a user can track their eating over the case of the day and receive notifications about how to course correct. The model utilized a database from apps and devices that the user is already using. <br />
[return to TOC](#table-of-contents-TOC)

## Github Repository and Resources
To execute this project, a github repository is utilized for public viewing and collaboration

You can see the following files stored in the github repository.

Images - Folder containing the image files used in the Notebook, Presentation, and README file
pre-kaggle - contains originally brainstorm notebook
- brainstorm.ipynb

.gitignore - git ignore file

README.md the currently file you're reading with descriptions about the coding file

guess_my_weight-6-8.ipynb - Notebook with Python analysis


[return to TOC](#table-of-contents-TOC)

