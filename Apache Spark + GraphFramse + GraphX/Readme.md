
# Graphs
A graph is a data structure having edges and vertices. The edges carry information that represents relationships between the vertices.

The vertices are points in an n-dimensional space, and edges connect the vertices according to their relationships:
![image](https://user-images.githubusercontent.com/81246356/208616353-f363b48b-1066-4766-b61d-799e3cb28270.png)
In the image above, we have a social network example. We can see the vertices represented by letters and the edges carrying which kind of relationship is between the vertices.

## Spark GraphX?
### GraphX is the Spark API for graphs and graph-parallel computation. It includes a growing collection of graph algorithms and builders to simplify graph analytics tasks. GraphX unifies ETL, exploratory analysis, and iterative graph computation within a single system. You can view the same data as both graphs and collections, transform and join graphs with RDDs efficiently, and write custom iterative graph algorithms using the Pregel API.

## GraphFrames 

### GraphFrames is a package for Apache Spark that provides DataFrame-based graphs. It provides high-level APIs in Java, Python, and Scala. It aims to provide both the functionality of GraphX and extended functionality taking advantage of Spark DataFrames. This extended functionality includes motif finding, DataFrame-based serialization, and highly expressive graph queries.

### GraphFrames and GraphX are useful tools for working with graph data in Spark. However, GraphFrames is generally easier to use and more efficient, as it is built on top of the DataFrame API, which is more optimized for large-scale data processing.

# Dataset
![image](https://user-images.githubusercontent.com/81246356/208618400-20eb51f2-5c21-49cb-bf7d-d499f76a9f1f.png)

![image](https://user-images.githubusercontent.com/81246356/208618463-a9363cca-fee0-43a4-af07-282b206f54d0.png)

![person and relation csv file](https://user-images.githubusercontent.com/81246356/208655258-14158d22-4d4b-42f5-85ca-a25f46ce3718.jpg)


# I already have VM installed so Just SSH to VM 
- Install Java
```
sudo apt-get update
sudo apt-get install openjdk-11-jdk
```
- Install Spark and Unpark it
```
wget https://dlcdn.apache.org/spark/spark-3.3.1/spark-3.3.1-bin-hadoop3.tgz
tar -xvf spark-3.3.1-bin-hadoop3.tgz
mv spark-3.3.1-bin-hadoop3 spark
```
# Create graphX directory and then prepare person.csv and relationship.csv file into graphX directory


![mkdir img-1](https://user-images.githubusercontent.com/81246356/208629949-197798df-0324-47b1-ac5f-7187d2bdff81.jpg)

# Install Numpy Library

```
sudo apt install python3-pip
pip3 install numpy
```
# Prepare for the Code
Download graphx.py: https://github.com/divyapandey03/Cloud-Computing/blob/main/Apache%20Spark%20%2B%20GraphFramse%20%2B%20GraphX/graphX.py

# Download GraphFrames jar file:
https://repos.spark-packages.org/graphframes/graphframes/0.8.2-spark3.1-s_2.12/graphframes-0.8.2-spark3.1-s_2.12.jar

![get-packages](https://user-images.githubusercontent.com/81246356/208646547-59fcfcf4-1425-4d47-add0-4b614fc03acd.jpg)


# Submit PySpark Job:
spark-submit --packages graphframes:graphframes:0.8.2-spark3.1-s_2.12 graphX.py

# Result
## GraphFrames
![graphframe output](https://user-images.githubusercontent.com/81246356/208653738-aa034190-b815-4f54-bbc4-778876194d4f.jpg)

![graphframe output-2](https://user-images.githubusercontent.com/81246356/208653752-5504e35c-4ee2-42f9-9b0c-424dbe2f3abc.jpg)

## TriangleCount
![triangle Count img-1](https://user-images.githubusercontent.com/81246356/208653807-4518a3ff-c8e4-4e6c-ba45-ed7a67d64442.jpg)

![triangle count output img-2](https://user-images.githubusercontent.com/81246356/208653864-7050d666-28ce-4863-8550-0191be6ea0b3.jpg)

![triangle count img-3](https://user-images.githubusercontent.com/81246356/208653885-e9da0127-42b6-4d1c-99d0-42568908db69.jpg)

![triangle count img-4](https://user-images.githubusercontent.com/81246356/208653911-69fac5b5-130f-40d2-8748-ee40459cb58f.jpg)

![triangle count output 2 3 4 5](https://user-images.githubusercontent.com/81246356/208653956-5d73e978-9f46-4f92-a16f-1ed7e9b0e6aa.jpg)

## PageRank

![pagerank img-1](https://user-images.githubusercontent.com/81246356/208654031-5ea282cf-8856-478f-9fd1-19a0dea870ea.jpg)

![pagerank img-2](https://user-images.githubusercontent.com/81246356/208654052-0658eda5-8ed6-4e1d-9baf-8e2a72e362f7.jpg)

## BFS
![bfs img-1](https://user-images.githubusercontent.com/81246356/208654141-aed97b73-998b-4f05-872e-0a65da47f0a6.jpg)

![bfs img-2](https://user-images.githubusercontent.com/81246356/208654167-e972f761-2462-4af4-bf9f-6d4388318477.jpg)

![bfs img-3](https://user-images.githubusercontent.com/81246356/208654199-9ce431fb-bdbe-424a-b65b-6186c9c83534.jpg)

# References
[Graphrames and Dataframes](https://graphframes.github.io/graphframes/docs/_site/index.html)
[Intoduction to Spark GraphFrames](https://www.baeldung.com/spark-graph-graphframes)

[Google Slide Presentaition for further detail](https://docs.google.com/presentation/d/1czQ5NuH8qud1Y95TqoVk1nD6JRV4bb43W-YHf-4GCmI/edit?usp=sharing)
