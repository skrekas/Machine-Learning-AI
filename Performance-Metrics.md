## Performance Metrics

### Regression 

#### 1. Introduction 

Regression models (linear, non-linear etc.) map the relationship between one or more independent variables (e.g. $X_1, X_2, ..., X_n$) with a dependent/target or response variable (e.g. $Y$). 

The example adopted herein, draws data from  <a href="https://www.kaggle.com/">Kaggle's</a> example about <a href="https://www.kaggle.com/datasets/andonians/random-linear-regression">Linear Reression</a>.

#### 2. Metrics
##### 2.1 Mean Squared Error (MSE)
This is one of the most common performance metrics used in regression problems. The mean squared error is defined as the <b>average of the squared difference of target variable</b> $y$ <b>and the value</b> $\tilde{y}$ <b>that is predicted by the regression model</b>.
$$MSE=\frac{1}{N}\sum_{i}^{N}(y_i-\tilde{y_i})^2$$
Some important features of the MSE:

- It is differentiable and therefore can be optimized better.
- Due to squaring, it emphasizes even small errors and therefore provides an overestimation of the models error.
- Again due to squaring, this metric is more <b><i>prone to outliers than other metrics</i></b>. 


```python
import numpy as np
```
  
##### 2.2. Mean Absolute Error (MAE)
The Mean Absolute Error is defined as the <b>average of the difference between the target variable</b> $y$ <b>and the value predicted by the regression model</b> $\tilde{y}$.
$$MAE=\frac{1}{N}\sum_{i}^{N}|y_i-\tilde{y_i}|$$
Key characteristics of the MAE:
- MAE is not differentiable.
- It is more robust to outliers when compared to MSE since it doesn't square errors.
- It provides a measure of how far the predicted value is from the actual one.

##### 2.3. Root Mean Squared Error (RMSE)
The root mean squared error is define as the squared root of the average squared difference between the actual value $y$ and the value $\tilde{y}$ predicted by the regression model.
$$RMSE=\sqrt{MSE}=\sqrt{\frac{1}{N}\sum_{i}^{N}(y_i-\tilde{y_i})^2}$$


##### 2.4. $R^2$ Coefficient of Determination
This metric aims to ansert the question: How much of the variation in target variable $y$ is explained by the variation in the independent variable $x_1, x_2, ..., x_n$.

This metric is calculated based on the mean squared error.
The steps to calculate $R^2$ are:

- Compute the total variation in $y$
$$SE(\bar{y})=\sum_{i}^{N}(y_i-\bar{y})^2$$

- Compute the percentage of variation described by the regression line
$$\frac{SE(line)}{SE(\bar{y})}$$

- Finally, we have a metric that expresses how good or bad the fit of the regression line is.
$$coeff(R^2)=1-\frac{SE(line)}{SE(\bar{y})}$$

The $R^2$ metric is a metric that is calculated by other metrics. Therefore it is called a <b>post metric</b>. 
A few comments about the coefficient $R^2$:
- if the sum of the squared error is small then the $coeff(R^2)\rightarrow 1$ which indicates an ideal fit, or in terms of variance, that the regression model has captured 100% of the variance in the target variable $y$.
