# Machine Learning in Python
In this lecture, we will be introducing some concepts and tools for machine learning in Python. Because of the many packages for data science and mathematics (eg. numpy, scipy, matplotlib, pandas), and a variety of machine learning packages ranging from simple (scikit-learn) to very low-level (theano), Python is one of the most popular languages for machine learning.
It is important to emphasize that these packages are huge, and even skilled data scientists do not commit them to memory in entirety. More important is the ability to recognize what tools are most suitable for a given situation and to find the appropriate documentation.

We will be working primarily with the scikit-learn package, which is simple, easy to use, and contains many popular machine learning algorithms out of the box. First, download scikit-learn using either the `pip` or `pip3` command:
```
pip install scikit-learn
```
To use scikit-learn in Python, simply import it. Although this package can be used alone, it is most commonly used with numpy and. In order to visualize results, we will also be using matplotlib.
```python
>> import numpy as np
>> import matplotlib.pyplot as plt
>> import sklearn as sk
```

## Scikit-learn Patterns

The scikit-learn package has two main patterns for working with data. Operations that do not require memory, like scaling transformations or loading data, are used as functions. On the other hand, operations that require memory or have parameters are stored as objects. Machine learning models are stored in this way, and are used in a two-step process. For instance, to train a linear regression model on toy data:
```
>> from sklearn.linear_model import LinearRegression
>> X = np.array([[1, 1], [1, 2], [2, 2], [2, 3]])
>> y = np.dot(X, np.array([1, 2])) + 3
>> reg = LinearRegression().fit(X, y)
>> reg.coef_, reg.intercept_
array([1., 2.]), 3.
>> reg.predict(np.array([[3, 5]]))
array([16.])
```
The `fit` step tunes internal parameters or stores relevant metadata. Here, it learns coefficients for the linear predictor (here `np.array([1., 2.])` and `3.`). The `predict` step then uses these coefficients to predict the label for a new example (here, the linear regression model predicts `16` for the example `(3,5)`).

The steps for machine learning are:
 1. preprocessing: transforming data into a usable format
 2. training: learning appropriate parameters for the prediction task
 3. model selection: evaluating the trained model and choosing good hyperparameters
We will walk through training a model to predict species using each of these steps.

## The Data

