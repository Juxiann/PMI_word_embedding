# word2vec

This notebook implements the skip-gram architecture of word2vec. It also shows some applications of the embedding such as finding synonyms and solving anagrams. 

A subset of the Wikipedia corpus of 126 million words is used here. You can create a Wikipedia corpus from the Wikipedia dump file with code such as: https://gist.github.com/mmmayo13/0f2ad1b0f7f83810514687c4ef61032e#file-make_wiki_corpus-py

## Method

Using the Wikipedia data with a symmetric context window size of 5, the pointwise mutual information (PMI) matrix is computed. Where the (i,j)-th entry is

$$
M_{ij} = \log\left( \frac{(N^p(w_i, w_j)+1)\cdot N(S^p)}{N^p(w_i)\cdot N^p(w_j)} \right)
$$

where $S^p$ is the set of all word-context pairs observed in the Wikipedia corpus. $N^p(w_i,w_j)$ is the number of times $w_i$ and $w_j$ ooccur within 5
words of each other across the entire corpus.

It can be shown that skip-gram with negative sampling is equivalent to the factorization of the symmetric matrix $M=VV^T$ whose entries consist of the pointwise mutual information. We use the k-SVD to factorize the large matrix.
