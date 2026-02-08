# mind-kg-news-recommender

## Project Structure

knowledge-graph-based-news-recommender system/
<br>
|--- data/ # Raw and processed datasets
<br>
| |--- raw/ # Original dataset (read-only)
<br>
| |--- processed/ # Generated data
<br>
|--- src/ # Core source code
<br>
| |--- kg/ # Knowledge graph construction
<br>
| |--- models/ # User and news representations
<br>
| |--- recommender/ # Candidate generation and ranking
<br>
| |--- evaluation/ # Metrics and evaluation logic
<br>
| |--- notebooks/ # Data exploration and analysis
<br>
|--- README.md
<br>
|--- main.py # End-to-end pipeline entry point

## Overview

This repository implements a knowledge graph–based news recommendation pipeline using entity-level representations from the MIND dataset.
<br>
The system models users and news articles through entities and relations to improve semantic relevance beyond keyword matching.

## Motivation

Traditional content-based and collaborative filtering methods struggle with semantic understanding and cold-start scenarios.
<br>
This project explores how knowledge graphs and entity embeddings can be used to enhance news recommendation quality.

## Dataset

The project uses the MIND news recommendation dataset.
<br>
Files:
- news.tsv – news articles and associated entities
- behaviors.tsv – user click histories
- entity_embedding.vec – pre-trained entity embeddings
- relation_embedding.vec – pre-trained relation embeddings
<br>
Raw data is stored under data/raw/ and is not modified.

## Pipeline Overview

User Click History
<br>
|
<br>
Entity Extraction
<br>
|
<br>
Knowledge Graph Construction
<br>
|
<br>
User & News Representation
<br>
|
<br>
Candidate Generation
<br>
|
<br>
Ranking & Recommendation

## Limitations
Uses pre-trained embeddings without fine-tuning
<br>
No real-time recommendation support
<br>
Candidate generation is heuristic-based
