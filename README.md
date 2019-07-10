# Sentiment_Analysis
Healthcare Topic from Canadian Twitter Users

The datasets are downloaded from the Harvard Dataverse using Hydrator tools. Those tweets are collected through healthcare relevant filter. There have 259GB JSON files were downloaded. 446011 tweets are posted by Canadian Twitter Users, after dropping the duplicates, only 294556 records left.

The basic selected features(attributes):
1. year, month, day (which were split from tweets created date) are the records created date. This datasets have 3, 5, 6, 7, 8, 9, 10 seven monthes.
2. user_name is the user’s profile name.
3. favorite_count is the count of the posted tweet where liked by other users.
4. Rewet_count is the count of the posted tweet be retweeted by others.
5. text is the sentences which the user posted.
6. usre_location_ab is the abbreviation of user defined provincial location.

Next important feature is the polarity. which means the positive when the number close with 1, extremely negative when the number reach to -1. We would use it as predicted variable in the future regression model. This attribute was created by TextBlob based on existing ‘text’ attribute.

Overall, Canadian twitter users’ view of healthcare topic is prone to positive, based on the mean of polarity is 0.055 and the histogram is slightly screw to the right.

Processing steps:

Step 1: <Data extraction from multiple Json files>
Tools: Python3, Pyspark, Pyspark.sql
1. The raw tweets have lots of irrelevant schemas and redundance need to be discarded. 
2. The topic is about Canadian users, so the following step is apply NLP techniques to extract the user_location at the proviencial level. 
        
Step 2: <Data combination and cleaning>
Tools: Pandas
1. Combine all of the files from step1 into one table.
2. Split create_date into year, month, day 3 features for future analysis.
3. Uniform the user’s location into abbreviation style.
4. Redundance remove, None value remove.
        
Step 3: < Labelling the data >
Tools: TextBlob
Twitter data missing the attribute label for sentiment analysis, I believe the better process is label each tweets manually but cost time. In my project, I was using TextBlob tool automatically label all of the records based on text.

Step 4: < Modeling >
Tools: TextBlob,pandas
First step is to break the text down says tokenization, then remove the most commonly “stop word” which is the irrelevant data. After that, combine “unigram”, “bigram”, “trigram” respectively with liner regression or Tree Kernel and do cross validation check which combination of the model is the best one.

Step 5: < …..>

