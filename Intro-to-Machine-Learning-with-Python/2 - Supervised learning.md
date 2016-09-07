# k-Nearest Neighbor

For small datasets, good as baseline, easy to explain.

When using nearest neighbours, it's important to preprocess the data. It does not perform well on dataset with many features (hundreds or more). It does particularly badly for sparse datasets, aka datasets where most features are zero most of the time. While it is an easy-to-understand algorithm, it is not often used in practice due to being slow, and its inability to handle many features.  

## k-Neighbors Classification

## k -Neighbors Regression  

# Linear Models 

Good first-try algorithm, good for large datasets, good for very high-dimensional data.

For datasets with many features, linear models can be very powerful. In particular, if you have more features than training data points, any target can be perfectly modelled as a linear function. In low dimensions, linear models seem very restrictive, but gain in power for higher dimensions, in which case guarding against overfitting becomes increasingly important. 

There is lots of linear models. They are all differ in two ways: 
* loss function
* regularisation 

## Linear Regression (OLS)

## Ridge Regression 

## Lasso 

## Linear models for Classification

## Linear Models for multi-class classification 

# Naive Bayes Classifiers 

Only for classification. Faster than linear models. However the price to pay is that generalization performance slightly worse than linear models. 

Good for very large, high-dimensional sparse data, and relatively robust to parameters.

# Decision Trees 

Very fast, invariant to scaling of the data, can be visualised well and explained easily (by non-experts).    

Two ways to prevent overfitting: 
* pre-pruning: stopping the creation of the tree
* post-pruning (or just pruning): building the tree but then removing or collapsing nodes that contain little information. Ways to do this are, limiting the maximum depth of the tree, limiting maximum number of leaves, requiring a minimum number of points in a node to keep splitting it. 

The main downside is that even with with regularisation techniques, decision trees tend to overfit and provide poor generalisation bounds.    

# Ensembles of Decision Trees

## Random Forests 

Nearly always perform better than a single decision tree, very robust and powerful. Don't need scaling of data. Not good for very high-dimensional sparse data. 

Among most widely used algorithms. Often work well without heavy tuning of the parameters, and don't require scaling of the data. Random forests share all of the benefits of decision trees, while making up for some of their deficiencies.

Setting different random states can drastically change the model that is built, thus the more trees there are in the forest, the more robust it will be against the choice of random state. 

They don't perform well on very high-dimensional sparse data (such as text). They require more memory and are slower to train and to predict than linear models.

Important parameters: 
* `n_estimators`: number of trees. The larger, the more robust (reducing overfitting), but also need more memory and more time to train.     
* `max_features`: varies between `1` and `n_features`. 
High `max_features` means that the trees in the random forest will be quite similar thus will be able to fit the data easily, using the most distinctive features.  
Low `max_features` means that the trees in the random forest will be quite different, and thus each tree might need to be very deep in order to fit the data well.  
* `max_depth`: pre-pruning parameter
* `random_state`: important to set if you want to have reproducible results.
* `n_jobs`: number of cores to use. more cores result in linear speed-up. To use all cores set `n_jobs = -1`  

## Gradient Boosting 

gradient boosting works by building trees in serial manner, where each tree tries to correct the mistakes of the previous one. They often use very shallow trees. The main idea is to combine many simple models (_weak learners_). 

They frequently win machine learning competitions.  

Often slightly more accurate than random forest. Slower to train but faster to predict than random forest, and smaller in memory. Need more parameter tuning than random forest. 

Parameters:
* pre-pruning 
* `n_estimators`: number of trees in the ensemble. The higher, the higher the model complexity.  
* `learning_rate`: controls how strongly each tree tries to correct the mistakes of the previous trees. 
High `learning_rate` leads to complex models. 
Lower `learning_rate` means that more trees are needed to build a model of similar complexity. 

Common approach is to first use random forest. If it works well, but one wants to squeeze out the last percentages of accuracy from the machine learning model, moving to gradient boosting often helps. 

One often tries to fit `n_estimators` first depending on time and memory budget, and then search over different `learning_rate` 's.

As with most of tree-based models, it often does not work well on high-dimensional sparse data.

# Kernelized Support Vector Machines 

Powerful for medium-sized datasets of features with similar meaning. Needs scaling of data, sensitive to parameters. 

Parameters:

* regularisation parameter `C`: Large`C` results in a more complex model. 
Small `C` means very restricted model, where each data point can only have very restricted influence. Increasing `C`, allows points to have stronger influence on the model.   
* choice of kernel
* kernel-specific parameters: the most common one is `rbf` kernel, which has only one parameter, namely `gamma`, which is the inverse of the width of the Gaussian kernel. 
A small `gamma` means large radius for the Gaussian kernel, and many points are considered close-by, which is reflected by very smooth decision boundary, thus high model complexity.
Large `gamma` implies that the boundary will vary slowly, which yields to low model complexity.  


`gamma` and `C` both control the model complexity and should be adjusted together. 

SVMs are very sensitive to the settings of the parameters, and to the scaling of the data. They require all features to vary on similar scale. As SVMs require careful preprocessing and parameter tuning, most people don't use them but instead use tree-based models. Also they might be tricky to explain to non-experts. 

A common rescaling method to preprocess data for SVMs is `MinMaxScaler`. 

# Neural Networks 

Can build very complex models, in particular for large datasets. Sensitive to scaling of the data, and to the choice of parameters. Large models need a long time to train.  

Important parameters:
* Number of hidden layers
* Number of nodes in each hidden layer:  
* regularisation parameter `alpha`
* activation function 
* 'algorithm' parameter: optimisation procedure that explains how the model is being learned. Examples are `l-bfgs`, `adam` (most common, works well in most situations), `sgd`


The get an idea of the model complexity, it's a good idea to calculate the number of coefficients being learned.  
An important property to keep in mind is that NN's initial weights are set randomly, and this random initialisation affects the model that is being learned. 

One way to introspect what was learned is to look at the weights in the model.

_Advantages:_ able to capture information in large datasets and build complex models. Given enough time, data, parameter tuning, NN often beat other machine learning algorithms. 

_Disadvantages:_ Often take a long time to train. Require careful preprocessing, similarly to SVMs, work best with 'homogenous' data. Ideally, all input features should have a mean of zero and variance of one. 
  
Common procedure: Start with one or two layers, then increase the network so that it is large enough to overfit (making sure that the task can actually be learned), then shrink the network or increase `alpha` to add some regularisation (cf. skinny jeans analogy) 


# Uncertainty estimates from classifiers    

# General recipe 

Start with: 
* linear model  
* naive Bayes 
* nearest neighbours

See how far you can get. Continue with:
* random forest
* gradient boosting
* SVM
* neural networks  
