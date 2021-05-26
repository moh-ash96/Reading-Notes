# Linear regression

Linear regression is a popular technique that attempts to model the relationship between two variables by fitting a linear equation to observed data.
It can be implemented by using *numpy*, *scipy*, *stats model*, and *scikit*.
Here we are going to use *scikit.*

## Scikit

scikit learn is a powerful python module for machine learning.

### Simple linear regression with scikit

1. Import packages and classes, we will need numpy and linear regression.

    ```python
    import numpy as np
    from sklearn.linear_model import LinearRegression
    ```

2. Provide data, The data we need here is the input (regression, x) and the output (predictor, y), and they should be arrays or similar objects.

    ```python
    x = np.array([5, 15, 25, 35, 45, 55]).reshape((-1, 1))
    y = np.array([5, 20, 14, 32, 22, 38])
    ```

    The reshape here is called for the input because this array is required to be two-dimensional.

3. Create a model and fit it, here we create an instance of linear regression, which will present the regression model and it can have optional parameters, such as:

    * **fit_intercept** is a Boolean (True by default) that decides whether to calculate the intercept 𝑏₀ (True) or consider it equal to zero (False).
    * **normalize** is a Boolean (False by default) that decides whether to normalize the input variables (True) or not (False).
    * **copy_X** is a Boolean (True by default) that decides whether to copy (True) or overwrite the input variables (False).
    * **n_jobs** is an integer or None (default) and represents the number of jobs used in parallel computation. None usually means one job and -1 to use all processors.

4. Get results, Once you have your model fitted, you can get the results to check whether the model works satisfactorily and interpret it.

5. Predict response, Once there is a satisfactory model, you can use it for predictions with either existing or new data, and for that we can use `.predict()` and we pass the regressor as the argument and get the corresponding predict response.
