# Sentiment_Analysis
Healthcare Topic from Canadian Twitter Users

The basic selected features(attributes):
1. year, month, day (which were split from tweets created date) are the records created date. This datasets have 3, 5, 6, 7, 8, 9, 10 seven monthes.
2. user_name is the user’s profile name.
3. favorite_count is the count of the posted tweet where liked by other users.
4. Rewet_count is the count of the posted tweet be retweeted by others.
5. text is the sentences which the user posted.
6. usre_location_ab is the abbreviation of user defined provincial location.

Next important feature is the polarity. which means the positive when the number close with 1, extremely negative when the number reach to -1. We would use it as predicted variable in the future regression model. This attribute was created by TextBlob based on existing ‘text’ attribute.

Overall, Canadian twitter users’ view is prone to positive. The mean of polarity is 0.057. The histogram is slightly screw to the right.

Processing steps:

Step 1: <Data extraction from multiple Json files>
Tools: Pyspark, Pyspark.sql
1. The raw tweets have lots of irrelevant schemas and redundancy. 
2. The topic is about Canadian users, so the following step is to applypr NLP techniques to extract the user_location at the provincial level. 
        
Step 2: <Data combination and cleaning>
Tools: Pandas
1. Combine all of the files from step1 into one table.
2. Split create_date into year, month, day 3 features for future analysis.
3. Uniform the user’s location into abbreviation style.
4. Redundance remove, None value remove.
        
Step 3: < Labelling the data >
Tools: TextBlob, Pandas, Numpy
Twitter data missing the attribute label for sentiment analysis. The best process is label each tweets manually but it’s cost time. In my project, I just used TextBlob tool which can automatically label the records at once based on “text” feature. 

Step 4: < Feature Engineering >
Tools: Scikit-learn, Pandas, Numpy 
First step is to break the text down into tokens, then remove the most commonly “stop_words” which is the irrelevant data. Stop words are words which are commonly used in text, but irrelevant (such as “the, and, an”). Scikit_learn has build-in pools of the stop_words, which I used in my project.
After that, converted ‘text’ into a matrix of TF-IDF (stands for Term-Frequency-Inverse-Document Frequency)  features. TF-IDF Is TF* IDF.
Then, Combine “Unigram”, “Bigram”, “Trigram” with “Logistic Regression”, “linerSVC”, “Random Forest” respectively. So, in the next step we have six models.

Step 5: < Modeling Selection>
Tools: Scikit-learn, Pandas, Numpy 
We already have six models,  this step is to rank them with all of the featured be selected. The three ranking critires are Precision score, F1 score, Processing time. 

Step 6: < Model Tuning (Feature Selection)>
Tools: Scikit-learn
In this step, I only choose the top 4 models.
In order to comparing how much improved after tuning, I split the training data into 80% for training and 20% for validation.
Basically, I only compared some different ‘C’ and ‘tol’ parametes and select the one with the best accuracy score.

Step 7: < Evaluation>
Tools: Scikit-learn
Before modeling, the whole dataset has been split into test data (20%) and train data (80%). 
In the Model Tuning, the train data is further split into validate data (20%) and train data (80%).
So, finally, we use the first test data to do the cross validation in order to find how much inprove after tuning.



