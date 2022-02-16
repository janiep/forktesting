--- 

# Spotify: Top 200 Weekly (Global) Song Analysis

--- 

## Executive Summary


### Problem Statement
Utilizing Spotify's Top 200 Weekly (Global) charts from 2020 and 2021, can we idenitfy what makes a song popular based on specific features of a song?

For this project, I will build a regression model to predict a song's popularity. Model performance will be determined by the root mean squared error and R2 score. The success of the model will be measured by an increase of at least 10% from the baseline score.

By looking into this problem, this could potentially help new musicians or independent artistswho are trying to get their song recognized.

### Description of Data
From the dataset, ['spotify_dataset.csv'](./datasets/spotify_dataset.csv), I created several CSV files from data cleaning and preprocessing.

Datasets that were created through data cleaning and preprocessing:
-genre.csv: Genres exploded and dummified
-spotify_df.csv: Dataframe with genres combined
-poly_features_df.csv: Create polynomial features on audio features
-final_df.csv: Combine polynomial features and finalized cleaning of dataset

#### Size
-spotify_dataset.csv (original dataset): 1556 rows and 23 columns
-genre.csv: 1545 rows and 15 columns
-spotify_df.csv: 1545 rows and 37 columns
-poly_features_df.csv:
-final_df.csv

#### Source
The dataset, "Spotify Top 200 Charts (2020-2021)" is from [Kaggle](https://www.kaggle.com/sashankpillai/spotify-top-200-charts-20202021).


#### Target
Target is a regression analysis predicting popularity of a song (0-100).

#### Data Dictionary
All songs reflect the Spotify Top 200 Weekly Global Charts in 2020 and 2021.

|Feature|Type|Dataset|Description|
|---|---|---|---|
|highest_charting_position|integer|spotify_dataset|Highest charting position the song has had|
|number_times_charted|integer|spotify_dataset|Number of times the song has been charted|
|week_highest_charting|object|spotify_dataset|Week when the song had the highest position on the charts|
|song_name|object|spotify_dataset|Name of song|
|streams|float|spotify_dataset|Number of streams|
|artist|object|spotify_dataset|Name of artist|
|artist_followers|float|spotify_dataset|Number of followers the artist has on Spotify|
|genre|object|spotify_dataset|Genre the song is classified as|
|release_date|datetime|spotify_dataset|Release date of the song|
|weeks_charted|object|spotify_dataset|The weeks the song was on the Top 200|
|popularity|float|spotify_dataset|Popularity of the song from 0-100 (highest)|
|danceability|float|spotify_dataset|How suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable [(source)](https://www.kaggle.com/sashankpillai/spotify-top-200-charts-20202021)|
|tempo|float|spotify_dataset|The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or pace of a given piece and derives directly from the average beat duration [(source)](https://www.kaggle.com/sashankpillai/spotify-top-200-charts-20202021)|
|duration_ms|float|spotify_dataset|Duration of song in milliseconds|
|valence|float|spotify_dataset|A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more negative (e.g. sad, depressed, angry) [(source)](https://www.kaggle.com/sashankpillai/spotify-top-200-charts-20202021)|
|chord|object|spotify_dataset|Chord of the song|
|start_week_highest_charting|datetime|spotify_df|The start of the week of highest number times charted|  
|end_week_highest_charting|datetime|spotify_df|The end of the week of highest number times charted|  
|contemporary|unsigned integer|genres|Count of songs with contemporary genre|
|edm|unsigned integer|genres|Count of songs with edm genre|
|electropop|unsigned integer|genres|Count of songs with electropop genre|
|hip hop|unsigned integer|genres|Count of songs with hip-hop genre|
|house|unsigned integer|genres|Count of songs with house genre|
|indie|unsigned integer|genres|Count of songs with indie genre|
|latin|unsigned integer|genres|Count of songs with latin genre|
|other|unsigned integer|genres|Count of songs with other genre (genres not listed)|
|pop|unsigned integer|genres|Count of songs with pop genre|
|rap|unsigned integer|genres|Count of songs with rap genre|
|reggaeton|unsigned integer|genres|Count of songs with reggaeton genre|
|rock|unsigned integer|genres|Count of songs with rock genre|
|trap|unsigned integer|genres|Count of songs with trap genre|
|dance|unsigned integer|genres|Count of songs with dance genre|

#### Model Performance on Training/Test Data
|Model|Train Score|Test Score|
|---|---|---|
|Baseline: Linear Regression|0.159|0.119|
|Baseline: Decision Tree|1.0|0.380|
|Baseline: Random Forest|0.951|0.744|
|Decision Tree: Gridsearch|0.725|0.711|
|Random Forest: Gridsearch|0.923|0.755|
|Random Forest: Final Features & Gridsearch|0.903|0.848|

### Model Performance on Training/Test Data - Random Forest
|Model|Train Score|Test Score|
|---|---|---|
|Random Forest: Polynomial Features|0.962|0.794|
|Random Forest: Chord|0.962|0.799|
|Random Forest: Release Date/Year|0.972|0.868|
|Random Forest: After LASSO|0.972|0.872|
|Random Forest: Final Features & Gridsearch|0.903|0.848|

### Train/Test RMSE
|Model|Train Score|Test Score|
|---|---|---|
|Random Forest: Polynomial Features|2.91|6.66|
|Random Forest: Chord|2.93|6.58|
|Random Forest: Release Date/Year|2.49|5.32|
|Random Forest: After LASSO|2.48|5.25|
|Random Forest: Final Features & Gridsearch|4.65|5.71|

### Conclusion
Overall, by doing data cleaning on the genres and taking the 335 various genres and creating 14 larger "family" genres to group Overall, by doing data cleaning on the genres and taking the 335 various genres and creating 14 larger "family" genres to group the 335 genres in, using polynomial features, and creating dummified columns from catergorical features, I was able to create a model to predict the popularity score of a song on Spotify.

With the goal of improving the RMSE and R2 score of at least 10%, I was able to achieve a train RMSE score of 4.65 and a test RMSE 5.71 and a R2 train score of 0.903 and R2 test score of 0.848. The RMSE was improved by ~30% and the R2 test score was improved by ~14% (Baseline random forest model had a R2 train score of 0.951, test score of 0.745, RMSE train of 3.47, and RMSE test of 8.28). This was achieved through a random forest regressor model. Looking at the attribute, feature importances, I found that the amount of followers an artist has, number of times the song has been charted, number of streams, and the year the song was released were the most prominent features in predicting popularity.

