Often, unsupervised learning is used in a exploratory setting, when the data scientist wants to understand or visualize the data better. 

Another common way to use unsupervised learning is as a preprocessing step for supervised learning. Better representations of the data can improve accuracy, time and memory consumption.  

It's hard to tell whether an unsupervised learning algorithm "did well".

Types of unsupervised learning: 

* _unsupervised transformations_, is creation of a new representation of the dataset, which is easier to understand and visualise. An example is _dimensionality reduction_, which takes high-dimensional data and finds a way to represent it in fewer dimensions summarising the main characteristics. Another example is _topic extraction_ in text documents, which tries to find unknown topics that are talked about in each document. 
   
* _clustering algorithms_, is the partitioning of the data into distinct groups of similar items or characteristics.    

#  Preprocessing and scaling 

There are four common ways to transform the data:

* `StandardScaler`: each feature being reduced to mean zero, and variance one. However this does not ensure any particular minimum and maximum values for the features.

* `RobustScaler`: similar to `StandardScaler`, uses median and quantiles, instead of mean and variance. It tends to ignore points that are very different from the rest, aka _outliers_.

* `MinMaxScaler`: shifts data so that all features are between 0 and 1.

* `Normalizer`: scales each data point so that the feature vector has euclidean norm 1. Thus every data point is scaled by a different number. You can see it as every vector being pulled back onto the unit circle, thus preserving only the direction of the vector. Mainly used when only direction matters.    

it goes without saying that one should apply the same transformation to test as well as training set. 


# Dimensionality reduction, Feature extraction and Manifold learning

## PCA (Principal Component Analysis)

Rotates the dataset so that features will be uncorrelated using the following steps: 
* First, pick the direction of maximal variance (direction containing most of information)
* Then, pick the direction of maximal variance while being orthogonal to the first direction. 

The directions found are called _principal components_.

One can use PCA for dimensionality reduction and feature extraction. One way to look at PCA is some sort of reconstruction of the original data using only some components. The disadvantage is that it is often hard to interpret the found directions in a meaningful way.

## NMF (Non-negative Matrix Factorization) 

Works similar to PCA, but one wants components and coefficients to be non-negative. Thus this method can only be applied to data where each feature is nonnegative.  It seeks to decompose data into a non-negative weighted sum. This helpful for data that is created as an addition of several independent sources, such as audio tracks, speech. NMF can identify the original components that make up the combined data.  

## Manifold learning with t-SNE

As the example of the labeled faces in the wild highlights, PCA limits its usefulness when there are more complex mappings at play. In this case _manifold learning_ provides better visualisation. Manifold learning is useful for exploratory data analysis but rarely used if the final goal is supervised learning as it doesn't allow transformation of the newly produced data. The most common manifold learning algorithm is called _t-SNE_. 

_t-SNE_ works as follows:
* starts with random 2-dim representation of the data. 
* then, pushes data closer together that are close in the original dataset, and pushes points far apart for points that are far in the original dataset (while putting more emphasis on points that are close together, "it tries to preserve neighbourhoods of points").

Tuning parameters: `perplexity` and `early_exaggeration`, usually the effects are minor and the default setting works well most of the time. 

  
# Clustering 

## k-Means clustering 

Starts with randomly choosing `n_clusters` cluster centres, then alternating between the following two steps:

* assign each data point to closest cluster centre.
* update cluster centre to the mean of the data points that are assigned to it.
 
An interesting perspective of k-Means, is to view it as a decomposition method, where each point is represented by a single component only, which is given by the cluster centre. This representation is called _vector quantization_. One can for example use many more clusters than input dimensions and then use a linear model to separate the data. 

_Advantages_: 

* easy to understand and implement 
* runs quickly 
* scales easily 

_Disadvantages_:

* relies on random initialization 
* requires to specify the number of clusters 
* restrictive assumptions made on the shape of clusters. each cluster is a convex hull, thus k-Means can only capture convex shapes, performs poorly on complex shapes such as `two_moon` dataset.
* treats every direction the same: it always draws the boundary between clusters to be in the middle between cluster centres, sometimes leads to surprising results, especially when not all directions are of same importance. 


## Agglomerative clustering 

Refers to collection of clustering algorithms built on the same principle:
* First, declare each point being its own cluster.
* Then, merge the two most similar clusters until some stopping criterion (usually the number of clusters).

The way agglomerative clustering algorithms differ is the way they measure "similarity" (_linkage_ criterion):
* _ward_, default choice. Picks two clusters to merge, if when merged the variance within clusters increases the least. 
* _average_, merges two clusters that have smallest average distance between all their points. 
* _complete_, merges two clusters that have smallest maximum distance between their points. 

_Ward_  works on most datasets, whereas _average_ or _complete_ might work better if clusters have very dissimilar number of members.  

## DBSCAN 

stands for "Density-based spatial clustering of applications with noise". It identifies points located in "crowded" regions of the feature space (referred to as _dense_ regions). It relies on the idea that clusters from dense regions in the data (whose points are called _core samples_), separated by regions that are rather empty. 

DBSCAN has two parameters `min_samples` and `eps`, and works as follows:
* picks a point to start with.
* if there are at least `min_samples` within distance of `eps` to the given data point, then the data point is declared _core sample_, otherwise it is declared _noise_. 
* If the original point was a _core sample_, every point within `eps` is assigned to the same cluster (if not already done) and checked whether it is a `core_sample` itself. If so, one continues and the cluster grows. If not another yet unvisited point is picked, and the procedure is repeated again. 

In the end there will be core points, points that are within `eps` distance of the core points (boundary points ), and noise. When running multiple times, the clustering of the core points is always the same, however a boundary point might be neighbour to core samples of more than one cluster. Thus the cluster membership depends on the order in which points are visited. 

Increasing `eps` leads to bigger and fewer clusters. Increasing `min_samples` leads to fewer core points, and more points labeled as noise. The former is the more important parameter. 

In contrast to k-Means DBSCAN doesnt require to specify the number of clusters explicitly, but only requires `eps` to be specified which seems to be easier especially after a rescaling such as `StandardScaler` or `MinMaxScaler`. 

## Evaluation of clustering algorithms 

    
