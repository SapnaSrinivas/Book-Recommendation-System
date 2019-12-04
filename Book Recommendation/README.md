# Capstone Project: Book Recommendation

Recommendation systems have been keeping my mind occupied for quite a while now and owing to my children's inclination for reading books, building book recommendation system is quite engaging.

Recommendation engine filters the data using different algorithms and recommends the most relevant items to users. It first captures the past behaviour of a customer and based on that, recommends products which the users might be likely to buy.


The project has 3 notebooks.
- First notebook : Gathered, cleaned the data and performed some exploratory data analysis.
- Second notebook : Performed Content Based Filtering
- Third notebook : Performed User-Item based collaborative filtering and Matrix Factorisation(Truncated SVD algorithm)

# Executive Summary

My journey to building Book Recommendation System began when I came across Book Crossing dataset. This dataset has been compiled by Cai-Nicolas Ziegler in 2004, and it comprises of three tables for users, books and ratings. 
Explicit ratings are expressed on a scale range from 1-10(higher values denoting higher appreciation) and implicit rating is expressed by 0.

Here 3 datasets are being provided. 
1. BX-Book.csv:
       shape   : (271360, 8)
       columns : ISBN, bookTitle, bookAuthor, yearofPublication, 
                 publisher, imageUrlS, imageUrlM, imageUrlL
2. BX-User.csv:
        shape  : (278858, 3)
        columns: userID, Location, Age
3. BX-Ratings.csv:
        shape  : (1149780, 3)
        columns: userID, ISBN, bookRating

### Book dataset provides the information of the books:

Firstly, i dropped all the image related columns as these will not help me to build recommendation engine. There were 3 null values in this dataset which i had filled up agter doing some googling.

Secondly in yearOfPublication, I found 4618 entries as zero and some incorrect entries. I corrected all the entries which were incorrect and replaced all the zero entries as NaN value.

Also I found some historical books whose year of publication is less than 1900 and there were some future books too which were greater than 2019.

I omitted all the historical and future books from the dataset as they may potentially skew the model.

Did some eda to find the top 10 publishers, book authors and famous book titles. While doing so, i found out that some books have multiple ISBN entries. Although all of the ISBN entries are unique in the 'books' dataframe, different forms of the same book will have different ISBNs - i.e. paperback, e-book, etc.

### User dataset  provides the information of the user:

Firstly the age column. The age range goes from 0 to 244 years old. Obviously these cannot be true. I'll set all ages less than 5 and older than 100 to NaN to try keep them realistic. Since, I am not considering the age as my feature for modelling, i will leave the unrealisitic ages as NaN values.

Location column is splitted into city, state and country column and later dropped the Location column. Did some eda to find the top 10 city and country where the users are from. while doing so I found that there were 4561 entries which has empty strings in the country column. Changed all those empty strings to NaN values.

### Ratings dataset has information of the rating which each user has given to each book.

We splitted the  ratings of the dataset into explicit and implicit ratings. The explicit ratings represented by 1 - 10 and implicit ratings is represented by 0 will have to be segregated now. We will be using only explict ratings for building our recommendation system. Similarly, users are also segregated into those who rated explicitly and those whose implicit behaviour was recorded. We are using only explicit ratings and users who have rated for recommendation.

Later we saved all the cleaned datasets.

## Content Based Filtering model:

This type of recommender uses the description of the item to recommend next most similar item. It uses the product features or keywords used in description to find the similarity between the items.

We cannot compute the similarity between the given description in the form it is in our dataset. For this purpose, TF-IDF is calculated for all the documents which would simply return you a matrix with each word representing a column. TFIDF Vectorizer would do this for us in a couple of lines.

We did the Cosine Similarity, Euclidean Distance and PearsonR correlation to measure how similar the documents are irrespective of their size.

## Collaborative Filtering for Item to Item based.

Collaborative filtering for recommender systems based on the similarity between items calculated using people's ratings of those items.

#### To implement item-based collaborative filtering:
K-NN is a perfect choice and also very good baseline for recommender system.
It uses a database in which the data points are separated into several clusters to make inference for new samples.
For high dimension space, we use cosine similarity for nearest neighbour search

#### To reduce the dimensionality, we did Truncated SVD algorithm.

Matrix Factorisation is simply a mathematical tool for playing around with matrices.The Matrix Factorisation techniques are usually more effective because they allow users to discover the latent (hidden) features underlying the interactions between users and items(books).

We use singular value decomposition (SVD)- one of the Matrix Factorisation model for identifying latent factors.

The SIngular Value Decomposition is a matrix decomposition method for reducing a matrix to its constituent parts in order to make certain subsequent matrix calculations simpler.


            