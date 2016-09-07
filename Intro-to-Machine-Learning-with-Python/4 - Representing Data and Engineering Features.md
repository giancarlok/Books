There is _continuous features_ and _categorical features_ (also known as _discrete features_). Regardless of the type, the way you represent your data can have tremendous effect on the performance of your machine learning algorithm, more than choosing the exact parameters. Examples from previous chapters are: 
* _augmenting_ data with additional features
* _rescaling_ your features. 
The question of how to best represent your features is called _feature engineering_. 

# Categorical variables 

The most common way to represent categorical variables is using _one-hot-encoding_ or _one-out-of-N_ encoding, all known as _dummy variables_. Dummy variables replace categorical variable with one or more new features that can have the values 0 or 1. There are two ways to accomplish this: one with `pandas` and the other one with `scikit-learn`.   

# Binning, Discretisation, Linear Models and Trees

The power of a feature representation largely depends on the model that is being used. Let's look at linear models and tree-based models: 

* Linear models can only model linear relationships. One way to make linear models more powerful on continuous data is to use _binning_ (or _discretization_) of the feature to split it up into multiple features as follows: 

`blurb= np.linspace(-3,3,11)` creates 10 equally spaced bins in the interval [-3,3].
`which_bin = np.digitize(X, bins=blurb)` records for each datapoint which bin it falls into.
`from sklearn.preprocessing import OneHotEncoder` 
`encoder.fit(which_bin)` finds the unique values that appear in `which_bin`.
`X_binned = encoder.transform(which_bin)`

Usually linear models benefit greatly from binning, whereas the performance of tree-based model decreases usually. 

* 
 

# Interactions and Polynomials 

# Univariate Non-linear transformations

# Automatic Feature Selection

# Utilizing Expert Knowledge   
