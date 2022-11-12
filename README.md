# Udacity Project 2: Wrangle And Analyze Data

Data wrangling is a process that involves gathering, assessing and cleaning of data to make data analysis
possible. In this project I gathered, assessed, cleaned, and analysed data from WeRateDogs; a professional
dog rating platforms that rates people’s dog with humorous comment about the dog.

The datasets were gathered from three different sources; twitter API, via a link, and the last one was
downloaded from Udacity learning platform. The datasets were assessed both visually (on excel spreadsheet)
and programmatically for quality and tidiness issues.

After assessing the datasets, some of the following quality and tidiness issues identified are listed below;


## Quality Issues

This deals with issues relating to contents.
1. Inaccurate and inconsistent numerator and denominator ratings in the twitter-archived dataset which was
   resolved replacing the ratings with the accurate rating using pandas **.at** function. 
2. The dataset contains comment and retweet: comments are replies to tweets. Since we only needed
   live ratings for our analysis, rows in which “in_reply_to_status_id” and “retweeted_status_id” columns
   in the twitter-archive-enhanced dataset in are not null were drop
3. Two dog stages for the same dog image: Another quality issue that was addressed in the project were
   instances where a dog is said to be in different dog stages at the same time. 
4. Inaccurate prediction for some dog images: in the image prediction dataset, some dog images were
   falsely predicted as not dog hence, were not drop. Every other image where “p1_dog”, “p2_dog” and
   “p3_dog” are “False” were dropped since we only need dog rating
5. Some images are not dog images: some of the images that are rated in the twitter archive dataset
   were not of dog images. Merging the image prediction and twitter-archive-enhanced datasets
   using pandas “merge” function with its default parameter, ensured that ONLY rated dog images are
   were analysed.
   
   
## Tidiness Issues

According to [Hadley Wickham](https://vita.had.co.nz/papers/tidy-data.html), a data is said to be tidy 
if each variable forms a column, each observation forms a row and each type of type of observational 
unit forms table.
1. Tweets and tweet’s URL in the same column: in the text column of the twitter enhanced table, tweets
   and the tweet’s URL are in the same column. The tweet’s ULR was separated to a new column using
   regular expression and pandas extract function.
2. Three breed’s names for the same dog image: due to the number of prediction models used to predict
   the dog breed’s type of each dog image, the image prediction dataset has three different columns for
   the same observation. This was compressed into one column by selecting the result of the model with
   the most confident prediction and where “p1_dog”, “p2_dog” or “p3” is “TRUE.”
