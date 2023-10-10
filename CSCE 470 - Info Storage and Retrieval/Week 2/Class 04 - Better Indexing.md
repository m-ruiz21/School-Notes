## Phrase Queries

Phrase queries are search queries that require the results to include a specific sequence of words or terms appearing in the exact order specified within the query.

For Example:
> "Taylor Swift", "470 Homework solution.

### Implementation Idea: Bi-word index

Remember [[Class 02 - Search Basics#Inverted Index (TF-IDF)|Inverted Index]] from the previous class. 
A bi-word index is going to work exactly like an TF-IDF index, except that instead of indexing every word, we're going to index every pair of words.

You can also expand it to more words by using Boolean queries.
So if I wanted to query "meet me at midnight" our query would be:  "meet me" AND "at midnight".
#### Issues
- Can create false positives - i.e. "at midnight I want her to meet me"
	- Can be solved by 3 word index, 4 word index, etc.? But we can go infinitely long with this strategy!  
- Takes up a lot of memory
	- Need to store every combination of two consecutive words O(2 * words) memory.

### Alternate Idea: Positional Index

The idea is to store the position in the index in the documents. So we have a dictionary, and for each term we have an entry like:

term 1: {
	document 1: position 1, position 2, position 6, …
	document 2: position 3, position 9, position 12, … 
	…
}

#### Phrase Querying with a positional index
When you query with a positional index, you not only check the existence, but the position as well.
> Note: with this solution we are exchanging processing power for storage. 
> This solution takes a lot more processing, but that the saving of 
## Proximity Queries

Another bonus of the positional index is that it also allows you to run proximity queries, i.e. "word 1 near word 2", "word 1 within 6 words of word 3", etc.

## Wildcard queries

Wildcard queries allow you to find anything that fits the given template. 
For example:

> "mid*"

is going to query for all words that start with "mid" like "midnight", "midterm", etc.

### Implementation Idea:  Binary Tree

Suppose we have a binary tree instead of a dictionary. This way, we can find all the words in the range mid <= words < mie. 

#### Issues
- This does not account for wildcard trees in the middle or the end of the word.

### Alternate Idea: Permuterm index

This is where you use a special "end of word" token like "@".

So for example:
midnight@
taylor@

Then you rotate every term:

taylor@, aylor@t, ylor@ta, lor@tay, or@tayl,  r@taylo, @taylor

midnight@, idnight@m, dnight@mi, night@mid, ght@midn, ght@midni, ht@midnig, t@midnigh

So if we have the query "ta * r", we can rotate the query so that the " * " is at the end $\rightarrow$ "r@ta*"

Now we can look it up in our rotated dictionary / binary tree. 
In this example, Taylor, Tater, Tailor should all be together since r@taylor, r@tater, r@tailor. 

## Tolerating Spelling Errors
Users make spelling mistakes all the time, so how do we know that  
britent spears $\leftrightarrow$ britney spears ?

We need to find a way to rewrite these queries so we get actual query results.

### One Approach: k-gram index / Jaccard Similarity
The k-gram index is going to check how many overlapping characters the query and the index have. It can be measured by the Jaccard Similarity formula:
$$ \begin{aligned} \frac{|A| \cap |B|}{|A| \cup |B|} \end{aligned} $$
This can also be used for [[Class 04 - Better Indexing#Wildcard queries|wildcard queries]].

### Another Approach: Edit Distance
Edit distance will check for the amount of least amount of edits (insert, replace, delete) to get to a known / indexed word using dynamic programming.
