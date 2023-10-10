Previously, we covered the [[Class 02 - Search Basics#Inverted Index|Inverted Index]], an index that references all the documents that contain our terms. However, we need to decide what is going to be in the index.

In other words, what are the valid tokens to go in our dictionary?
Furthermore, how can we improve our index and help our users do more than just simple queries?

## Tokenization
**Definition**: Tokenization is the process of creating new "tokens" from our query / document text.
### Example:
**Input**: a bunch of text
> "Welcome to class!"

**Output:** valid tokens
> Approach 1: "welcome", "to, "class", "!"
> Approach 2: "welcome", "to", "class !"

Tokenization is a critical step in determining the way our users interact with our search engine since if the token is not in our index, then the user cannot search for it!

### Typical Issues in Tokenization

- Language: i.e. "!!!"
- Hyphens: i.e. "13-3"
- Numbers
- Whitespace
- Normalization: i.e. U.S.A $\rightarrow$ USA, Windows $\rightarrow$ windows. 
- Case folding: i.e. Windows $\rightarrow$ windows
- Stop words: words we can safely remove, i.e. "to", "a", "an", etc

## Tokenization strategies
### Stemming
When tokenizing, it might be useful to introduce stemming.
**Stemming is the process where we "stem" or remove the last few "meaningless" characters.**
It's meant to join similar words together in our index to reduce the size.
However, this process can sometimes result in the shortening of a word like "caring" to "car".

### Lemmatization
Lemmatization is a processes similar to stemming since it serves the same purpose of joining similar words together. 
However, Lemmatization doesn't just blindly remove the last few characters. 
Rather, it looks at the context of its use and converts it to its meaningful base form. 

### Stop Words Removal
Stop words removal is the process of removing the empty "filler" words in a sentence like "at", "and", "from", etc.
## Testing our Tokenization strategy
- User tests (A/B testing)
- Create custom test cases (create expected results vs actual results).