Let's first discuss the data that we will be using, in order to motivate the different tasks that we will be performing.
We will be using the Iris dataset, which contains measurements of flowers from three subspecies of the iris plant. There are 150 examples total, split evenly among the subspecies. The data may be downloaded in CSV form [here](https://archive.ics.uci.edu/ml/datasets/iris), but scikit-learn has a custom loader for this dataset. Each example has four attributes: sepal length, sepal width, petal length, and petal width.
```python
from sklearn import datasets

>> iris = datasets.load_iris()
>> X, y = iris.data, iris.target
```
Here, `iris.data` is a two-dimensional 150x4 numpy array containing measurements from each flower, and `iris.target` is a one-dimensional array containing which species each flower comes from. 

Given a dataset, there are multiple interesting tasks that we can perform using this data. Three of the main types of tasks are:

 - Supervised: learning to predict some attribute based on labeled training data. For example, predicting the subspecies of iris based on measurements.
 - Unsupervised: learning a function that describes the internal structure of unlabeled data. For example, grouping measurements into clusters.
 - Semisupervised: a hybrid of supervised and unsupervised,learning, learns to predict some attribute using some labeled and some unlabeled training data.

For the sake of brevity, we will only talk about supervised learning in this prelecture.

## Preprocessing

Although the Iris dataset is well-behaved and does not have any missing attributes, it is common to have some attributes which are correlated with one another, have vastly different scales, or are missing some entries. For example, some responses from a user survey might be missing fields. Running machine learning algorithms without first addressing these issues will lead to unnecessary frustration later on.
The whitening and normalization transformations manipulate the data to have zero mean and unitary covariance. Since many machine learning algorithms depend strongly upon the magnitude of data features, normalization can lead to improved performance.
In scikit-learn, whitening is very easy using the `sklearn.preprocessing` module:
```
>> X = iris.data
>> np.mean(iris.data, axis=0)
>> np.mean(X, axis=0)
array([5.84333333, 3.05733333, 3.758     , 1.19933333])
>> X_norm = sklearn.preprocessing.scale(X)
>> np.mean(X_norm, axis=0)
array([-1.69031455e-15, -1.84297022e-15, -1.69864123e-15, -1.40924309e-15])
```

Another commonly-used preprocessing functions is `preprocessing.OneHotEncoder`, which transforms a categorical integer-valued variable into a one-hot vector. For instance, the dataset represents Iris Setosa as 0, Iris Versicolor as 1, and Iris Virginica as 2. Note that unlike scaling, the OneHotEncoder needs memory (ie. which integer maps to which one-hot vector). Scikit-learn represents this encoder as a OneHotEncoder object.

## Training

Supervised learning tasks are tasks where visible (training) data are labeled, and we would like to be able to predict these labels for unseen (test) data. For our Iris dataset, we would like to predict the species of iris given flower measurements.
Supervised learning tasks are divided into two types: *regression*, where the desired output is a real-valued quantity (eg. predicting the petal size from species and sepal size), and *classification*, where the desired output is a named label (eg. predicting species).

### Regression

Let's first look at regression. For many real-world applications, predicting a missing real-valued quantity is useful. As an example, the insurance industry might be interested in predicting the risk (in dollars) associated with issuing a particular policy. For the iris dataset, we will first try to predict petal width from petal length using *linear regression*, which learns coefficients for a linear function (ie. a line or hyperplane) that best fits the data. 
```python
>> petal_width = X[:, 2].reshape(-1, 1) # features should be a 2-d array
>> petal_length = X[:, 3]               # targets should be a 1-d array
>> reg = LinearRegression()
>> reg.fit(petal_width, petal_length)
>> reg.coef_, reg.intercept_
array([0.41575542]), -0.3630755213190291
```
As expected, there is a positive correlation between petal width and petal length. Plotting the learned regressor, we see that the model fits well.

![linear regression](https://github.com/CS196Illinois/lecture-notes-sp19/blob/master/assets/iris-1.png).

Note that especially for more complex problems, we want to use as many features as possible. To use sepal width, sepal height, and petal width to predict, simply replace `X[:, 2]` with `X[:, :3]`.

### Classification

Next, we get to the task of predicting species from flower measurements. We cannot simply use linear regression, since this task requires that the model return one of three discrete labels Iris setosa, Iris versicolor, or Iris virginica. Instead of trying to choose between three labels, let's first consider a simpler problem where the model picks between two labels: whether or not a flower is Iris setosa.

For this problem, we'll use a different class of model called logistic regression. With a bit of hand-waving, logistic regression is similar to linear regression, except for the function that is fit to the data.

![logistic function](https://upload.wikimedia.org/wikipedia/commons/thumb/8/88/Logistic-curve.svg/320px-Logistic-curve.svg.png)

Note that this logistic function is exactly what we want in a binary classification problem: it returns values from 0 (corresponding to the binary answer "no") to 1 (corresponding to the binary answer "yes"). Intermediate values can also be interpreted as various degrees of confidence in a decision.

Despite the more complex function class, training and using a logistic regression model is still simple in scikit-learn:
```python
>> setosa = (y == 0) # setosa is encoded as class 0
>> reg = LogisticRegression(solver="liblinear", multi_class="auto")
>> reg.fit(X, setosa)
>> reg.predict(np.array([[5.1, 3.5, 1.4, 0.2]])) # setosa example from the dataset
array([ True])
>> reg.predict(np.array([[5.9, 3.0, 5.1, 1.8]])) # virginica example from the dataset
array([False])
```

We can also plot out the model's predictions for every example in the dataset:
```python
>> y_hat = reg.predict(X)
>> plt.scatter(X[:,2], X[:,3], c=y_hat, cmap="viridis")
>> plt.show()
```

![logistic regression](https://github.com/CS196Illinois/lecture-notes-sp19/blob/master/assets/iris-2.png).

At this point, we can now predict whether or not a flower comes from a particular species. However, we can easily extend this to *multinomial*, or multi-class classification, by having one classifier for each species, then picking the one with the highest confidence. By default, scikit-learn supports multinomial classification, and is invoked in exactly the same way.
```python
>> reg = LogisticRegression(solver="liblinear", multi_class="auto")
>> reg.fit(X, y)
>> reg.predict(np.array([[5.1, 3.5, 1.4, 0.2]])) # setosa example from the dataset
array([0])
>> reg.predict(np.array([[5.9, 3.0, 5.1, 1.8]])) # virginica example from the dataset
array([2])
>> y_hat = reg.predict(X)
>> plt.scatter(X[:,2], X[:,3], c=y_hat, cmap="viridis")
>> plt.show()
```

![multi-class logistic regression](https://github.com/CS196Illinois/lecture-notes-sp19/blob/master/assets/iris-3.png).

## Model Selection

Model selection is the principled process of choosing an appropriate model class and hyperparameters. From a cursory glance at the scikit-learn documentation, there are a variety of models for any given machine learning task.
Therefore, it is important to have a way of evaluating which models are most suitable for a given problem. We introduce two concepts: evaluation metrics and the train-validation-test split.

### Evaluation Metrics

Our previous process for training linear and logistic regressors has a few flaws. First of all, we simply accepted that the trained models worked acceptably. This is indeed the case for the Iris dataset, but there are more complex problems for which linear classifiers are unsuitable. The fundamental question is: _"How do we measure how good a model is at a prediction task?"_ Several evaluation metrics are available. The simplest is *accuracy*, which measures how many examples are classified correctly. We can evaluate the accuracy of our logistic regression classifier easily using scikit-learn:
```python
>> y_hat = reg.predict(X)
>> sklearn.metrics.accuracy_score(y, y_hat)
0.96
```
We see that indeed, the logistic regression model predicts species well. There are other problems where logistic regression is unsuitable. On those problems, we will observe a much lower accuracy score.
```python
>> x = np.linspace(-5, 5, 20)
>> class0 = np.vstack((x,x**2 - 12)).T
>> class1 = np.vstack((x,x**2 - 14)).T
>> X = np.vstack((class0, class1))
>> X.shape
(40, 2)
>> y = np.hstack((np.zeros(20), np.ones(20)))
>> y.shape
(40,)
>> reg = LogisticRegression(solver="liblinear", multi_class="auto")
>> reg.fit(X, y)
>> y_hat = reg.predict(X)
>> sklearn.metrics.accuracy_score(y, y_hat)
0.5
```
Note that the logistic regression classifier has a low accuracy score, which means that logistic regression is a poor choice for this problem. By plotting the data and the classifier, we visually confirm this intuition.

![logistic regression failure case]((https://github.com/CS196Illinois/lecture-notes-sp19/blob/master/assets/iris-4.png).

A more thorough explanation of why some models are unsuitable for some problems will be given during lecture on Tuesday.

### Train-Test Split

Another bad practice from the previous demonstration was that we trained (and evaluated) on the entire dataset. In the real world, training and testing in this way is unfair, since certain models are capable of memorizing all of the points on which it was trained. Running evaluation metrics using data the model has already seen, therefore, does not give a fair indication of how well the model will perform on unseen data.

The difference between how well a model performs on examples that it has seen versus examples that it has not seen is called *generalization*. In order to fairly evaluate a model, it is important to run these metrics on an unseen portion of the data, known as the test set. Standard practice is to randomly select 10 percent of the data as the test set, and train on the other 90 percent. 
