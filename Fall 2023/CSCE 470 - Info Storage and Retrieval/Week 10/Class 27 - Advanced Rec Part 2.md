
# The Big Idea:

-  Use a de-noising autoencoder instead of vanilla autoencoder (as in [[Class 26 - Advanced Rec#AutoRec Autoencoding + Collaborative Filtering|AutoRec]]).

# Denoising Autoencoder

**Idea**: insert noise into the input (often called "corrupting" the input).

**Hope**: force the hidden encoding layer to discover more robust features and to prevent it from simply learning the identity function.

## How to add noise?

**Gaussian Noise**: the values that the noise can take is Gaussian-distributed. 

**Mask-out/drop-out**: randomly overwrite each of the dimensions of x with 0 with a probability of q. 

## Summary

Two autoencoder-based methods for recommendations.
- AutoRec.
- CDAE $\rightarrow$ idea of adding noise.

# Neural Collaborative Filtering

Remember [[Class 16 - Latent Factors|latent factors]] and their use in [[Class 15 - Collab Filtering|collaborative filtering]]. 

So now, instead of the dot product, let's try to learn the similarity function.

**What's the intuition?**
- Dot product is fixed, not flexible.
- There could be interesting non-linear interactions between users and items.
- A learned similarity function should give us better results.