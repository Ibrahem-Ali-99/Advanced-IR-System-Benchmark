# Advanced-Information-Retrieval-System-for-CORD-19

Overview

This project implements a comprehensive Information Retrieval (IR) system with a focus on advanced retrieval and re-ranking techniques. Built using the PyTerrier framework, it provides a robust foundation for classic and neural-based retrieval models, evaluated with standard IR metrics.

Key Features





Classic IR Foundation: Establishes a robust baseline with PyTerrier, featuring an inverted index and standard retrieval models (TF-IDF, BM25).



Advanced Query Expansion:





Implements RM3, a classic pseudo-relevance feedback model.



Introduces a custom neural query expansion using Sentence-BERT (SBERT) embeddings to identify semantically similar terms from initial documents, enhancing query richness.



Two-Stage Neural Re-ranking Pipeline:





First-pass retrieval using BM25 to generate candidate documents.



Second-stage re-ranking with two BERT-based models:





MonoBERT (Pointwise): A cross-encoder scoring individual query-document relevance for precise ranking.



DuoBERT (Pairwise): A model comparing document pairs (doc_i, doc_j) per query to refine ranking accuracy.



Rigorous Evaluation: Compares performance across BM25, TF-IDF, RM3, SBERT-Expansion, MonoBERT, and DuoBERT using metrics like nDCG, MAP, and P@10.



Interactive Demonstration: Deployed as a Gradio web interface for real-time queries, enabling side-by-side model comparisons.
