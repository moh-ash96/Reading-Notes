# Data Science and Machine Learning

## Bird's Eye View

### What is machine learning

Machine learning is the practice of teaching computers how to learn patterns from data, often decisions and predictions.

### Terminology

* **Model** - a set of patterns learned fro data.

* **Algorithm** - a specific ML process used to train a model.

* **Training data** - the dataset used from which the algorithm learns the model.

* **Test data** - a new dataset for reliably evaluating model performance.

* **Features** - Variables (columns) in the dataset used to train the model.

* **Target variable** - A specific variable you're trying to predict.

* **Observance** - Data points (rows) in the dataset.

### Machine Learning Tasks

#### Supervised Learning 

It includes tasks for "labled" data.

* It is used for an advanced predictive modeling.

* Each observation must be labeled with the correct answer.

* Only with the previous labeling you build a predictive model, because you should tel the algorithm whats is correct.

* **Regression** - it is the task of modeling continuous target variables.

* **Classification** - the task for modeling categorical target variables.

#### Unsupervised Learning

It includes tasks for unlabeled data.

* It is used either as a form of automated data analysis or automated signal extraction.

* Unlabeled data has no predetermined correct answer.

* You'll allow the algorithm to directly learn patterns from the data.

* **Clustering** is the most common unsupervised learning task, and it's for finding groups within your data.

### Three elements of great machine learning

1. A skilled chef (Human guidance) - First, even though we are "teaching computers to learn on their own," human guidance plays a huge role.

2. Fresh ingredients (Clean relative data) - The second essential element is the quality of your data.

3. Don't overcook it (Avoid overfitting) - An overfit model has "memorized" the noise in the training set, instead of learning the true underlying patterns.

### The Blueprint

1. Exploratory Analysis - First, "get to know" the data. This step should be quick, efficient, and decisive.

2. Data Cleaning - Then, clean your data to avoid many common pitfalls. Better data beats fancier algorithms.

3. Feature Engineering - Next, help your algorithms "focus" on what's important by creating new features.

4. Algorithm Selection - Choose the best, most appropriate algorithms without wasting your time.

5. Model Training - Finally, train your models. This step is pretty formulaic once you've done the first 4.

