# Approaching machine learning 

* First set goal 
* Think of a measure of success
* Think of what a success would imply in the big picture (eg. revenue for company)
* Fine-tuning models not always most important: collecting more or different data, changing task formulation may be more meaningful.   
* Analysing mistakes done by model is often a great idea
* Consider how humans intervene: sometimes immediate decisions, or high levels of precision are needed. 

# From Prototype to production

* Python and scikit-learn is widely used, but not always best fit (cf. complex infrastructure) 
* Production teams usually work with Go, Scala, C++, Java to build robust, simple and scalable systems 
* Common practice is to _reimplement_ solution (found with Python or R by analytics team) in high-performance language inside a larger framework. 
* Article about: creating vs maintaining ML software in production at large scale. http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/43146.pdf   
 
# Testing production systems 

One mainly distinguishes between _offline testing_ and _online testing_.

* _offline testing_, is evaluating predictions on a test set collected beforehand.
* _online testing_, is done when being user-faced. Users interact with the learning system on a ongoing basis auch as a website, which allows one to employ _A/B testing_, selecting a portion of users when running algorithm A, evaluated against the other portion of users when running Algorithm B. One can further refine the strategy and match algorithms to segments of users in an optimal way. For further reading: http://shop.oreilly.com/product/0636920027393.do     
 
# Building own estimator

http://danielhnyk.cz/creating-your-own-estimator-scikit-learn/

# Where to go from here 

## Further reading 
* "Elements of Statistical Learning": https://www.amazon.com/Elements-Statistical-Learning-Prediction-Statistics/dp/0387952845
* "Machine Learning - An Algorithmic Perspective": https://www.amazon.com/Machine-Learning-Algorithmic-Perspective-Recognition/dp/1466583282
* "Pattern Recognition and Machine Learning": https://www.amazon.com/Pattern-Recognition-Learning-Information-Statistics/dp/0387310738
* "Machine Learning: A Probabilistic Perspective": https://www.amazon.com/Machine-Learning-Probabilistic-Perspective-Computation/dp/0262018020
* "Deep learning": http://www.deeplearningbook.org
* "Introduction to Information retrieval": http://nlp.stanford.edu/IR-book/pdf/irbookonlinereading.pdf

## Other packages or programming languages 

* for statistical modelling and inference: python package `statsmodel`
* `R`
* `vowpal rabbit` (often called `vw`): ML package written in C++ useful for large datasets.
* Scala library `mllib` built on top of `spark` for running ML algorithm on a cluster.  
* `PyMC`: probabilistic programming language which can be used in Python.
* `Stan`: probabilistic programming language which can be used from several languages including Python.

## Scaling to larger datasets

There are two ways to process large amounts of data on a budget (otherwise rent server from cloud provider):
* _out-of-core learning_, data is being read one sample or one chunk of samples at a time: http://scikit-learn.org/stable/modules/scaling_strategies.html 
* _parallelization over a cluster_, distributing data over multiple machines in a compute cluster, and let each computer process part of the data. Most popular platforms: `spark` built on top of `hadoop`, which - as already mentioned - includes `mllib` package. Otherwise the `vw` package provides distributed features.   
 
