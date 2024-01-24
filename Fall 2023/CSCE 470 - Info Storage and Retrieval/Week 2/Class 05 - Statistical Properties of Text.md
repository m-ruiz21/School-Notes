## Heap's Law

Heap's law states that, in practice, the vocabulary continue to grow with our collection size.  

$$ \begin{aligned} V_R(n) = Kn^\beta \end{aligned} $$
Where $V_R$ is the number of distinct words in text of size $n$ and $K$ / $\beta$ are variables whose values we decide empirically. 

## Zipf's Law 

Zipf's law states that the the $i$th most frequent term has a frequency proportional to 1/i.

$$ \begin{aligned} cf_i \propto \frac{1}{i} \end{aligned} $$
Where $cf_i$ is the collection frequency for the $i$th most frequent term. 

> Essentially: "A few words happen a lot, and a lot of words show up very little"

This is caused through a "Balance between the speaker's desire for a small vocabulary and the listeners desire for a large one".