![Successful model](https://elitedatascience.com/wp-content/uploads/2018/05/What-Goes-Into-a-Successful-Model.jpg)

## Exploratory Analysis

### Why Explore dataset upfront?

* It gives you valuable hints for data cleaning.

* It help you think of ideas for feature engineering.

* You'll feel the database, which will help you communicate results and deliver greater impact.

### Steps for dataset Explore

#### Start with basics

that are the answers of the following questions:

1. How many observations do I have?

2. How many features?
3. What are the data types of my features? Are they numeric? Categorical?

4. Do I have a target variable?

#### Plot Numerical Distributions

It can be very enlightening to plot the distributions of your numeric features, here we should use histograms.
You should look out for:

* Distributions that are unexpected.

* Potential outliers that don't make sense.

* Features that should be binary (i.e. "wannabe indicator variables").

* Boundaries that don't make sense.

* Potential measurement errors.

#### Plot Categorical Distributions

You can use bar plots in this situation.

In particular, you'll want to look out for sparse classes, which are classes that have a very small number of observations, They tend to be problematic when building models.

* In the best case, they don't influence the model much.

* In the worse case, they can cause the model to be overfit.

Therefore, we recommend making a note to combine or reassign some of these classes later.

#### Plot Segmentation

Segmentation is a powerful way to observe the relationship between categorical features and numeric features.
Box plots allow you to do so.

#### Study Correlations

Correlations allow you to look at the relationships between numeric features and other numeric features, it is a value between -1 and 1 that represents how closely two features move in unison.
The value will reflect the following:

* Positive correlation means that as one feature increases, the other increases.
* Negative correlation means that as one feature increases, the other decreases.

* Correlations near -1 or 1 indicate a strong relationship.
* Those closer to 0 indicate a weak relationship.
* 0 indicates no relationship.

## Data Cleaning

Better data beats fancier algorithms, in other words, Garbage in gets you garbage out.
If you have a properly cleaned dataset, even simple algorithms can learn impressive insights from the data, different types of data will require different types of cleaning.

### Remove Unwanted observations

This includes, **Duplicate** and **Irrelevant** Observations

#### Duplicate Observations

They most frequently arise during data collection, such when,

* Combine datasets from multiple places.
* Scrape data.
* Receive data from clients/other departments.

#### Irrelevant Observations

They are those that don’t actually fit the specific problem that you’re trying to solve.

### Fix Structural Errors

They are those that arise during measurement, data transfer, or other types poor housekeeping.

These errors include:

* Typos.
* inconsistent capitalization.
* mislabeled classes.

### Filter Unwanted Outliers

Outliers can cause problems with certain types of models.
In general, if you have a legitimate reason to remove an outlier, it will help your model’s performance, but you must have a good reason for removing an outlier, such as suspicious measurements that are unlikely to be real data.

### Handle Missing Data

You cannot simply ignore missing values in your dataset. You must handle them in some way for the very practical reason that most algorithms do not accept missing values.

There are two common ways to deal with missing data, these are:

1. **Dropping** observations that have missing values.
2. **Imputing** the missing values based on other observations.

Dropping missing values is sub-optimal because when you drop observations, you drop information.

* The fact that the value was missing may be informative in itself.
* Plus, in the real world, you often need to make predictions on new data even if some of the features are missing.

Imputing missing values is sub-optimal because the value was originally missing but you filled it in, which always leads to a loss in information, no matter how sophisticated your imputation method is.
You should tell your algorithm if a value was missing and even if you build a model to impute your values, you’re not adding any real information.
The best ways to deal with missing data:

#### Missing Categorical data

The best way to handle missing data for categorical features is to simply label them as ’Missing’, ane here you are essentially adding a new class for the feature, and this tells the algorithm that the value was missing, and also gets around the technical requirement for no missing values.

#### Missing numeric data

For missing numeric data, you should flag and fill the values.

* Flag the observation with an indicator variable of missingness.
* Then, fill the original missing value with 0 just to meet the technical requirement of no missing values.

By using this technique of flagging and filling, you are essentially allowing the algorithm to estimate the optimal constant for missingness, instead of just filling it in with the mean.

## Feature Engineering

Feature engineering is about creating new input features from your existing ones.

### Infuse Domain Logic

Here you can engineer informative features according to your or others' expertise about domain, by thinking about information you might need to isolate.

### Create Interaction Features

You can look at each pair of features and ask yourself, "could I combine this information in any way that might be even more useful?"

### Combine Sparse Classes

**Sparse classes** (in categorical features) are those that have very few total observations. They can be problematic for certain machine learning algorithms, causing models to be overfit.

* There's no formal rule of how many each class needs.
* It also depends on the size of your dataset and the number of other features you have.
* As a rule of thumb, we recommend combining classes until each one has at least ~50 observations.

So at first, we group similar classes, and thus we have fewer unique classes but each one has more observations.

### Add Dummy Variables

**Dummy variables** are a set of binary (0 or 1) variables that each represent a single class from a categorical feature.

Most machine learning algorithms cannot directly handle categorical features, specifically, they cannot handle text values therefore, we need to create dummy variables for our categorical features.

### Remove Unused Features

**Unused features** are those that don’t make sense to pass into our machine learning algorithms. Examples include:

* ID columns
* Features that wouldn't be available at the time of prediction
* Other text descriptions

## Algorithm Selection

### Why Linear Regression is Flawed

Simple linear regression models fit a "straight line" (technically a hyperplane depending on the number of features, but it's the same idea). In practice, they rarely perform well. We actually recommend skipping them for most machine learning problems.

Their main advantage is that they are easy to interpret and understand. However, our goal is not to study the data and write a research report. Our goal is to build a model that can make accurate predictions.

In this regard, simple linear regression suffers from two major flaws:

* It's prone to overfit with many input features.
* It cannot easily express non-linear relationships.
* Let's take a look at how we can address the first flaw.

### Regularization in Machine Learning

This is the first "advanced" tactic for improving model performance. It’s considered pretty "advanced" in many ML courses, but it’s really pretty easy to understand and implement.

The first flaw of linear models is that they are prone to be overfit with many input features.

### Regularized Regression Algorithms

#### Lasso Regression

It stands for **L**east **A**bsolute **S**hrinkage and **S**election **O**perator.

Lasso regression penalizes the absolute size of coefficients, this leads to coefficients that can be exactly 0.
Thus, Lasso offers automatic feature selection because it can completely remove some features.

#### Ridge Regression

It stands for **R**eally **I**ntense **D**angerous **G**rapefruit **E**ating

Ridge regression penalizes the squared size of coefficients, this leads to smaller coefficients, but it doesn't force them to 0.
In other words, Ridge offers **feature shrinkage**.

#### Elastic-Net

It is a compromise between Lasso and Ridge.

Elastic-Net penalizes a mix of both absolute and squared size and the ratio of the two penalty types should be tuned.
The overall strength should also be tuned.

### Decision Tree Algorithms

It is a Supervised learning technique that can be used for both classification and Regression problems, but mostly it is preferred for solving Classification problems. It is a tree-structured classifier, where internal nodes represent the features of a dataset, branches represent the decision rules and each leaf node represents the outcome.

### Tree Ensembles

Ensembles are machine learning methods for combining prediction from multiple separate models, the most common methods for ensembles are the following:

#### Bagging

These attempt to reduce the chance overfitting complex models.
It trains a large number of strong learners in parallel, while strong learner is a model that is relatively unconstrained, Bagging then combines all the strong learners together in order to "smooth out" their predictions.

#### Boosting

Boosting attempts to improve the predictive flexibility of simple models, it trains a large number of "weak" learners in sequence.
while weak learner is a constrained model(i.e. you could limit the max depth of each decision tree), each one in the sequence focuses on learning from the mistakes of the one before it, boosting then combines all the weak learners into a single strong learner.

## Model Training

### How to Train ML Models

#### Split Dataset

Think of your data as a limited resource.

You can spend some of it to train your model (i.e. feed it to the algorithm).
You can spend some of it to evaluate (test) your model, but you can’t reuse the same data for both, and if you evaluate your model on the same data you used to train it, your model could be very overfit and you wouldn’t even know. A model should be judged on its ability to predict new, unseen data.
Therefore, you should have separate training and test subsets of your dataset.

![split dataset](https://elitedatascience.com/wp-content/uploads/2017/06/Train-Test-Split-Diagram.jpg)

Training sets are used to fit and tune your models. Test sets are put aside as "unseen" data to evaluate your models.

You should always split your data before doing anything else.
This is the best way to get reliable estimates of your models’ performance.
After splitting your data, don’t touch your test set until you’re ready to choose your final model!
Comparing test vs. training performance allows us to avoid overfitting... If the model performs very well on the training data but poorly on the test data, then it’s overfit.

#### Hyperparameters

There are two types of parameters in machine learning algorithms.
The key distinction is that model parameters can be learned directly from the training data while hyperparameters cannot.

##### Model parameters

They are learned attributes that define individual models, and they can be learned directly from the training data.

##### Hyper-parameters

They express "higher-level" structural settings for algorithms, and they are decided before fitting the model because they can't be learned from the data.

#### Cross-Validation

Cross-validation is a method for getting a reliable estimate of model performance using only your training data.

There are several ways to cross-validate. The most common one, 10-fold cross-validation, breaks your training data into 10 equal parts (a.k.a. folds), essentially creating 10 miniature train/test splits.

##### Steps for cross validation

1. Split your data into 10 equal parts, or "folds".
2. Train your model on 9 folds (e.g. the first 9 folds).
3. Evaluate it on the 1 remaining "hold-out" fold.
4. Perform steps (2) and (3) 10 times, each time holding out a different fold.
5. Average the performance across all 10 hold-out folds.

### Fit and Tune Models

Basically, all we need to do is perform the entire cross-validation loop on each set of hyperparameter values we'd like to try.
​
The high-level pseudo-code looks like this:

```shell
    For each algorithm (i.e. regularized regression, random forest, etc.):
    For each set of hyperparameter values to try:
    Perform cross-validation using the training set.
    Calculate cross-validated score.
```

At the end of this process, you will have a cross-validated score for each set of hyperparameter values... for each algorithm.

### Select Winning Model

* For regression tasks, we recommend Mean Squared Error (MSE) or Mean Absolute Error (MAE). (Lower values are better)
* For classification tasks, we recommend Area Under ROC Curve (AUROC). (Higher values are better)

The process is very straightforward:

* For each of your models, make predictions on your test set.
* Calculate performance metrics using those predictions and the "ground truth" target variable from the test set.

Finally, use these questions to help you pick the winning model:

* Which model had the best performance on the test set? (performance)
* Does it perform well across various performance metrics? (robustness)
* Did it also have (one of) the best cross-validated scores from the training set? (consistency)
* Does it solve the original business problem? (win condition).
