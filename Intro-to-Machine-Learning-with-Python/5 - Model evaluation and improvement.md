# Cross- validation 

For _k-fold cross validation_, one splits the dataset into _k_ roughly equally sized sets (_k_ to be specified), also called _folds_, then the sequence of models is trained on the whole dataset with one fold removed, and tested on the removed fold. For each model one computes and stores the accuracy, and keeps going until all folds have been selected once. One then computes the arithmetic mean of all the accuracies. The choice of a specific _fold_, is called a _split_. 

It's pretty interesting to see whether the choices of splits produce a high variation in accuracies, which would imply that the accuracy of the model is very dependant on the particular folds used for training (but could of course also be a consequence of the dataset being too small). Having multiple splits provides some information about how sensitive the model(s) are to the selection of the training set. 

`cross_val_score(model, data, labels)` is scikit-learn function from the `model_selection` module, which returns an array of accuracies of three-fold cross validation (by default) for each split. One can change the number of folds by setting the parameter `cv`. 

The only drawback of cross-validation is increase in computational cost. There are more drawbacks which we will see in the next section. 
   
# Stratified Cross-validation 

Imagine one runs three-fold cross-validation for classification algorithm, where the first fold only has members from class 1, the second fold only from class 2, and the third fold only from class 3. Then the average accuracy would be zero, but it is obvious that we can do much better than that. 

We notice that we need to have each fold to contain as much diverse information as possible, i.e. the proportions between the classes need to be the same for each fold, and thus the same as in the overall dataset. That's the idea of _stratified k-fold cross-validation_. As you probably guess, it gives much more reliable estimates of generalisation performance. 

For regression, one uses the standard k-fold cross-validation by default, although one could totally segment the labels into bins and look at the proportion between the number of elements of each bin.   



# More control over cross-validation 

# Grid Search 



# Evaluation metrics and scoring 

# Model selection 
