# Recap

[[Class 24 - Ranking With Word Embeddings|Last time]], we talked about how we can use word embeddings like [[Class 22 - word2vec|word2vec]] to create a better understanding of the user's query and retrieve the most conceptually relevant documents.

We also found that was usually works better is using the OUT vectors for the document and the IN vectors for the query (IN-OUT embedding).

# Beyond DESM

The traditional IR Setup works as following:

![[Pasted image 20231210165130.png]]

Idea: use neural models atop of existing techniques.

![[Pasted image 20231210165742.png]]

# BERT

In 2018, BERT came out and largely outperformed most previous methods on common NLP tasks. 

In addition, according to GLUE, BERT also achieved state-of-the-art performance on question answering and commonsense inference.

## Typical Usage

 **First Phase: pre-training**: 
- Train BERT on large-scale and unlabeled dataset to capture general language knowledge.

**Second Phase: fine-tuning:**
- Fine-tune BERT on usually a small size and labeled NLP dataset.