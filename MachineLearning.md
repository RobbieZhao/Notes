Regression: Linear regression

Classification:

 - Logistic Regression
 - K nearest neighbors
 - Decision trees and random forests
 - Support Vector Machines
 - Neural networks and Deep learning

How to evaluate a classification algorithm?

 - Confusion matrix

### Linear regression

 - Underfit & Overfit
   - Underfit: accuracy for training data and testing data is low. This means the model is not complicated enough. Should add more terms
   -  Overfit: training set accuracy is high, but testing set accuracy is low. The model learned all the wiggles in the training set.

### Logistic Regression

How does it work?

 - Y values are 0 and 1
 - Run a linear regression, but this gives us values from -infinitiy to infinity. 
 - Use a function to smush the curve. 
 - A high value of slopes means there is a very narrow uncertainty region. It will transition very faster from 0 to 1

Limitations: 

 - The boundary curve is "straight" (a line, plane, or hyperplane). What if the true boundary is not straight?
 - Only deals with 2-class classification

### KNN

 - Parameters:
   - K: KNN is not sensitive to the choice of K
   - How to measure distance

### Decision tree

 - Overfit
   - can limit the tree depth
   - can set a minimum leaf size
 - Random forest
   - limit the set of attributes to vote, and generate a bunch of trees to vote

### Support vector machines

 - Pick the budget: total sum of costs we're tolerating
   - the less the budget, the smaller the margin, the line is more sensitive to the points close to the line, we risk overfitting
 - To produce curved decision boundaries: add one dimension and smush the points (by the kernel trick), and use a hyperplane to separate the points.

### K means clustering

 - Pick K first

### Hierarchical clustering

 - Dendrogram: Don't need to pick K

### PCA

 - Dimension reduction: Why?
   - compress data
   - reduce cost when training models
   - if we can reduce it to 2D or 3D, we can visualize it
### Selection of features

 - Chi-Squared Test
   - Divide the dataset by one feature. If the feature is a great predictor, we would expect to see different distributions of the two datasets.
### Measurements

 - K-fold cross validation
 - Bootstrapping
   - Select number of random samples from the dataset to make it look like we have done the experiment several times, and to get the true values of the estimates.
   - The random samples aren't independent, we don't get nice guarantees. (CLT requires data to be independent) 
 - Bagging (boostrapping for decision trees)
   - boostrapping to get a bunch of datasets; overfit a tree for each dataset; let all the trees vote

   


