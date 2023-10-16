## Evaluating a Search Engine
### Measures for a Search Engine
- How fast does it index.
- How fast does it return results
- The expressiveness 

Alternatively, we can measure it through user happiness. This could be through A/B testing, measuring time in website, time to purchase, etc. 

However, these measurements take a long time and have various complications / setbacks. 
Thus, it is easier for us to measure the **relevance** of the search results.

## Measuring Search Relevance (Offline)

### Requirements to measure relevance
- A benchmark document collection
	- Issues: large data collection and filtering.
- A benchmark set of queries
	- Issues: crafting thousands of queries.
- A binary assessment of "Relevant" and "Not Relevant" for each query and each document.
	- Very human intensive task with large cost.


### Some evaluation measures

**Unranked**
- [[#Precision and Recall|Precision]]
- [[#Precision and Recall|Recall]]
- [[#F Combining Precision and Recall|F]]

**Ranked**
- [[#Precision @ k]]
- [[#NDCG]]

### Precision and Recall
**Precision**: Retrieved documents that are relevant / retrieved documents.
**Recall**: Retrieved documents that are relevant / all relevant documents.

### F: Combining Precision and Recall

$$\begin{align} F = \frac{2}{recall^{-1} + precision^{-1}} = 2 \frac{precision * recall}{precision + recall} = \frac{2tp}{2tp + fp + fn}\end{align}$$

### Precision @ k
**Precision @ k:** retrieved documents that are relevant in the top-k / k

This is especially useful when users tend to especially focus on the top search results, thus emphasizing the ranking of the search results.

### NDCG
**Normalized Discounted Cumulative Gain**
- Sensitive to the position of the highest ranking documents.
- Log discounting of results.
- Normalized for different length lists.
- Very popular in practice

Rather than thinking of binary relevance, we think of documents with multiple values of relevance.

For example: 
0 - Not relevant
1 - Somewhat relevant
2 - Really Relevant
3 - Perfectly Relevant