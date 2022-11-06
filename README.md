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
= (1-d) + d * (PR(B) / 2 + PR(C) / 1 + PR(D) / 3)
= (1-0.85) + 0.85 * (0.5 + 1 + 0.33)
= 1.71
2. PR(B)
= (1-d) + d * (PR(D) / 3)
= (1-0.85) + 0.85 * 0.33
= 0.43
3. PR(C)
= (1-d) + d * (PR(B) / 2 + PR(D) / 3)
= (1-0.85) + 0.85 * (0.5 + 0.33)
= 0.86
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
###**1.Setup PySpark on GCP**


