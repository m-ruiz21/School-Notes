
At this point in the class, we decide that our store currently only supports Boolean queries and the queries will be run to search lyrics.

>Example: karma, love OR song, Taylor AND Swift, Taylor AND (NOT Swift), etc.

Based on those results, we return the songs **as a set**

First issue: how will we store / index our information?

## Term-Document Incidence Matrix

A term-document incidence matrix is a matrix has the term as the key and the existence of the term in the document as the value.

### Example

|         | Song 1 | Song 2 | Song 3 | Song 4 |
| ------- | :----: | :----: | :----: | :----: |
| any     | 0      | 1      | 1      | 1      |
| believe | 1      | 0      | 1      | 0      |
| choose  | 1      | 0      | 0      | 0      |
| love    | 1      | 1      | 0      | 0      |

*Query*: "love" AND "any"
*Result*: Song 2

### Pros and Cons

Pros:
- Performing AND and OR operations between terms is straightforward (and thus quicker) by using binary logical operations directly on the matrix.

Cons: 
- TDIM can be memory-intensive, especially for large document collections with many unique terms, as it requires a cell for each term-document pair.

TDIM can be efficient for certain types of Boolean queries but may become impractical for very large collections due to its memory requirements.

## Inverted Index
To reduce memory usage, the inverted index only stores if the term is included in the document.

### Example

**Any** $\rightarrow$ song2 $\rightarrow$ song3 $\rightarrow$ song4   
**believe** $\rightarrow$ song1 $\rightarrow$ song3   
**choose** $\rightarrow$ song1   
**love** $\rightarrow$ song1 $\rightarrow$ song2    

### Summary: Boolean Retrieval
Advantages  
- Precise, if you know the right strategies (e.g., how to itera4vely refine your  queries, use of boolean operators, ...)  
- Typically, efficient in practice

Disadvantages
- Users must understand Boolean logic!  
- Boolean logic does not capture language richness  
- Feast or famine in results: you get 0 results or 1000s  
- Result sets are unordered — users have to sift through 1000s of hits  
- Does not give partial matches E.g., a doc doesn’t exactly match the query but it’s “close”.