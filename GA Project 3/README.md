

General Assembly Project 3: Web API and NLP

Author: Khoo Qi Xiang (DSI31)


This project comprises 3 notebooks:

Part 1 - Web Scraping

Part 2 - Data Cleaning and NLP

Part 3 - Processing & Modeling

## Introduction


We are a data science team that works for the renowned cosmetic company Diorz. Diorz values customer feedback and reviews highly, therefore a backend crew frequently monitors forum posts and comments using machine learning models to help direct keyword searches to the appropriate division.


## Problem Statement
- The backend team has informed the data science team that the machine learning model frequently jumbled up the perfume and makeup categories and placed them in the incorrect forum.

- An improved machine learning-based algorithm has been sought by the management team to find the appropriate category terms for cosmetics and scent. When the right words are chosen and sent to the relevant venue, the appropriate department can handle any problems or criticism. 
## Dataset 
Subreddit websites that were used for scraping:
- perfumes.csv -- https://api.pushshift.io/reddit/search/?subreddit=Perfumes
- makeup.csv -- https://api.pushshift.io/reddit/search/?subreddit=Makeup

https://github.com/pushshift/api/blob/master/README.md


## Data Dictionary



|Feature|Type|Description||
|---|---|---|---|
|subreddit|object|The name of the subbreddit that the comment came from.|
|selftext|object|The contents of the comment.|
|created_utc|int|The epoch time stamp of when the comment was created.|
|comment_length|int|How many characters the comment contains.|
|word_count|int|How many words the comment contains.|







## Data Cleaning and NLP

The DataFrame that was gathered was first cleaned using pandas, and I also used it to make sure that the function I made to scrape the data didn't have any duplicate rows. I also created features for measuring the length and word count of the selftext and title features. Following initial cleaning, I started to apply Natural Language Processing techniques to build upon the title and selftext elements that had already been extracted.

Once all the cleaning was complete, I began to explore the data to see what trends can be found to separate the two Subreddits. Using count vectorising and  TfidfVectorising I was able to see some trends of 2-words and 3-words that can be use to separate the two different Subreddit.


## Model used:
Vectorizers:
- CountVectorizer(Bi-gram) (CVEC)
- Term Frequency–Inverse Document Frequency Vectorizer (TFIDF)

Models/Classifiers:
- Naive Bayes 
- Logistic Regression
- Decision Tree Classifier
- Random Forests Classifier
- Gradient Boost

Metrics:
- Training/Testing Score

## Summary of the Five models:

|Vectoriser|Model|train|test|
|---|---|---|---|
|CVEC|Bernoulli Naive Bayes |0.565|0.564|
|TFIDF|Bernoulli Naive Bayes |0.563|0.563|
|CVEC|Multinomial Naive Bayes|0.561|0.564|
|TFIDF|Multinomial Naive Bayes|0.974|0.943|
|CVEC|Gaussian Naive Bayes |0.565|0.564|
|TFIDF|Gaussian Naive Bayes |0.968|0.887|
|CVEC|Logistic Regression|0.991|0.878|
|TFIDF|Logistic Regression|0.992|0.952|
|CVEC|Random Forest|0.993|0.840|
|TFIDF|Random Forest |0.997|0.935|
|CVEC|Decision Tree|0.993|0.771|
|TFIDF|Decision Tree|0.997|0.915|
|CVEC|Gradient Boost|0.711|0.692|
|TFIDF|Gradient Boost|0.897|0.881|

The final 2 models selected for final evaluation were:

|Vectoriser|Model|train|test|
|---|---|---|---|
|TFIDF|Multinomial Naive Bayes|0.974|0.943|
|TFIDF|Logistic Regression|0.992|0.952|

After that we ran a confusion matrixs on both the model with Grid search:

|Vectoriser|Model|train| Best test|Accuracy(Test Score)|Sensitivity|Specificity|Precision|
|---|---|---|---|---|---|---|---|
|TFIDF|Logistic Regression|0.983|0.948|0.951|0.958|0.941|0.955|
|TFIDF|Multinomial Naive Bayes|0.969|0.951|0.954|0.976|0.925|0.944|

In comparing our two best models, we prefer using our Multinomial NB model as compared to our Logistic Regression model. Main reasons for this: Best overall balance in our 4 metrics and the best score. Our Multinomial Naive Bayes scores over 94% on 2 out of 4 metrics, while specificity scores a hair below 92% and precision at 94%. Our Logistic Regression performed an impressive 95%+ on precision, but poorer than Multinomial NB for accuracy and sensitivity (95.1% and 95.8% respectively).

We prioritize accuracy and sensitivity as the key criteria for the model in order to address the problem statement. And as such, the best test result points to using a Multinomial NB model vs Logistic Regression (95.1% vs 94.8%), we believe that a Multinomial NB would be more reliable overall to meet the request of Diorz management.


Final Model:
|Vectoriser|Model|train| Best test|Accuracy(Test Score)|Sensitivity|Specificity|Precision|
|---|---|---|---|---|---|---|---|
|TFIDF|Multinomial Naive Bayes|0.969|0.951|0.954|0.976|0.925|0.944|


## Recommendation
Through the final model, we are able to :
- Solved the initial issues with the incorrect categorization.
- Create market plans based on trending and enhance any existing tactics in order to increase marketing efforts for the top-rated brands and goods in the posts.
- Able to identify and determine key words that can improve our product and services.

## Suggestion for further analysis:
- Expand data collection from other sources (not just Reddit).
- Identifying more stop words to reduce noise in our data.
- Improve the accuracy of predictions by trying and explore a more diverse range of models including but not limited to Random Forests Classifier, Ensemble Techniques, SVM, GLM in order to get better scores.