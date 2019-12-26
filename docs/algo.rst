Machine learning algorithms
###########################

Supervised methods
******************

Linear regression
=================

Linear methods are parametric methods where function learned has form :math:`f(x) = \phi \left( w^T x \right)` where :math:`\phi()` is some activation function.

Generally, optimized by learning weights by applying (stochastic) gredient descent to minimize loss function, e.g. :math:`\sum \lvert \hat{y_i} - y_i \rvert^2`

Simple; a good place to start for a new problem, at least a baseline

Methods: Linear regression for numeric target outcome. Logistic regression for categorical target outcome. 

Linear regression (univariate)
------------------------------

Image:univariate.png

Model relation between a single feature (explanatory variable :math:`x`) and a real-valued response (target variable :math:`y`)

Given data :math:`(x,y)` and a line defined by :math:`w_0` (intercept) and :math:`w_1` (slope), the vertical offset for each data point from the line is the error between the true label :math:`y` and the prediction based on :math:`x`

The best line minimizes the sum of squared errors (SSE)

We usually assume the error is Gaussian distributed with mean zero and fixed variance

Linear regression (multivariate)
--------------------------------

Multiple linear regression includes :math:`N` explanatory variables with :math:`N \geq 2`:

.. math::

    y = w_0x_0 + w_1x_1 + \cdots + w_Nx_N = \sum_{i=0}^{N} w_ix_i

Sensitive to correlation between features, resulting in high variance of coefficients.

scikit-learn implementation: 

.. code-block:: console

	sklearn.linear_model.LinearRegression

Logistic regression
===================

Predict whether a credit card transaction is fraud

Image:fraud.png

Estimates the probability of the input belonging to one of the two classes: positive and negative.

Vulnerable to outliers in training data.

Relation to linear model:

.. math::

    \sigma (z) = \frac{1}{1+\mathrm{e}^{-z}}

:math:`z` is a trained multivariate linear function

:math:`\phi` is a fixed univariate function (not trained)

Objective function to maximize = probability of the true training labels.

Sigmoid curve. Image: sigmoid.png 

Model relation between features (explanatory variables :math:`x`) and the binary responses (:math:`y=1` or :math:`y=0`)

For all features, define the linear combination:

.. math::

    z = w^T x = w_0 + w_1x_1 + \cdots + w_Nx_N

Define the probability of :math:`y=1` given :math:`x` as :math:`p` and find the logit of :math:`p` as:

.. math::

    logit(p) = \log \frac{p}{1-p}


Logistic regression finds the best weight vector by fitting the training data

.. math::

    logit(p(y=1 \vert x)) = z

Then, for a new observation, you can use the logistic function :math:`\phi(z)` to calculate the probability to have label :math:`1`. If it is larger than a threshold (for example :math:`0.5`), you will predict the label for the new observation to the positive.

.. code-block:: console

	sklearn.linear_model.LogisticRegression

Linear separable versus non-linearly separable

Image:separable.png
