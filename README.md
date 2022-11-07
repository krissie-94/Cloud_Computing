# Cloud_Computing
Page Rank on GCP with Scala and PySpark
# A. Page Rank
![prank_img1](https://user-images.githubusercontent.com/81246356/200151934-0bad9be0-a16b-4672-9790-779552f96fdb.jpg)

**Page Rank Overview**
- If
1. The initial PageRank value for each webpage is 1.
PR(A) = 1
PR(B) = 1
PR(C) = 1
2. Page B has a link to pages C and A
3. Page C has a link to page A
4. Page D has links to all three pages
- and
1. A's PageRank is
PR(A) = (1-d) + d * (PR(B) / 2 + PR(C) / 1 + PR(D) / 3)
2. B's PageRank is
PR(B) = (1-d) + d * (PR(D) / 3)
3. C's PageRank is
PR(C) = (1-d) + d * (PR(B) / 2 + PR(D) / 3)
4. D's PageRank is
PR(D) = 1-d
5. Damping factor is 0.85

- Then after first Iteration
- **A. Output**
1. Page B would transfer half of its existing value, or 0.5, to page A and the other half, or 0.5, to page C.
2. Page C would transfer all of its existing value, 1, to the only page it links to, A.
3. Since D had three outbound links, it would transfer one third of its existing value, or approximately 0.33, to A.
- **B. Input**
1. PR(A)
= (1-d) + d * (PR(C) / 1 
= (1-0.85) + 0.85 * ( 1 )
= 1
2. PR(B)
= (1-d) + d * (PR(A) / 2)
= (1-0.85) + 0.85 * 0.5
= 0.575
3. PR(C)
= (1-d) + d * (PR(A) / 2 + PR(B) / 1)
= (1-0.85) + 0.85 * (0.5 + 1)
= 1.425
4. PR(D)
= 1-d
= 0.15
- **Process of Calculating Page Rank**
1. Initialize each page’s rank to 1.0
2. On each iteration, have page p send a contribution of rank(p) / numNeighbors(p) to its neighbors (the pages it has links to).
3. Set each page’s rank to 0.15 + 0.85 * contributionsReceived.
Note:
- 0.85 is the damping factor
# **Observation of Page Rank**
- A web page does not have input will have:
- constant PageRank: 1-d
- the smallest PageRank
- Input Web Pages' impact to the PageRank of a web page
- The more Input Web Pages the better.
- The higher PageRank of an Input Web Page the better.
# **B. Page Rank + PySpark + GCP**
### 1. **Setup PySpark on GCP**
- Enable Computer Engine API on Google cloud
- Create Dataproc cluster
- Configure and start running the cluster on Google cloud
![create-cluster_img2](https://user-images.githubusercontent.com/81246356/200157646-ff80b7b0-1e53-4928-878c-9e596fe4c3f9.jpg)
![create-cluster_img3](https://user-images.githubusercontent.com/81246356/200204710-6aa25f7c-a6bb-4cf8-bead-209427b92396.jpg)


- Connect to Master node by clickin on SSSH
![connect to ssh](https://user-images.githubusercontent.com/81246356/200157820-82f7f5e2-3cb0-4b9c-b03b-4a6a91801bff.jpg)
- Install Scala
```
$ curl -fL https://github.com/coursier/launchers/raw/master/cs-x86_64-pc-linux.gz | gzip -d > cs && chmod +x cs && ./cs setup
$ export SCALA_HOME=/usr/local/share/scala 
$ export PATH=$PATH:$SCALA_HOME/ 
```

### 2. **Do this question using Pyspark**
<img width="161" alt="do this question" src="https://user-images.githubusercontent.com/81246356/200159042-e0baa134-3f3f-460e-8684-e9472db25298.png">

1. Manually calculate the first two(2) iterations of the pagerank
 
- Frist iteration A = 1 B = (1/2) = 0.5 C = 1 + (1/2) = 1.5 PageRank (A) = 1 – 0.85 + 0.85 * 1 = 1 PageRank (B) = 1 – 0.85 + 0.85 * 1 = 0.575 PageRank (C) = 1 – 0.85 + 0.85 * 1.5 = 1.425

- Second iteration A = 1 B = (1/2) = 0.5 C = 0.575 + (1/2) = 1.075 PageRank (A) = 1 – 0.85 + 0.85 * 1.425 = 1.36125 PageRank (B) = 1 – 0.85 + 0.85 * 0.5 = 0.575 PageRank (C) = 1 – 0.85 + 0.85 * 1.075 = 1.06375
- 
3. Prepare Data in hadoop distributed file system hdfs
- Manually input the Data
```
vi pagerank_data.txt
```

### Data

```
A B
A C
B C
C A
```
 ### Create a dictory to store the data
```
hdfs dfs -mkdir hdfs:///mydata 
hdfs dfs -put pagerank_data.txt hdfs:///mydata
```
### RUn this command to verify data is stored in directory
```
hdfs dfs -ls hdfs:///mydata 
```
### Prepare  the program 

```
 pagerank.py
```
### Run the program with PySpark

```
pyspark
```
![pagerank-inut-pyspark1 0](https://user-images.githubusercontent.com/81246356/200213653-ff7da045-1d68-4e55-89b4-f61594ce113f.jpg)

# Result

- **Final output**
![pagerank-output_yspark_final](https://user-images.githubusercontent.com/81246356/200213687-0554da28-13a2-4df9-ba14-a7194a1d1c2c.jpg)

 # **B. Page Rank + Scala + GCP**
 
 ## Setup Scala On GCP##
1. Create a cloud storage bucket
![scala_bucket1](https://user-images.githubusercontent.com/81246356/200214656-ffd62c7f-e261-421e-b8b5-61451a5c0168.jpg)
2. Create a Dataproc Cluster
![create-cluster_img3](https://user-images.githubusercontent.com/81246356/200214679-50b729e2-ce9f-4a21-b79e-94bfd4b55aaf.jpg)
3. Connect to master node ssh

![masternode-scala](https://user-images.githubusercontent.com/81246356/200214892-f1076781-de09-4ad3-8349-d373a26b1de0.jpg)

4. Install Scala
```
$ curl -fL https://github.com/coursier/launchers/raw/master/cs-x86_64-pc-linux.gz | gzip -d > cs && chmod +x cs && ./cs setup
$ export SCALA_HOME=/usr/local/share/scala 
$ export PATH=$PATH:$SCALA_HOME/ 
```


# Do this question Using Scala#

### Manually Input the data
```
vi pagerank_data.txt
```
### Data
```
A B
A C
B C
C A
```
### Create a dictory to store the data
```
hdfs dfs -mkdir hdfs:///mydata 
hdfs dfs -put pagerank_data.txt hdfs:///mydata
```
### RUn this command to verify data is stored in directory
```
hdfs dfs -ls hdfs:///mydata 
```
### Prepare and run the program in Scala

```
spark-shell
```
- First Iteration
![scala_implementation-img1](https://user-images.githubusercontent.com/81246356/200219074-200e0da0-3796-45a7-86a2-157ca19b54a3.jpg)

![scala_implementation-img2](https://user-images.githubusercontent.com/81246356/200219120-102ec432-3ad6-49f7-8cbb-5444634d1813.jpg)

- Second Iteration
![scala_implementation_img_try1](https://user-images.githubusercontent.com/81246356/200219156-6e033e25-f846-494b-a38b-5babb46d9eef.jpg)

![scala_implementation_img_try2](https://user-images.githubusercontent.com/81246356/200219170-87bb18a0-1d05-47cc-acf3-9b0219def7eb.jpg)


# Sut Down the Cluster to Save credit


![shut down cluster GCP scala](https://user-images.githubusercontent.com/81246356/200219443-f7720229-aaa9-4608-a9a7-eae79f49ea63.jpg)



# Google Slide Presentation of Design and Implementation steps in Detail
PageRank On GCP
[title](PageRank On GCP)

