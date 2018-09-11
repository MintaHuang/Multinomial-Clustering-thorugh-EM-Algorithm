# Multinomial-Clustering-thorugh-EM-Algorithm

In this exercise, we will apply the EM algorithm and a finite mixture of multinomial distributions to the image segmentation problem. One way to approach image segmentation is to extract a suitable set of features from the image and apply a clustering algorithm to them. The clusters output by the algorithm can then be regarded as the image segments. The features we will use are histograms drawn from small regions in the image.

Histogram clustering: The term histogram clustering refers to grouping methods whose input features are histograms. A histogram can be regarded as a vector; if all input histograms have the same number of bins d, a set of input histograms can be regarded as a set of vectors in Rd. We can therefore perform a simple histogram clustering by running a k-means algorithm on this set of vectors. The method we will implement in this problem is slightly more sophisticated: Since histograms are represented by multinomial distributions, we describe the clustering problem by a finite mixture of multinomial distributions, which we estimate with the EM algorithm.

### The EM algorithm for multinomial mixtures. The input of the algorithm is:
• A matrix of histograms, denoted H, which contains one histogram vector in each row. Each column corresponds to a histogram bin.

• An integer K which specifies the number of clusters.

• A threshold parameter ⌧.
### The variables we need are:
• The input histograms. We denote the histogram vectors by H1 , ..., Hn .

• The centroids t1 , ..., tK . These are Rd vectors (just like the input features). Each centroid is the parameter vector of a multinomial distribution and can be regarded as the center of a cluster; they are computed as the weighted averages of all features assigned to the cluster.

• The assignment probabilities a1,...,an. Each of the vectors ai is of length K, i. e. contains one entry for each cluster k. The entry aik specifies the probability of feature i to be assigned to cluster k. The matrix which contains the vectors ai in its rows will be denoted P.
