# Guess My Weight

<p align="center">
<img src="images/guess_your_weight.gif" width="400" height="400" />
</p>

[Table of Contents TOC]
[Overview](#overview)<br />
[Google Colab Instruction](#google-colab-instructions)<br />
[Business Case](#business-case)<br />
[Data Understanding](#data-understanding)<br />
[Data Preparation](#data-preparation)<br />
[Modeling](#modeling)<br />
[Evaluation](#evaluation)<br />
[Key Findings](#evaluation)br />
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
[return to TOC](#table-of-contents)

## Google Colab Instructions
To run this notebook, you'll need a Kaggle log-in and web access to [Google Colab and link to this notebook](https://colab.research.google.com/github/bennettandrewm/guess_my_weight/blob/master/guess_my_weight_notebook-6-8.ipynb). Google Colab is a free, user-friendly platform to run software, specifically data models. Kaggle is a [website](https://www.kaggle.com/) popular with the data industry that hosts databases and runs data analytics competition. To access the [database](https://www.kaggle.com/datasets/andrewmbennett/guess-my-weight-4-25) for this model, you
will need to create a Kaggle account and follow the instructions to download your 'token' and 'key'. This
model will prompt you to have that information.
[return to TOC](#table-of-contents)


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
[return to TOC](#table-of-contents)

## Data Understanding
The data source for this analysis is my personal health information. That data was download from my smart device to a local setting, where it was pre-processed, formatted, and uploaded to [Kaggle](https://www.kaggle.com/datasets/andrewmbennett/guess-my-weight-4-25) to made available pubically. You can also find it in this github repository. Follow [instructions](#github-repository) below. 

The data can be found in the following files:

* [Kaggle](https://www.kaggle.com/datasets/andrewmbennett/guess-my-weight-4-25)
* [merge_health_4_25.csv](content/guess-my-weight-4-25/merge_health_4_25.csv)

Over the course of 6 months, I lost approximately 20 lbs. Tracking my calories and weight was a big part of it, as well data captured from my devices passively, such as workouts, heart rate, sleep, etc. You can see the weigh-in data here.

<p align="center">
<img src="images/daily_weigh_in.png" width="400" height="400" />
</p>

[return to TOC](#table-of-contents)

## Data Preparation
The model aims to predict whether a loser lost weight. The wiegh-in data is used to establish whether the
user gained or lost weight from the previous day's weigh-in. This was achieved through differencing, and the
data was verified for stationality to ensure there was no correlation with time (beyond the previous day). To
understand the data in terms of weight gain days, see the below graph.
[return to TOC](#table-of-contents)

<p align="center">
<img src="images/weight_days.png" width="400" height="400" />
</p>

Prior to modeling, there were concerns regarding correlation. PCA and Correlations were study. Due to these
concerns, the feature data we divided into segments based on a data heirarchy. A schematic can be seen
below.

<p align="center">
<img src="images/data_heirarchy.png" width="400" height="400" />
</p>

## Modeling
In order to select the best model, we surveyed a variety of traditional algorithms and use different feature
segments (level 1, level 2, and level 3). KNN, Logistic Regression, Decision Tree, Naive Bayes, SVM, and
Neural Network models were scored in a table using evaluation metrics. Of all of the metrics, precision was
given the highest preference, second was accuracy. Because we want to predict weight loss, we have a
strong emphasis on getting True Positives corret! We want to recommend to users with confidence to lose
weight. Accuracy is secondary but still matters, because we are interested in True Negatives, namely,
predicting weight gain accurately as well.

<p align="center">
<img src="images/precision_table.png" width="400" height="400"/>
</p>

<p align="center">
<img src="images/precision_table.png" width="400" height="400"/>
</p>

Based on these results, a Decision Tree model was utilized.
return to TOC

[return to TOC](#table-of-contents)

## Evaluation
The Decision Tree from the modeling survey in the previous section scored 80% and 78% precision,
respectively. Upon inspection of the data, it was clear that feature_2, expressing the Total Carbohydrates
consumed, was the strongest indicator. To reflect this, the model was fine tuned, combining elements from
feature_2 and feature_3 segments. This tuning yielded key findings in the section shown below, while
sacrificing some Precision on the test data (75% from 80%). This was a difference of one prediction. The
confusion matrix for the model's test results are shown below.

<p align="center">
<img src="images/confusion_matrix.png" width="400" height="400"/>
</p>

[return to TOC](#table-of-contents)

## Key Findings

#### Carbs

The strongest indicator in the model of potential weight loss. When under the carbohydrate threshold (223
g) the user experienced 74% of their weigh-ins the next day showed weight loss. Vice-Versa, when the user
was over the threshold (223g), 67% of the weigh-ins next day showed a gain.

<img src="images/rec1_pic1.png" width="400" height="400"/>

<img src="images/rec1_pic2.png" width="400" height="400"/>

#### Lack of Sleep

Lack of sleep may contribute to weight gain. In instances when the user was over the carbohydrate
threshold, and slept less than 6.9hrs, almost 80% of the weigh-ins showed a gain. That's a 12% increase.

<img src="images/rec_2.png" width="400" height="400"/>

#### Fiber

Fiber may assist in weight loss. In instances when the user was under the carbohydrate
threshold, but consumed at least 14.75g of Fiber, the occurence of weight loss increased to nearly 82% of the weigh-ins showed a gain. That's an 8% increase.

<img src="images/rec_3.png" width="400" height="400"/>

#### [return to TOC](#table-of-contents)

## Summary
This model shows that with tracking the right data we can identify strong indicators towards managing weight. Targeting weight loss days turned out to be an effective way to apply machine learning to health data.


### Next Steps:
#### Additional Data
We need to continue to refine the model to boost performance. Typically, over 1000 observations are needed to have confidence in a model. We only had 195 observations, nearly 30% of which had gaps in weight data. With more data we can optimize the success we already have.

#### Test UI Prompts
Recommendations for course correction are only as effective as how the message is delivered. For carb tracking, perhaps the user could monitor their carb intake through the day and receive a notification when intake is high. With Fiber, the user could be pinged at the end of the day if their fiber intake is low. When carb intake increases, the user could be reminded to get enough sleep.

#### Try Calorie Counting
Increase awareness around calorie counting. It's hard at first but then it becomes second nature. It's very helpful to track what one eats.


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

#### [return to TOC](#table-of-contents)









## 4. Data Approach

### Overview
The program asks a user to rate five random movies from an existing database, and then returns five recommendations. It utilizes the [ratings.csv](data/ratings.csv) file from the [Movielens 100K ratings](#data) database containing movie ratings (0.5-5) on thousands of movies from hundreds of users. The program uses a collaborative filtering model - no content-based or hybrid filtering was performed. Specifically, it relies on the model's ability to predict how any user would rate any movie. The `surprise` module is well suited for explicit ratings system. With data on over 600 users and 9700 movies, collaborative filtering is an appropriate choice.

### Source Data 
This project uses the Movielens dataset from the [GroupLens](https://grouplens.org/datasets/movielens/) lab at the University of Minnesota, which can be found in in the [`data`](#data) folder in this GitHub repository. 

The website notes that "This dataset (ml-latest-small) describes 5-star rating and free-text tagging activity from MovieLens, a movie recommendation service. It contains 100836 ratings and 3683 tag applications across 9,742 movies. These data were created by 610 users between March 29, 1996 and September 24, 2018. This dataset was generated on September 26, 2018. Users were selected at random for inclusion. All selected users had rated at least 20 movies. No demographic information is included. Each user is represented by an id, and no other information is provided."



### Recommender Implentation

The approach can be summarized as follows:

* Step 1: Prior to input from the new user, we create a user-based collaborative filtering prediction model to predict how an existing user would rate a movie from the database. A few different models were attempted, but a model-based, single value decompisition method was selected.
* Step 2: Prompt user to rate five movies.
* Step 3: Add user's rating to the existing database.
* Step 4: Use the model from step 1 with the new user's data to make predictions for how they would rate (0-5) for all movies in the database and make a list.
* Step 5: Output the top 5 recommendations. 


## 5. Modeling

### Overview
To determine the best collaborative filtering model, multiple iterations were performed utilizing the `surprise` module's built-in capabilities. The metric for evaluation was Root Mean Square Error (RMSE) as this is a standard error metric and well-suited for explicit ratings predictions. Considering that the scale is (0-5), we're targeting something less than 1, and maybe even within 0.5. 

### Random Baseline
At a minimum, we wanted our model to beat (ie have a lower RMSE) than two random prediction models. One picks a rating (0.0-5.0) at random. The other will assume the rating is just the median rating of the entire set, which in this case is 3.5. The results of this show an RMSE of the median case is the lowest, at approximately 1.04.

### Model Testing
After that, we utilized the `surpise` method to test SVD with GridSearch, KNNBasic, and KNNBaseline. KNNBasic and KNNBaseline hyperparameters were tested manually, alternating between pearson/cosine similarities and user/item based filtering.

### Cross-Validation and Hypertuning
Cross-validation was performed using testsets for each algorithm tested. We used 5-fold cross-validation (default hyperparameters) during hypertuning of the SVD model, using the CVGridSearch function in `surprise`. Actual 

### Best Results
The method with the lowest RMSE (0.855) was a user-based, SVD with tuned hyperparameters {n_factors=150, n_epochs=25, lr_all=0.010, reg_all=0.05}. The KNN_baseline algorithm had a the next lowest RMSE utilizing similarity metric of pearson correlation coefficient and user-based filtering. 


## 6. Sample Input/Output
So... the moment of truth. Did the model work? Or even worse, do I have bad tase in movies?

### Sample input
Some input below. You can see I've rated a John Mulaney comedy highly. The CHiPs movie? Not so much.

![input](images/input.png)

### Output

![output](images/output.png)

The output is spot on. I love four out of five of these movies. And I've never seen No. 4. Maybe I'll stream it tonight!


## 7. Summary

We were able to create a movie recommendation system that could help with user indecision to boost engagement on streaming platforms. Our system created a model using collaborative filtering on explicit ratings using the `suprise` module. We got an average accuracy of less than a point, and were able to successfully pick some movies for *this* developer to watch this weekend!







