# Item-Item Collaborative Filtering

The idea of item-item collaborative filtering is the same as [[Class 14 - Recommenders#User-User Collab Filtering|User-User Collab Filtering]], except we're going to look at similar items instead of users.

So we're going to find items similar to items that our user has liked in the past:

$$p_{u,i} = \frac{\sum_{j \in S} s(i,j) r_{u,j}}{\sum_{j\in S}|s(i,j)|}$$

# Issues  

There are some issues with collaborative filtering:
- Cold start: we need sufficient users to bootstrap the recommendations.
- Sparsity: in many cases, the ratings matrix can be very sparse making it difficult to find the "nearest" neighbors.
- New items: how do we handle new items that have no ratings yet?
- Unique tastes: can be difficult to recommend for users with unique tastes.