This class is a continuation of [[Class 06 - Ranking]], where we discuss about how we will organize / [[Class 02 - Search Basics#"Front-end" vocabulary|represent our data]] using the [[Class 06 - Ranking#Vector Space Model|Vector Space Model]]. 
This time, we cover different functions we use to actually implement ranking using the [[Class 06 - Ranking#Vector Space Model|Vector Space Model]]. 

## Vector Space Scoring Functions
In vector space [[Class 06 - Ranking#Scoring|scoring functions]] work as [[Class 02 - Search Basics#"Back-end" vocabulary|comparison functions]] that compare the query and the index documents.
### Euclidean distance
The Euclidean distance formula finds the "physical" distance between two vectors in vector space.
It can be calculated by:
$$\begin{align} d(p,q) = \sqrt{\sum_{i \in |V|} (p_i - q_i)^2} \end{align}$$
where $p$ and $q$ are the vectors being compared and $|V|$ is the size of the vector space.

#### The Problem
Euclidian distance also takes into account the length of the documents. 
So if a document is entirely identical to the first half of another document, simply because of their difference in size, they would be considered to have a large distance from each other despite being, in large part, identical. 

### Cosine Similarity
Instead of finding the total space between the two vectors, we can just find the cosine of the angle between the two vectors to decide their similarity / difference.

To do this with vectors, we need to take the normalized dot product as follows:
$$\begin{align} d(p,q) = cos(\theta) = \frac{A \cdot B}{||A||\space ||B||} \end{align}$$
Alternatively, we can also normalize first:
$$\begin{align}d(p,q) = \frac{A}{||A||} \cdot \frac{B}{||B||} \end{align}$$
## Weighting 
We need to find weights / importance weights of each document and the query since good weighting is essential. 
Good / bad weighting can be the difference between good and bad scoring since it's going to make up the content of out vectors.

There are some words that are more informative, and some words that are less informative. 
So we need to make sure that we emphasize more informative words when querying. 
If we query "the aggies", "aggies" results should have more weight than "the".
### Classic Weighting: TF-IDF

- **TF** = term frequency
- **IDF** = inverse document frequency

Usually when we think of the "vector space model", we use TF-IDF weights + cosine similarity.

#### TF = term frequency
**The idea**: score each term in the document by the number of times it occurs in the document.
**Intuition**: the more a term occurs the more valuable it is.

There's two types main variations: 
**Raw TF**: $tf(t,d) =f_{t,d}$
**Logarithmically-scaled frequency** $tf(t,d) = log(1+f_{t,d})$

#### IDF = Inverse Document Frequency
**The Idea**: we want to see how rare the document is across all documents.
**The Intuition**: the rarer a term is across a collection, the more valuable it is. So a word like "the", which is found in almost every document, is not deemed highly informative.

We measure IDF through the following equation:
$$\begin{align} idf(t,D) = log \frac{||D||}{|\{ d\in D: t
\in d\}|} \end{align}$$
where $D$ is the set of all documents t is the term we want to weigh. 

In laymen's terms you can also view it as:

$$
\begin{align} 
	idf(t,D)=
	log \frac{
		total\space amount \space of \space docments
	}{
		amount\space of\space documents\space with \space term \space t
	}
\end{align}$$