# Collaborative Filtering using MLlib
## 1. What is Collanorative Filtering :
### ***Collaborative filtering is commonly used for recommender systems. These techniques aim to fill in the missing entries of a user-item association matrix. spark.mllib currently supports model-based collaborative filtering, in which users and products are described by a small set of latent factors that can be used to predict missing entries.***
[Study Collaborative Filtering](https://spark.apache.org/docs/latest/mllib-collaborative-filtering.html)

# 2. Colab

### What is Colaboratory?
Colaboratory, or “Colab” for short, is a product from Google Research. Colab allows anybody to write and execute arbitrary python code through the browser, and is especially well suited to machine learning, data analysis and education. More technically, Colab is a hosted Jupyter notebook service that requires no setup to use, while providing access free of charge to computing resources including GPUs.

### Is it really free of charge to use?
Yes. Colab is free of charge to use.

[Study more anout Google Colab](https://research.google.com/colaboratory/faq.html#:~:text=The%20Basics&text=Colaboratory%2C%20or%20%E2%80%9CColab%E2%80%9D%20for,learning%2C%20data%20analysis%20and%20education.)

# 3. Experiment Pyspark code (ipynb) of PySpark Collaborative Filtering with ALS
### 1. Create a Google colab account if you don't have any and start a New Project
![img-1Google-colab](https://user-images.githubusercontent.com/81246356/203697014-90b4f3bf-e22f-4bd1-8eb0-90a306ceaf13.jpg)

### 2. Upload the your data for this project, mine is csv file. Next install PySpark on Google Colab
![img-2Google-colab](https://user-images.githubusercontent.com/81246356/203697342-5b937a57-71be-475a-874b-036c96d4cbaf.jpg)

# Cmpare Models and Make Recommendations
![img-3Google-colab](https://user-images.githubusercontent.com/81246356/203703878-efc964a9-bef8-4459-9b16-ab19c074cb88.jpg)
![img-4Google-colab](https://user-images.githubusercontent.com/81246356/203703900-a12d8a52-3f68-46f0-a985-faf52efb17c2.jpg)

## Show Result
![img-5Google-colab](https://user-images.githubusercontent.com/81246356/203704070-d1658e17-b2bc-42ff-9b29-e2887dc991f6.jpg)

## Save the modified ipynb file as py format
![img-6Google-colab](https://user-images.githubusercontent.com/81246356/203704381-0c2f767a-8c80-4fca-be42-dab64ff17b17.jpg)

## Save the modified ipynb file as html format

![save as html](https://user-images.githubusercontent.com/81246356/203704449-ffb9bf54-11d7-431f-bacb-def2145668bc.jpg)

# Run the py file saved on GCP
## Set up PySpark on GCP
- Make sure Enable Computer Engine API
- Configure and launch Google Cloud Dataproc Cluster 
![google cloud cluster](https://user-images.githubusercontent.com/81246356/203713556-9b0cdc3d-d514-4bbe-9229-2e62a4d934a7.jpg)
![dataproc-cluster](https://user-images.githubusercontent.com/81246356/203713812-61f94c1c-d237-4446-80ee-cda9ab863977.jpg)
# Connecting to the Master Node using Secure Shell (ssh)
![open-SSH-img1](https://user-images.githubusercontent.com/81246356/203721002-49878519-1804-43dd-8579-9bc0781a965f.jpg)

# Prepare Data in HDFS
- movies.csv
- rating.csv
- tags.csv
- movie_recommendation_mllibs.py

***1.Upload movies.csv and ratings.csv files at GCP***
![upload movies, ratings](https://user-images.githubusercontent.com/81246356/203723586-a31473b6-404a-4183-a3ad-492d7d023386.jpg)

***2. create a directory (folder) to store the data:
```
hdfs dfs -mkdir hdfs:///mydata 
hdfs dfs -put movies.csv hdfs:///mydata
hdfs dfs -put ratings.csv hdfs:///mydata
```
##  verify that the file is indeed located in the mydata folder by running  the following command:
```
hdfs dfs -ls hdfs:///mydata 
```
![add files to directory](https://user-images.githubusercontent.com/81246356/203724544-99abd5c1-1bcc-4e2b-b0f6-45b9af7d3d6e.jpg)


# 3.Prepare the program
- Upload the py file to GCP
```
vi movie_recommendation_mllibs.py
```
![movie-recommendation-](https://user-images.githubusercontent.com/81246356/203725851-6f23f4e9-6bf0-4804-93aa-082557eecf8c.jpg)

# Run the program with Pyspark

```
spark-submit recommendation_engine_movielens.py
```

# 5.Result
