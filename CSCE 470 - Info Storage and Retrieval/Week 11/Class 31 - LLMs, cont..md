# Recap

Last time, we covered that [[Class 30 - Language Models|Language Models]] are simply anything that calculated the probability of a sentence or a random word combination.

# Practical Issues

As we add more sentences, the probability of a sentence becomes ridiculously low (practically 0). 

So to avoid underflow, we're going to log everything.

$$log(p_1*p_2*p_3*p_4) = log(p_1) + log(p_1) + log(p_3) + log(p_4)$$

# Evaluation

So now, how do we evaluate our LLM?
We use **perplexity**:

$$PP(W) = n\sqrt{\prod^{N}_{i=1} \frac{1}{P(w_i|w_{i-1})}}$$