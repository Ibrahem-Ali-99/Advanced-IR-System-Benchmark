# Advanced Information Retrieval: A Comparative Analysis of Classic and Neural Models

## Overview

This project implements and critically evaluates a multi-stage Information Retrieval (IR) system, benchmarking classic retrieval techniques against modern neural network architectures. Using the **PyTerrier** framework and the standard **Vaswani** dataset, this work explores the practical trade-offs and performance nuances of various models, from TF-IDF baselines to sophisticated BERT-based re-rankers.

The primary goal was not just to build a system, but to analyze why certain advanced techniques succeed or fail, providing valuable insights into the practical application of neural IR.

## Key Features & Technical Implementation

### 1. Classic IR Foundation
- **Indexing:** A robust inverted index was constructed from the Vaswani collection using PyTerrier's flexible indexing capabilities.
- **Baselines:** Established strong performance baselines with standard retrieval models, including **TF-IDF** and **Okapi BM25**, to ensure a fair comparison for more advanced methods.

### 2. Advanced Query Expansion Techniques
- **Classic Pseudo-Relevance Feedback:** Implemented and evaluated **RM3**, a powerful and widely-used query expansion model that enriches queries with salient terms from top-ranked documents.
- **Neural Query Expansion:** Engineered a custom query expansion technique using **Sentence-BERT (SBERT)** embeddings. This method identifies semantically similar expansion terms from an initial document set, moving beyond simple keyword matching.

### 3. Two-Stage Neural Re-ranking Pipeline
A "retrieve-and-rerank" pipeline was built to leverage the efficiency of classic models and the contextual power of Transformers.
- **First Stage (Candidate Retrieval):** Utilized BM25 to efficiently retrieve an initial set of 100 candidate documents for each query.
- **Second Stage (Neural Re-ranking):** Implemented and benchmarked two powerful, out-of-the-box BERT-based re-ranking models:
    - **MonoBERT (Pointwise):** A cross-encoder that individually scores the relevance of each query-document pair, providing a deep contextual understanding.
    - **DuoBERT (Pairwise):** A more advanced model that learns relative preferences by comparing pairs of documents (e.g., is `doc_i` more relevant than `doc_j` for this query?), aiming for a more accurate final ranking.

### 4. Rigorous Evaluation & Performance Analysis
A comprehensive evaluation was conducted comparing all implemented systems using standard IR metrics. The results provided surprising and important insights into the behavior of pre-trained neural models when applied without task-specific fine-tuning.

#### **Performance on the Vaswani Dataset**

| Model                      | MAP vs. Baseline | nDCG vs. Baseline | P@10 vs. Baseline |
| :------------------------- | :--------------- | :---------------- | :---------------- |
| BM25                       | +0.10%           | +0.24%            | +0.00%            |
| **BM25 + RM3**             | **+0.46%**       | **+0.30%**        | **-3.68%**        |
| BM25 + Neural QE           | -12.00%          | -3.90%            | -12.63%           |
| BM25 >> MonoBERT (Top 100) | -61.10%          | -43.78%           | -58.42%           |
| BM25 >> DuoBERT (Top 100)  | -64.17%          | -45.47%           | -61.05%           |

*(Baseline: TF-IDF)*

#### **Key Analytical Insights**
- **Classic Methods Remain Robust:** The classic `BM25 + RM3` model proved to be the most effective system "out-of-the-box," demonstrating that well-established IR techniques are still highly competitive.
- **The "Domain Gap" Challenge:** The most significant finding was the **critical failure of the pre-trained BERT re-rankers**. Despite being powerful language models, their poor performance highlights a crucial concept: without fine-tuning on a relevant task (like the MS MARCO passage ranking dataset), general-purpose models lack the specific knowledge to effectively rank documents for relevance. They understand language, but not the *task* of ranking.
- **Neural QE Underperformance:** The SBERT-based query expansion also failed to improve results, likely due to introducing noisy, semantically-related but contextually-irrelevant terms.

This project serves as a practical demonstration that simply applying larger, more complex neural models does not guarantee better performance. It underscores the importance of **fine-tuning** and **domain adaptation** for achieving state-of-the-art results in neural search.

### 5. Interactive Demonstration
To showcase the full system, a user-friendly web interface was built using **Gradio**. This demo allows for real-time queries and a side-by-side comparison of the different retrieval models, making the performance differences tangible and easy to explore.
