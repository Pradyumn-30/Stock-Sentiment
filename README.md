# Stock-Sentiment

Sentiment Analysis of TESLA stocks using Recurrent Neural Network

---
## Project Description

This project aims at classifying tweets into positive, neutral, and negative sentiment and building a classification model to predict the sentiment of tweets.

---
## Data Cleaning and Preprocessing

TESLA tweets are scrapped from Twitter using snscrape module. Data consists of TESLA related tweets from 21-04-2021 to 21-05-2021. Data is in .csv format and has 59,025 records with three columns (date, content, and username).
Data has no missing values.

remove_url(text) : Removes URLs from tweet text

remove_mentions(text) : Removes mentions from tweets

remove_hashtags(text) : Removes hastags from tweets

remove_whitespace(text) : Removes extra whitespaces from tweet text

The above modules uses regular expressions to carry out the related tasks.

Duplicates were dropped.

## Labelling tweets with sentiment score

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

## Data Cleaaning for Classification Task

Apart from removing URLs, mentions, and hastags we need to remove punctuations, special characters, and emoticons from tweet before we go for classification task.

Every character in the tweet was changed to lowercase and then stop words using nltk library, punctuations, special characters, and emoticons were removed.

Each word was lemmatized (changed to its root form) using Text blob lemmatizer.

##Balancing the dataset

Since accuarcy was considered as the evaluation metric it is important to balance the dataset first.

Dataset was balanced by taking a random sample of 11466 records from data with class 0 and 2. This makes all three classes to have 11466 records. Now dataset has total of 34398 records.

## Tokenizing the tweets

Tokenizer with 5000 words were used and fitted on the cleaned tweets to obtain corresponding text vector. Text vector was padded with zeros so that each text vector has same length.

## Training the model

Dataset was split into training set (0.90) and validation set (0.10).

A Sequential model was trained with an Embedding layer of 5000 words, dropout layer with 0.80, LSTM layer with tanh activation function and the last output layer with 3 nodes and sigmoid activation function.

Categorical cross entropy was used as the loss function and adam as the optimizer.

With batch size of 150 records model was fitted for 15 epochs with Early stopping (for regularization).

After 6 epochs traing was stopped with ***0.89 % training accuracy*** and ***0.85 % vaildation accuarcy***.

## Evaluating different models

Different Sequential models were trained to comapare the results

1. Sequential model with Embedding layer of 5000 words and 0.80 dropout

Training accuracy: 0.89

Validation accuracy: 0.85

2. Sequential model with Embedding layer of 3000 words

Training accuracy: 0.88

Validation accuracy: 0.84

3. Sequential model with Embedding layer of 3000 words and L2 regularization

Training accuracy: 0.88

Validation accuracy: 0.83

4.  Sequential model with Embedding layer of 5000 words

Training accuracy: 0.90

Validation accuracy: 0.84

---

Clerly first model performed the best ( low bias and low variance) and the last model performed the worst (high varaince model)


 















