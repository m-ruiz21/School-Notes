Previously, we covered the [[Class 02 - Search Basics#Inverted Index|Inverted Index]], an index that references all the documents that contain our terms. However, we need to decide what is going to be in the index.

In other words, what are the valid tokens to go in our dictionary?
Furthermore, how can we improve our index and help our users do more than just simple queries?

## Tokenization

Tokenization is the process of creating new "tokens" from our query / document text.

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
- Normalization: i.e. U.S.A $\rightarrow$ USA
- Case folding: i.e. Windows $\rightarrow$ windows
- Stop words: words we can safely remove, i.e. "to", "a", "an", etc
- Stemming / Lemmatization: joining similar words, i.e. "words" and "word"

### Testing our Tokenization strategy
- User tests (A/B testing)
- Create custom test cases



