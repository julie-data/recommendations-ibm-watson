# Recommendations with IBM Watson platform

### Table of Contents

1. [Installation](#installation)
2. [Project Motivation](#motivation)
3. [File Descriptions](#files)
4. [Results](#results)
5. [Licensing, Authors, and Acknowledgements](#licensing)

## Installation <a name="installation"></a>

The main component of the project is the python notebook Recommendations_with_IBM.ipynb. You should have all the other files in the same directory in order for the notebook to work.

## Project Motivation<a name="motivation"></a>

The goal of this project is to provide article recommendations to the users of the IBM Watson platform. We have at disposal the interactions data of users with the articles, which help us find similar users. 

## File Descriptions <a name="files"></a>

There are three types of files in this repository:

1. The folder data contains the raw data used in this project, in a csv format:
  - articles_community.csv: contains the article ids along with information on the article such as name and description
  - user-item-interactions.csv: contains a row for every time a user saw an article
  
2. The Jupyter notebook and HTML files are duplicates and contain the code and explanation of the project:
- Recommendations_with_IBM.ipynb
- Recommendations_with_IBM.html

3. The other files are used within the notebook as tests. They help making sure the code is providing the expected result.
- project_tests.py
- top_10.p
- top_20.p
- top_5.p

## Results<a name="results"></a>

Two methods were used to create recommendations. Here are the results for both methods:

1. Collaborative filtering and ranked based

We use collaborative filtering for users who have seen at least one project. We are calculating the similarity between users by taking the dot product between the users regarding whether they have seen a project or not. If multiple users have the same similarity, we choose the users that have the most total article interactions before choosing those with fewer article interactions. If we need to select only a subset of articles among those seen by a user, we choose articles within the articles with the most total interactions before choosing those with fewer total interactions. 

For the new users, we use the ranked-based approach.

2. Matrix Factorization with SVD

There are no null values in the matrix since we are not using ratings, but whether the user has seen an article or not. Therefore it is enough for us to use SVD, we do not need to use funkSVD which needs to be used when handling null values.

When using SVD on the test dataset, the accuracy decreases with the number of latent factors. This is due to the fact that only a small amount of users (20) are common between the train and test dataset. This makes that our data (0s and 1s) is imbalanced, that there is a big disproportionate ratio of 0s in the dataset compared to the 1s.

Moreover, when increasing the number of latent factors, we are increasing the overfitting on the training data (accuracy increases), which also explains why the accuracy on the testing dataset decreases.

## Licensing, Authors, Acknowledgements<a name="licensing"></a>

Thank you first to IBM for sharing their data, you can find more information about them [here](https://www.ibm.com/watson). Second, I would like to acknowledge Udacity for their great Data Scientist nanodegree of which this project is part of. Finally, I would like to thank Nicolas Essipova, my mentor for this Data Scientist nanodegree who have helped me out throughout this project.
