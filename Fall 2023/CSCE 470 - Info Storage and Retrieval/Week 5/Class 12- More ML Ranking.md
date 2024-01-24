# Recap

So [[Class 11 - Start ML Ranking|last time]] we discovered that given:
- A benchmark document collection.
- A benchmark suite of queries.
- A binary assessment of either Relevant or Non-relevant for each query and each document.

The hope being that if we learn a good classifier, then we can classify new (unseen) query-document pairs as either relevant or non-relevant.

# Implementing ML Ranking

There's many ways to learn function f, but specifically we're going to focus in on Rocchio Classification and k-Nearest Neighbors Classification.

## Rocchio Classification

**Training**: For our labeled training data, we need to find the centroid of each "class" (in this case relevant vs non-relevant).

**Testing**: For our unlabeled testing data, assign each point to the class of the closet centroid.

## k-Nearest Neighbors Classification

**Training:** Nothing.

**Testing**: For out unlabeled testing data, assign each point to the majority class of the k-closest points.
> So for k = 3, we find the k-closest points and see if they're majority Relevant or Non-relevant.

## Types of Classifiers

- Linear (we can find a line and hyperplane to divide the data).
	- Rocchio is a linear classifier.
- Non-Linear (we cannot find a hyperplane).
	- KNN is non-linear.

## Interesting Side Note: Nallapati 2004.

In 2004, these ML methods were state of the art. However, Nallapati in 2004 found that these ML classifiers could **NOT**
outperform traditional scoring functions based on features.