--- 

# Project 3: Web APIs & NLP

--- 

## Executive Summary

### Problem Statement

Can we predict which posts came from the "Animal Crossing" and "The Sims" Subreddit?

With an increased rate of children spending time on entertainment devices, there are parental concerns on whether or not a game is appropriate for their children. Many popular games have Subreddit pages in which fans of said game post updates, gameplay and content. This makes Reddit a useful website on gaming information. 

A group of employees at Reddit came up with classification models to analyze and supervise Subreddits in order to make sure that posts are being posted on the correct Subreddit. Currently, Reddit has moderators “to help guide and create Reddit's many communities. Each Reddit community has its own focus, look, and rules, including what posts are on-topic there and how users are expected to behave [source](https://reddit.zendesk.com/hc/en-us/articles/204533859-What-s-a-moderator-#:~:text=A%20moderator%2C%20or%20a%20mod,users%20are%20expected%20to%20behave.&text=Add%20other%20redditors%20as%20moderators.).”

To improve the accuracy and automation of on-topic posts on Subreddit pages, the group of employees at Reddit will be building models and comparing two similar life-simulation games.

This project will be utilizing the Pushshift Reddit API to obtain the "Animal Crossing" and "The Sims” Subreddit pages from Reddit. The type of models that will be developed are Multinomial Naive Bayes, Random Forest, and Logistic Regression and will be evaluated based on the accuracy in which the model is able to predict whether or not the user's post comes from the Animal Crossing or Sims Subreddit page.

### Description of Data

From the "Animal Crossing" Subreddit, I created a dataframe of 1100 rows an saved it as [`animal_crossing.csv`](./datasets/animal_crossing.csv). I then created a dataframe of 1100 rows and saved it as [`sims.csv`](./datasets/sims.csv). For both dataframes, the only columns included were "subreddit", "selftext", and "title".
Lastly, I merged the two dataframes into one final dataframe [`subreddit`](./datasets/subreddit_merged.csv).

#### Size
The size of the `animal_crossing.csv` dataset is 1100 rows and 3 columns.
The size of the `sims.csv` dataset is  1100 rows and 3 columns.
The size of the `subreddit_merged.csv` dataset is 2053 rows and 8 columns.

#### Source
Provided using Pushshift's API:
[r/animalcrossing](https://api.pushshift.io/reddit/search/submission?subreddit=animalcrossing)

[r/thesims](https://api.pushshift.io/reddit/search/submission?subreddit=thesims)

#### Target
Target is a classification analysis predicting which post came from which subreddit (Animal Crossing or The Sims).

#### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|subreddit|object|subreddit|Title of Subreddit|
|selftext|object|subreddit|Text in something|
|title|object|subreddit|Title of Reddit post|
|label|integer|subreddit|Subreddit into binary labels (Sims = 0 and Animal Crossing = 1)|
|full_text|object|subreddit|Selftext and Title columns combined|
|tokenized_sentences|object|subreddit|Tokenized sentences from full_text|
|full_text_length|integer|subreddit|Count of full_text characters|
|full_text_word_count|integer|subreddit|Word count for full_text|

#### Model Performance on Training/Test Data
|Model|Train Score|Test Score|
|---|---|---|
|Multinomial Bayes (Count Vectorizer)|0.932|0.835|
|Multinomial Bayes (TF-IDF Vectorizer)|0.956|0.852|
|Random Forest (Count Vectorizer)|0.906|0.778|
|Random Forest (TF-IDF Vectorizer|0.999|0.765|
|Logistic Regression (Count Vectorizer)|0.995|0.813|
|Logistic Regression (TF-IDF Vectorizer)|0.735|0.667|

### Conclusion/Recommendations
In conclusion, I found that my models were overfit. This may be due to words such as “sims” and “sim” that occured many times in posts and were included in the model.

But, by utilizing Count Vectorizer and TF-IDF Vectorizer, I found that the best models were the Multinomial Naive Bayes Model. They were the least overfit models while also getting the highest specificity when compared to the Random Forest and Logistic Regression Models. I found specificity to be more important for this problem because between the two games, it would be best to classify Animal Crossing as the Sims rather than putting the Sims into Animal Crossing. This is because The Sims is rated more explicit when compared to Animal Crossing.

Based on my findings of the Multinomial Naive Bayes model, as a Reddit employee I would say that parents should use Reddit as an informational tool and feel confident in using Subreddit pages to look into gaming information. However, I think that further fine-tuning of hyper-parameters is needed in order to get a better model.


### Next Steps
Next Steps: 
- Take out stop-words such as "sims" and "sim" and see how the model will run
- Do more data cleaning such as looking at emojis, hyperlinks, videos, etc.
- Create my own list of words that may be positive/negative that pertain more to the game and test on the sentiment analysis
- Tune parameters carefully to avoid overfitting