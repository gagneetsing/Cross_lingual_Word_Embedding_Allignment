
# Cross-Lingual Word Embedding Alignment

This project implements both supervised and unsupervised cross-lingual word embedding alignment methods to align English and Hindi word embeddings. The alignment enables word translation between the two languages by mapping the embeddings into a shared vector space.

# Methods Overview
1. # Supervised Procrustes Alignment

Goal: Learn a linear mapping from the source language (English) embeddings to the target language (Hindi) embeddings using a bilingual dictionary (MUSE).

# Approach:
The Procrustes method learns an orthogonal transformation to align the source embeddings with the target embeddings while preserving distances and angles in the vector space.
The mapping is learned by minimizing the distance between word pairs in the bilingual lexicon.

2. # Unsupervised CSLS + Adversarial Training

Goal: Learn the mapping between the source and target embeddings without any parallel data or bilingual dictionary.

# Approach:

Adversarial Training:
A mapping network is trained to align the English embeddings to the Hindi embeddings.
A discriminator network is trained to distinguish between real Hindi embeddings and mapped English embeddings.
The mapping network is optimized to “fool” the discriminator, forcing it to produce mappings indistinguishable from the target embeddings.

CSLS (Cross-Domain Similarity Local Scaling):
CSLS is used to refine the translation by adjusting the similarity scores based on local density to mitigate the “hubness” problem (where some points appear as nearest neighbors too often).


# How It Works

The notebook performs the following steps:

1. # Data Preparation
Embeddings: Pre-trained FastText embeddings for English and Hindi are used




you can download from this link
 https://fasttext.cc/

 Bilingual Lexicon: The MUSE dataset provides a list of English-Hindi word pairs for supervised alignment.

 you can download Bilingual dictionary from here https://dl.fbaipublicfiles.com/arrival/dictionaries/en-hi.txt

 for more information visit here https://github.com/facebookresearch/MUSE

 2. # Supervised Alignment (Procrustes Method)

The Procrustes method is used to learn an orthogonal transformation mapping the English embeddings to the Hindi embeddings.

Evaluation:
Precision@1 and Precision@5 are computed using the MUSE test dictionary.
Cosine similarities between aligned word pairs are calculated to assess semantic similarity.
An ablation study is conducted to assess the impact of the bilingual lexicon size on alignment quality.

3. # Unsupervised Alignment (CSLS + Adversarial Training)

Adversarial Training is used to learn the mapping between English and Hindi embeddings without parallel data.
CSLS refines the translation by improving the nearest neighbor search through local scaling.

Evaluation:
Precision@1 and Precision@5 metrics are used to compare the unsupervised method with the supervised Procrustes method.

# Evaluation:
Supervised Precision Results:

Precision@1: 29%
Precision@5: 56.6%

Unsupervised Precision Results (CSLS):

Precision@1: 1.78%
Precision@5: 1.78%



# Cosine Similarity Analysis

Cosine similarity between aligned word pairs shows that the supervised Procrustes method generally produces better semantic alignment than the unsupervised method.

# Instructions to Run the Notebook

1. Clone the Repository
git clone https://github.com/yourusername/cross-lingual-word-embedding-alignment.git

cd cross-lingual-word-embedding-alignment

2. Install Dependencies
Install the required libraries using pip

3. Run the Colab Notebook

# Ablation Study
An ablation study is conducted to measure the effect of the size of the bilingual lexicon (e.g., 5k, 10k, 20k word pairs) on alignment quality. The results show that:

Increasing the lexicon size improves the precision of word translation, as the model has more data to learn the mapping effectively.

# Conclusion
This project demonstrates the implementation and evaluation of both supervised and unsupervised methods for cross-lingual word embedding alignment. The results show that while supervised methods are more accurate when a bilingual lexicon is available, unsupervised methods like CSLS combined with adversarial training can be effective in the absence of parallel data.

