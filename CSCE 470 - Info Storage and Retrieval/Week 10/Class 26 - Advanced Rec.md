# Pros / Cons of Deep Learning for Rec

**Strengths**
- Nonlinear transformation
- Representation learning
- Sequence modeling
- Flexibility

**Weaknesses**
- Interpretability
- Data requirement
- Extensive hyperparameter tuning

# AutoRec:  Autoencoding + Collaborative Filtering

Recall [[Class 16 - Latent Factors|latent factors]] and matrix factorization and how it allows us to estimate the rating for every user-item pair through two smaller matrices rather than having a large sparse ratings matrix. Also recall its use with [[Class 15 - Collab Filtering|collaborative filtering]].

In sum: it allows us to take a sparse vector and turn it into a dense **embedding** matrix.

**So, AutoRec is another way to "densify" the matrix.**

Given ratings vector r from the set of ratings vectors S, and a reconstruction function h, the goal is to minimize the error:
$$\underset{\theta}{min} \sum_{r\in S} ||r-h(r;\theta)||^2_2,$$

## What do we get?

With this, we can densify the matrix, meaning we can immediately use those estimated ratings for recommendation.

We also get dense representations of our users (or items), which we can use as inputs to other recommendation models.

It does this with the **reconstruction function** $h(x)$:
$$h(x) = f(g(xV + b_1)Q + b_2)$$
where $f(\cdot)$ and $g(\cdot)$ are activation functions, $V$ and $W$ are the weights in the first and second layer, $b_1$ and $b_2$ are the bias vectors in the first and second layers.

## Reminder: Activation Functions

The most common activation functions:
- Identity: $f(x) = x$
- Binary step: $f(x) = \left\{ \begin{array}{ll} 0 & x < 0 \\ 1 & x \geq 0 \\ \end{array} \right.$ 
- Sigmoid (aka logistic or soft step): $f(x) = \sigma (x) = \frac{1}{1+e^{-x}}$ 
- TanH: $f(x) = tanh(x) = \frac{(e^x - e^{-x})}{(e^x + e^{-x})}$  