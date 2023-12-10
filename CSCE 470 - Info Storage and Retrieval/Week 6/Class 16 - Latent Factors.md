# Recap

Recall [[Class 15 - Collab Filtering|item-item collaborative filtering]] and [[Class 14 - Recommenders|user-user collaborative filtering]]. 

Note what it is used for and its flaws, specifically the cost of evaluation given a large sparse matrix.

# The Netflix Prize: Evaluation
## RMSE = Root Mean Squared Error

$$\sqrt{\frac{1}{n} \sum_{u,i}(\hat{r_{u,i}} - r_{u,i})^2}$$

## The winning strategy: Genres/groups of related movies

These are called "latent factors" or "hidden factors". Our goal is to uncover these latent factors with matrix factorization.

To estimate the rating: user latent factor * item latent vector = estimated ratings!
$$e(u,i) = p_u^T \cdot q_i$$