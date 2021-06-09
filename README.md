# Stock-Sentiment

Sentiment Analysis of TESLA stocks using Recurrent Neural Network

---
## Project Description

This project aims at classifying tweets into positive, neutral, and negative sentiment and building a classification model to predict the sentiment of tweets.

---
## Data Cleaning and Preprocessing

TESLA tweets are scrapped from Twitter using snscrape module. Data consists of TESLA related tweets from 21-04-2021 to 21-05-2021. Data is in .csv format and has 59,025 records with three columns (date, content, and username).
Data has no missing values.

remove_url(text) : Removes url from tweet text

remove_mentions(text) : Removes mentions from tweets

remove_hashtags(text) : Removes hastags from tweets

remove_whitespace(text) : Removes extra whitespaces from tweet text

The above modules uses regular expressions to carry out the related tasks.

Duplicates were dropped.

##Labelling tweets with sentiment score

VADER sentitment library is used to attach a sentiment score (compound score) to every single tweet. VADER uses an inbuilt dictionary of words (keys) and the corresponding sentiment score (values). This dictionary can easily be updated depending on the domain we are working. For example here we added words like bear and bull (which are commonly used in stock market) along with corresponding sentiment score.

VADER takes into account emojis, punctuations, and capitalization to generate the compund score and hence we do not remove emojis and punctuations at this point. Also note we did not convert tweet to lower case yet.

compound score < 0 ----> Negative Sentiment
compound scaore = 0 ----> Neutral Sentiment
comopund score > 0 -----> Positive Sentiment

Using the above criterion tweets are labelled 1, 0, and 2 for negative, neutral, and positive sentiment respectively. For this another feature 'sentiment' is created.


A simple group by sentiment score shows dataset is higly imbalanced.
1 ---> 11467 records
0 ---> 20609 records
2 ---> 26949 records

![Capture](https://user-images.githubusercontent.com/53952516/121306860-fd3f8d80-c91c-11eb-8501-3be4affc9359.PNG)

Compound scores were resampled day wise and mean compound score for everyday was computed.
A simple line graph was plotted to see how average sentiment varies everyday.

![Capture](https://user-images.githubusercontent.com/53952516/121307514-b0a88200-c91d-11eb-99f5-f3a06c1f0667.PNG)







