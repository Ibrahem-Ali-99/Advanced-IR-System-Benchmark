# Information Retrieval System
## Overview
- This project implements a comprehensive Information Retrieval (IR) system with a focus on advanced retrieval and re-ranking techniques. Built using the PyTerrier framework, it provides a robust foundation for classic and neural-based retrieval models, evaluated with standard IR metrics.
Key Features & Technical Overview
Classic IR Foundation

- Built a robust baseline using the PyTerrier framework, with an inverted index supporting standard retrieval models like TF-IDF and BM25.

## Advanced Query Expansion

- Implemented and benchmarked a classic pseudo-relevance feedback model, RM3.
Engineered a custom neural query expansion technique using Sentence-BERT (SBERT) embeddings to find semantically similar terms from initial documents and enrich the original query.

## Two-Stage Neural Re-ranking Pipeline

- Developed a first-pass retrieval stage (using BM25) to generate an initial set of candidate documents.
- Designed and implemented two powerful BERT-based re-ranking models for the second stage:
### MonoBERT (Pointwise): A cross-encoder that individually scores the relevance of each query-document pair for fine-grained ranking.
### DuoBERT (Pairwise): A more advanced model that learns relative preferences by comparing pairs of documents (doc_i, doc_j) for a given query, improving ranking accuracy.



## Rigorous Evaluation

- Conducted a thorough performance analysis comparing all implemented systems (BM25, TF-IDF, RM3, SBERT-Expansion, MonoBERT, DuoBERT) using standard IR metrics like nDCG, MAP, and P@10.

## Interactive Demonstration

- Deployed the full system into a user-friendly Gradio web interface, allowing for real-time queries and side-by-side comparisons of the different retrieval models.

