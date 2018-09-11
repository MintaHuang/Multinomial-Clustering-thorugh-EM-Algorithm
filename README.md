# Multinomial-Clustering-thorugh-EM-Algorithm

### In this exercise, we will apply the EM algorithm and a finite mixture of multinomial distributions to the image segmentation problem. One way to approach image segmentation is to extract a suitable set of features from the image and apply a clustering algorithm to them. The clusters output by the algorithm can then be regarded as the image segments. The features we will use are histograms drawn from small regions in the image.

### Histogram clustering: The term histogram clustering refers to grouping methods whose input features are histograms. A histogram can be regarded as a vector; if all input histograms have the same number of bins d, a set of input histograms can be regarded as a set of vectors in Rd. We can therefore perform a simple histogram clustering by running a k-means algorithm on this set of vectors. The method we will implement in this problem is slightly more sophisticated: Since histograms are represented by multinomial distributions, we describe the clustering problem by a finite mixture of multinomial distributions, which we estimate with the EM algorithm.

### The EM algorithm for multinomial mixtures. The input of the algorithm is:
• A matrix of histograms, denoted H, which contains one histogram vector in each row. Each column corresponds to a histogram bin.
• An integer K which specifies the number of clusters.
• A threshold parameter ⌧.
### The variables we need are:
• The input histograms. We denote the histogram vectors by H1 , ..., Hn .
• The centroids t1 , ..., tK . These are Rd vectors (just like the input features). Each centroid is the parameter vector of a multinomial distribution and can be regarded as the center of a cluster; they are computed as the weighted averages of all features assigned to the cluster.
• The assignment probabilities a1,...,an. Each of the vectors ai is of length K, i. e. contains one entry for each cluster k. The entry aik specifies the probability of feature i to be assigned to cluster k. The matrix which contains the vectors ai in its rows will be denoted P.

### The algorithm iterates between the computation of the assignment probabilities ai and adjusting the cluster centroids tk.

### The algorithm:
1. Choose K of the histograms at random and normalize each. These are our initial centroids t1, ..., tK . 
2. Iterate:
(a) E-step: Compute the components of each ai, the assignment probabilities aik, as follows:
 ik := exp0@XHij log(tkj)1A
j aik := Pck ik
Kl=1 cl il
Note that  ik is the multinomial probability of Hi with parameters tk, up to the multinomial coe cient
n! , which cancels out in the computations of aik. Hi1 !···Hid !
  2
(b) M-step: Compute new mixture weights ck and class centroids tk as
ck =
Xn
Pni=1 aik n
 bk =
tk = Pbk
i=1
aikHi
 dj=1 bkj
(c) Compute a measure of the change of assignments during the current iteration:
  := kA   Aoldk ,
where A is the assignment matrix (with entries aik), Aold denotes assignment matrix in the previous step, and k . k is the matrix 1-norm (the largest sum of column absolute values). This is implemented in R as norm(.,"O").
3. Terminate the iteration when   < ⌧.
4. Turn the soft assignments into a vector m of hard assignments by computing, for i = 1, ..., n,
mi := arg max aik , k=1,...,K
i. e. the index k of the cluster for which the assignment probability aik is maximal.
The histogram data: The histograms we use have been extracted from an image by the following procedure:
1. Select a subset of pixels, called the sites, at which we will draw a histogram. Usually, this is done by selecting the pixels at the nodes of an equidistant grid. (For example, a 2-by-2 grid means that we select every second pixel in every second row as a site.)
2. Place a rectangle of fixed radius around the site pixel.
3. Select all pixels within the rectangle and sort their intensity values into a histogram.
The data we provide you with was drawn from the 800x800 grayscale image shown below (left):
The image is a radar image; more specifically, it was taken using a technique called synthetic aperture radar (or SAR). This type of image is well-suited for segmentation by histogram clustering, because the local intensity dis- tributions provide distinctive information about the segments. The image on the right is an example segmentation using K = 3 clusters, computed with the algorithm described above.
  3

The histograms were drawn at the nodes of a 4-by-4 pixel grid. Since the image has 800 ⇥ 800 pixels, there are 200 ⇥ 200 = 40000 histograms. Each was drawn within a rectangle of edge length 11 pixels, so each histogram contains 11 ⇥ 11 = 121 values.
