# Guess My Weight

<p align="center">
<img src="images/guess_your_weight.gif" width="400" height="400" />
</p>

## Table of Contents TOC
[Overview](#overview)<br />
[Google Colab Instruction](#google-colab-instructions)<br />
[Business Case](#business-case)<br />
[Data Understanding](#data-understanding)<br />
[Data Preparation](#data-preparation)<br />
[Modeling](#modeling)<br />
[Evaluation](#evaluation)<br />
[Key Findings](#evaluation)<br />
[Summary](#summary)<br />
[Github Repository](#github-repository)<br />


## Overview
Health and Wellness is a $142 billion dollar industry designed to help people managed their weight. This
model is intended as a feature to guide users tracking lifestyle data (diet, exercise, sleep) with
recommendations to target weight loss. A machine learning Decision Tree algorithm analyzed captured lifestyle data and fine-tuned to consider precision and accuracy metrics. The model determined a Carbohydrate
threshold, or Carb Number, which corresponded to next day weight loss or gain. At under 221g (for this
user) nearly 74 percent of the next days weigh-in showed a loss. This increased to nearly 82% when
acheiving a minimum fiber intake around 14.5 grams as well. Conversely, at over 221g, nearly 66 percent of
the weigh-ins showed a gain. This increased to 79 percent when less than 6.9 hrs of sleep was recorded in
addition to the carb threshold. Based on these findings, it's recommended that these analytics be used to
prompt/guide users through out the day to course correct on encourage certain habits.
<br />[return to TOC](#table-of-contents-TOC)

## Google Colab Instructions
To run this notebook, you'll need a Kaggle log-in and web access to [Google Colab and link to this notebook](https://colab.research.google.com/github/bennettandrewm/guess_my_weight/blob/master/guess_my_weight_notebook-6-8.ipynb). Google Colab is a free, user-friendly platform to run software, specifically data models. Kaggle is a [website](https://www.kaggle.com/) popular with the data industry that hosts databases and runs data analytics competition. To access the [database](https://www.kaggle.com/datasets/andrewmbennett/guess-my-weight-4-25) for this model, you
will need to create a Kaggle account and follow the instructions to download your 'token' and 'key'. This
model will prompt you to have that information.
<br />[return to TOC](#table-of-contents-TOC)


## Business Case
According to a CDC study, the obesity prevalence rate in the US was 42 percent in 2020. The Health and
Wellness industry, valued at around $142 billion, has a plethora of systems, apps, and protocols to address
this, yet it's still a problem. On a human level, we all know that managing our weight is both critical to health
and happiness but also incredible challenging. The average person has dieted over 6 times in their life,
according to a survey by the Mayo Clinic. There's a demand among users as well as a basic human earn to
feel in control of our health. Creating additional, more intuitive tools to manage weight loss is a vast
importance.

In this model, we focus on a small short term goals to determine if daily diet, exercise, and sleep goals can
impact your weigh-in the next day. To simplify this task, we'll utilize binary prediction, either weight loss or
weight gain, to determine if the sum of these daily habits to determine how they predicted this binary
outcome.
<br />[return to TOC](#table-of-contents-TOC)

## Data Understanding
The data source for this analysis is my personal health information. That data was download from my smart device to a local setting, where it was pre-processed, formatted, and uploaded to [Kaggle](https://www.kaggle.com/datasets/andrewmbennett/guess-my-weight-4-25) to made available pubically. You can also find it in this github repository. Follow [instructions](#github-repository) below. 
<br />[return to TOC](#table-of-contents-TOC)

The data can be found in the following locations:

* [Kaggle](https://www.kaggle.com/datasets/andrewmbennett/guess-my-weight-4-25)
* [THis Repository](content/guess-my-weight-4-25/merge_health_4_25.csv)

Over the course of 6 months, I lost approximately 20 lbs. Tracking my calories and weight was a big part of it, as well data captured from my devices passively, such as workouts, heart rate, sleep, etc. You can see the weigh-in data here.

<p align="center">
<img src="images/daily_weigh_in.png"/>
</p>

## Data Preparation
The model aims to predict whether a loser lost weight. The wiegh-in data is used to establish whether the
user gained or lost weight from the previous day's weigh-in. This was achieved through differencing, and the
data was verified for stationality to ensure there was no correlation with time (beyond the previous day). To
understand the data in terms of weight gain days, see the below graph.
<br />[return to TOC](#table-of-contents-TOC)

<p align="center">
<img src="images/weight_days.png"/>
</p>

Prior to modeling, there were concerns regarding correlation. PCA and Correlations were study. Due to these
concerns, the feature data we divided into segments based on a data heirarchy. A schematic can be seen
below.

<p align="center">
<img src="images/data_heirarchy.png"/>
</p>

## Modeling
In order to select the best model, we surveyed a variety of traditional algorithms and use different feature
segments (level 1, level 2, and level 3). KNN, Logistic Regression, Decision Tree, Naive Bayes, SVM, and
Neural Network models were scored in a table using evaluation metrics. Of all of the metrics, precision was
given the highest preference, second was accuracy. Because we want to predict weight loss, we have a
strong emphasis on getting True Positives corret! We want to recommend to users with confidence to lose
weight. Accuracy is secondary but still matters, because we are interested in True Negatives, namely,
predicting weight gain accurately as well.
<br />[return to TOC](#table-of-contents-TOC)

<p align="center">
<img src="images/precision_table.png"/>
</p>

<p align="center">
<img src="images/precision_table.png"/>
</p>

Based on these results, a Decision Tree model was utilized.

## Evaluation
The Decision Tree from the modeling survey in the previous section scored 80% and 78% precision,
respectively. Upon inspection of the data, it was clear that feature_2, expressing the Total Carbohydrates
consumed, was the strongest indicator. To reflect this, the model was fine tuned, combining elements from
feature_2 and feature_3 segments. This tuning yielded key findings in the section shown below, while
sacrificing some Precision on the test data (75% from 80%). This was a difference of one prediction. The
confusion matrix for the model's test results are shown below.
<br />[return to TOC](#table-of-contents-TOC)

<p align="center">
<img src="images/confusion_matrix.png"/>
</p>

[return to TOC](#table-of-contents)

## Key Findings

#### Carbs

The strongest indicator in the model of potential weight loss. When under the carbohydrate threshold (223
g) the user experienced 74% of their weigh-ins the next day showed weight loss. Vice-Versa, when the user
was over the threshold (223g), 67% of the weigh-ins next day showed a gain.

<img src="images/rec1_pic1.png"/>

<img src="images/rec1_pic2.png"/>

#### Lack of Sleep

Lack of sleep may contribute to weight gain. In instances when the user was over the carbohydrate
threshold, and slept less than 6.9hrs, almost 80% of the weigh-ins showed a gain. That's a 12% increase.

<img src="images/rec_2.png"/>

#### Fiber

Fiber may assist in weight loss. In instances when the user was under the carbohydrate
threshold, but consumed at least 14.75g of Fiber, the occurence of weight loss increased to nearly 82% of the weigh-ins showed a gain. That's an 8% increase.

<img src="images/rec_3.png"/>

<br />[return to TOC](#table-of-contents-TOC)

## Summary
This model shows that with tracking the right data we can identify strong indicators towards managing weight. Targeting weight loss days turned out to be an effective way to apply machine learning to health data.


### Next Steps:
#### Additional Data
We need to continue to refine the model to boost performance. Typically, over 1000 observations are needed to have confidence in a model. We only had 195 observations, nearly 30% of which had gaps in weight data. With more data we can optimize the success we already have.

#### Test UI Prompts
Recommendations for course correction are only as effective as how the message is delivered. For carb tracking, perhaps the user could monitor their carb intake through the day and receive a notification when intake is high. With Fiber, the user could be pinged at the end of the day if their fiber intake is low. When carb intake increases, the user could be reminded to get enough sleep.

#### Try Calorie Counting
Increase awareness around calorie counting. It's hard at first but then it becomes second nature. It's very helpful to track what one eats.
<br />[return to TOC](#table-of-contents-TOC)

## Github Repository

To execute this project, a github repository is utilized for public viewing and collaboration. The source file for the original data is not available.

You can see the following files stored in the github repository.

* *content* <a id='data'></a> - Folder containg process personal health data files
    * [merge_health_4_25.csv](content/guess-my-weight-4-25/merge_health_4_25.csv)

* *Images* - Folder containing the image files used in the Notebook, Presentation, and README file

* *PDFs* - Folder containing the pdf versions of the Slides, the Notebook, and Presentation

* *pre_kaggle* - Folder containing previous revisions of different files
            
* [README](README.md) the currently file you're reading with descriptions about the coding file

* [.gitignore](.gitignore) - git ignore file 

* [guess_my_weight_notebook](guess_my_weight_notebook-6-8.ipynb) - Notebook with Python analysis

<br />[return to TOC](#table-of-contents-TOC)
