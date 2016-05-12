# RPHash: Scalable Big Data Clustering by Random Projection Hashing.

This project is developing scalable techniques for high-dimensional data clustering using
approximate methods.  In particular, the RPHash algorithm combines (i) Random Projection (RP), (ii)
Locality Sensitive Hashing (LSH), and (iii) count-min sketch for clustering high-dimensional data.
The algorithm can be structured as a two-pass clustering operation or it can be deployed as a method
for clustering streaming data (StreamingRPHash).  RPHash is able to perform clustering at a rate
much faster than traditional clustering algorithms and provides clustering results that are on par
with K-Means.

The RPHash algorithm is easily parallelized and has nearly linear speedup on a single node.  It is
also possible to deploy RPHash in a map-reduce framework for distributed clustering.  The
distributed clustering can be performed on a single high volume data source or it can be performed
on a collection of distributed datasets.  Furthermore, the ability for clustering distributed data
sets is achieved without requiring the exchange of data between the distributed databases.  The
clustering of secure, distributed datasets is achieved by sending the same random seeds to the
various instances of RPHash so that the random projection and LSH perform the same transforms to the
source vectors.  The distributed instances of RPHash then partition the local vectors using centroid
hash ids that are then exchanged to identify the global centroids.  The global centroids are then
sent sent back to the distributed instances of RPHash for a final partitioning step.  Only hash ids
of the candidate centroids are exchanged between the nodes of the cluster.  Thus, since the
probability of reproducing the original source data from the hash ids is quite low, the data is
secure.  Hence RPHash can serve to provide a clustering solution from a distributed set of databases
where the data within them must remain secure.

The RPHash project has

* [rphash-java:](https://github.com/wilseypa/rphash-java) This is the main RPHash repository that
  contains many configuration options.  While there are many configuration options, the principle
  choices are:
  ..* The RP step: full JL or DB Friendly; number of dimensions to reduce to; and number of
  multi-probe operations
  ..* Specific LSH algorithms: Leech, Spherical (multiple configuration settings), E8, and p-space
  (Euclidean, Manhattan, or .5 fractional)

* [rphash-spark:] Source code to embed the rphash-java runtime into the Spark map-reduce framework.

* [rphash-golang:](https://github.com/wilseypa/rphash-golang) A golang implementation of the
  StreamingRPHash algorithm from the rphash-java repository.  Implementing DB Friendly with three
  multi-probe steps with a Spherical LSH step.  This implementation includes a count-min sketch for
  partitioning the resulting LSH values and computing an average centroid for each partition.

*IGNORE THIS FOR NOW* See the project webpages at http://wilseypa.github.io/rphash
