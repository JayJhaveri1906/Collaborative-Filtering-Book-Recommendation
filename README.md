# __Collaborative Filtering Based Recommendation System__
## Introduction
Developed a Recommendation System mimicking the infamous Netflix Competition as part of my midterm of CSE 258. 

## Dataset
The dataset is uploaded in tar zip format above. For detailed, explaination about the dataset please refer the [problem statement](https://github.com/JayJhaveri1906/Collaborative-Filtering-Book-Recommendation/blob/main/Assignment_1.pdf)

About the hidden test data: It was never released for me to link :)

## Models
I implemented previously learned Jaccard, Cosine, Pearson similarity based models. I will explain each of the sections below:

### Read Prediction
1) For read prediction, I first started with the most naive approach being the N most popular books being treated as read. I used the "74%" thresholding from HW3. Got a 0.7668 on gradescope.
2) Because I know the test set is evenly distributed between positive and negative samples, whatever models I tried next, I split it 50-50, and top 50 were marked as ones.

#### The models I tried are
* Using the ratings from Alpha and user and item bias values, I sorted these values in descending order for every user and marked the top 50 as ones and the bottom 50 as zeros. This gave me an accuracy of 0.6227
* Next, I tried to predict whether read or not based on rating prediction based on Jaccard similarity. Acc: 0.6993
* Normal Jaccard Similarity: Read prediction only based on max Jaccard values
* Inception Jaccard Similarity: Because the dataset is too sparse, I tried doing a multi-layered Jaccard wherein, instead of only getting the similarity of all the users of the predItem and set of all users of all items of predUsers, I tried doing all items of all the users of all items that were ever interacted with the pred user. Compared to all the items of all users who interacted with the pred item. Acc: It started with 0.76, but after some tweaking, it later shot up to 0.8247
* Also tried Jaccard similarity combined with most popular books, Cosine rating, and similarity, Pearson similarity, Libraries like LibRecommender, XgBoost, SVD from surprise library, and implicit BPR rating, all giving accuracy between 0.5-0.7
* Also tried a voting mechanism, where multiple models get a chance to vote, and the top 50% of votes get predicted as 1, the rest as 0. This improved the accuracy by 0.003.
#### Conclusion 
The data is too unrelated, with way less overlapping data for any traditional methods to work. Finally decided to go with the twisted inception Jaccard to artificially create a dense similarity score. 

### Rating Prediction
1) The first model I tried was from my HW3 submission of alpha and bias values with a lambda value of 4.46122830200134. This gave me an MSE of 1.47. 
2) I then counted and saw the trend of the number of ratings at each place, i.e., counts of 1-5 in the train data. I noticed that more people are voting 3 than 2, which makes sense considering human tendencies. So, I manipulated the ratings to round up to 3 if it is above 2.7 and less than 3. Also, I rounded off the numbers if they were within 0.1 of their round. This gave me an MSE of 1.4619, and I decided to finalize this.


## Resuts
Achieved top 20th position for prediction rating amongst the batch of 600 students and top 25th for read prediction.


###### P.S. The IPYNB file is well documented with testing resuts for each models, I highly recommend you to glance at it