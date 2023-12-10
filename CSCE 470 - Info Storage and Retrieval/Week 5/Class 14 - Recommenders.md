# Recap

We're adding to Cav's Algorhythms old rec system.
So far we can do:
- [[Class 02 - Search Basics|Boolean Keyword Queries]]
- [[Class 04 - Better Indexing#Phrase Queries|Phrase Queries]]
- [[Class 04 - Better Indexing#Proximity Queries|Proximity Queries]]
- [[Class 04 - Better Indexing#Wildcard queries|Wildcard Queries]]
- [[Class 07 - Ranking Functions|Ranked Retrieval]]

For the rest of the class we will be generating recommendations for our users, even in the absence of a query.  (Recommender Systems aka RecSys).

First new feature: creating a top-k list.

# Recommenders

## Non-personalized Recommenders

Editorial and hand-curated
- Your list of favorites or "essentials".
- Promoted items.

Simple aggregates
- Most-viewed songs this month, week, day, etc.
- Most recent.

## Introducing Ratings

Ratings will be the backbone of our system. 
After some time, we'll have a large and sparse rating matrix with users and their ratings of different items.

## Creating Ratings

So, given these user ratings, how can we populate the top-k list?

All the previous recommendations we've mentioned were non-personalized. Using these ratings, we should be able to create personalized ratings. 
We want each person to be able to view their personalized top-k list.

## Estimating Ratings

Using our ratings matrix, we can create a baseline estimate:

$$b_{u, i} = \mu + b_u + b_i $$
Where 
$\mu$ is the overall mean rating for all items
$b_u$ is the rating deviation for user $u$ = avg rating of user $\mu_i-\mu$  $b_i$ is the rating deviation for item $i$ = avg rating of item $\mu_i-\mu$

We can use this baseline estimate as our first personalized recommender!

Alternatively, you can define these "residuals" as:

$$b_u = \frac{1}{|I_u|} \sum_{i \in I_u} (r_{u,i} - \mu) $$

$$b_i = \frac{1}{|U_i|} \sum_{u \in U_i} (r_{u,i} - b_u - \mu) $$

We can further "regularize" the baseline, e.g., 
$$b_u = \frac{1}{|I_u| + \beta_u} \sum_{i\in I_u} (r_{u,i} - \mu)$$

Here, the $\beta$ term acts as a "damping term". If a user has given very few ratings, then we don't have a lot of confidence in the rating deviation $b_u$.
A very large choice means the rating deviation is close to 0.
However, a very small chose of $\beta$ means that we're back to our original baseline.

### Takeaways
If you have ratings, use the baseline estimate as your foundation. 
It's super easy to implement and gives reasonable guesses. 
Soon, we'll combine it with collaborative filtering and ML learning methods.

# User-User Collab Filtering

## The Big Idea

Somewhere in our collection of users, there are some users who have a similar preference for albums as our current user. 

So, we can recommend albums that these "similar" users prefer.

## Challenges

- How do we find these users with similar preferences as our target user?
	- Let's define a similarity score between users based on the ratings that users give (in our ratings matrix).
	- Then use this similarity score to find the k nearest neighbors to our target user.
- How do we find good items to recommend our target user?
	- Let's aggregate the ratings of the neighbors to find good items to recommend.

## Defining Similarity

### Jaccard Coefficient
One way we can find similarity is with the **Jaccard Coefficient**:. 
$$J(A,B)=\frac{|A\cap B|}{|A \cup B|}$$
Given two sets A and B, the Jaccard Coefficient measures the size of the intersections divided by the size of the union of the two sets. So:
- $J(A,B)=0$ means that the two sets have nothing in common.
- $J(A,B)=1$ means the two sets are exactly the same.

### Cosine Similarity

$$s(u, v) = \frac{\sum_i r_{u,i}r_{v,i}}{\sqrt{\sum_i r^2_{u,i}} \sqrt{\sum_i{r^2_{v,i}}}}$$

Cosine similarity measures the angle between two vectors (based on the ratings given by the user).
- If angle between the two vectors is 0, then cosine = 1.
	- Meaning that the two vectors are perfectly similar!
- If the angle between the two vectors is 90, then cosine = 0.
	- Meaning that the two vectors are not similar at all!

## Finding The Recommended Items

We can find the recommended items with:
$$p_{u,i} = \bar{r_u} + \frac{\sum_{u'\in N} (r_{u',i} - \bar{r_{u'}})}{\sum_{u' \in N} |s(u, u')|}$$

= Akbar's average rating shifted by the weighted average of the neighboring user's ratings differences. 