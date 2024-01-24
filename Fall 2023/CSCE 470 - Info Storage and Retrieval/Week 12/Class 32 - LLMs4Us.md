# Recap
Last time we went over [[Class 30 - Language Models#N-gram models|N-Gram Models]]and how they can be used and evaluated. 

# N-gram Language Model Problems

**Storage:** Need to store count for all n-grams you saw in the corpus. Remember, increasing n or increasing corpus increases the model size and thus the storage needed!

**Quality:** Models only know about a small window (e.g. the past n words).

**Sparsity:** if the sentence we're looking at doesn't exist? The probability is 0. 

## From memorization to modeling

N-gram models essentially memorize what words occur next to each other, they don't truly *learn* of the relationships between the words.

So how do we build models that capture these relationships?

## Neural Language Model

**Advantages:**
- Can process any length input
- Computation for step t can (in theory) use information from many steps back.
- Model size doesn't increase for longer input context.

**Disadvantages:**
- Recurrent computation is slow.
- In practice, difficult to access information from many steps back.

## Character Level Language Models
*Let's train RNNs to generate text character by character and ponder the question "how is that even possible".*

So, let's train RNN character-level language models.  
That is, we’ll give the RNN a huge chunk of text and ask it to model the probability distribution of  the next character in the sequence given a  sequence of previous characters. 
This then allow us to generate new text one character at a time.

# Pre-Trained LM to LLMs

One key emergent ability in GPT-2 is **zero-shot learning**.
## N-shot learning

**0 shot learning** is the ability to predict without examples.
So for example, imagine we train a model on pictures of animals + text descriptions.  
The training data includes horses but no zebras (That is, it has no examples (or “shots”) of zebras).  
So at “test” time, a model that can identify a zebra from a  picture would be an example of zero-shot learning.

Then, with GPT-3 the ability to do emergent **few-shot learning**, or predicting with few examples.

## LLM Downsides

Some tasks seem too hard for even large LM's to learn through prompting alone. 
This is especially the case for tasks involving richer, multi-step reasoning.

One idea: **Chain-of-thought** prompting.

Chain-of-thought prompting is the act of adding the chain of thought for the prompting examples given.