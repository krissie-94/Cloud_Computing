val sparkConf = new SparkConf().setAppName("PageRank")
val sc = new SparkContext(sparkConf)

// Assume that our neighbor list was saved as a Spark objectFile:
// - objectFile is a SequenceFile containing serialized objects, 
//   + with NullWritable keys and 
//   + BytesWritable values that contain a serialized partition.
// - The content of the file "links" 
//   + logically , it contains the list of neighbors of each page,
//     (pageID, linkList) 
//          (B (C,A))
//          (C (A))
//          (D (A,B,C))
//   + physically, it contains 
//          B C
//          B A
//          C A
//          D A
//          D B
//          D C
val links = sc.objectFile[(String, Seq[String])]("links")
              .partitionBy(new HashPartitioner(100))
              .persist()

// - Initialize each page's rank to 1.0; since we use mapValues, 
//   the resulting RDD will have the same partitioner as links
//       PR(A)=PR(B)=PR(C)=PR(D)=1
// - ranks contains the current rank for each page: (pageID, rank):
//      (B 1)
//      (C 1) 
//      (D 1)
var ranks = links.mapValues(_ => 1.0)

// Run 10 iterations of PageRank
for (i <- 0 until 10) {
  // Step 1: Obtain the link list and rank for each  page ID
  //         by joining between the current ranks RDD and the 
  //         static links RDD. 
  //             links.join(ranks)
  //         Iteration 0
  //           WebPage   Links       PageRank
  //           ---------------------------------
  //              (B     (C,A          1))
  //              (C     (A            1))
  //              (D     (A,B,C        1))
  // Step 2: Apply flatMap to the ouput of join to create “contribution” 
  //         values to send to each of the page’s neighbors. 
  //
  //              Dest WebPage      Contributed (i.e., received) PageRank
  //           -----------------------------------------------------------
  //               C                    0.5
  //               A                    0.5
  //               A                    1.0
  //               A                    0.33
  //               B                    0.33
  //               C                    0.33
  //               
  val contributions = links.join(ranks).flatMap {
    case (pageId, (links, rank)) =>
      links.map(dest => (dest, rank / links.size))
  }
  // Step 3: Add up "contribution" values by dest webpage (i.e. by the page 
  //         receiving the contribution) and set that page’s 
  //         rank to 0.15 + 0.85 * contributionsReceived.
  //
  //           A = 0.15 + 0.85 * (0.5 + 1.0  + 0.33) 
  //           B = 0.15 + 0.85 * 0.33
  //           C = 0.15 + 0.85 * (0.5 + 0.33) 
  //
  ranks = contributions.reduceByKey(_ + _).mapValues(0.15 + 0.85 * _)
}

// Write out the final ranks
ranks.saveAsTextFile("ranks")
