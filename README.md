<p align="center">
  <img src="https://github.com/gokulbytes/readme-images/blob/main/kars2019.png">
</p>

# Knowledge Graph-Based News Recommender

This project implements a sophisticated news recommendation engine that leverages a Knowledge Graph (KG) to bridge the gap between simple collaborative filtering and semantic content understanding. By mapping users, news articles, and Wikidata entities into a unified relational structure, the system provides highly relevant, discovery-oriented recommendations.

## What id does?

Traditional recommenders often suffer from the "filter bubble" or "cold start" problems. This system solves those by using a Multi-Relational Knowledge Graph:
- __Semantic Mapping__: It doesn't just look at word frequency; it identifies specific Wikidata Entities (e.g., people, places, organizations) within the news.
- __Relational Reasoning__: It connects users to news they’ve clicked, and then connects that news to its categories and underlying entities.
- __Vector Space Similarity__: It utilizes high-dimensional Knowledge Graph Embeddings `entity_embedding.vec` to calculate the mathematical similarity between a user’s historical interests and new, unread content.
- Path-Based Discovery: It can recommend news that a user hasn't seen before by following paths `User -> Clicked News -> Entity (e.g., ElonMusk) -> New News mentioning ElonMusk.`

## System Architecture
The recommender is built on three core pillars:
- __NetworkX Graph__: A heterogeneous graph storing relationships (clicked, mentions, belongs_to).
- __News Metadata__: Processed news titles and categories for human-readable output.
- __Embedding Layer__: Pre-trained vectors that allow the system to understand that two different entities might be related (e.g., "Apple" and "Steve Jobs").

### How to integrate into any system?

Integrating a Knowledge Graph-Based Recommender into an existing production environment requires a shift from traditional linear data processing to a relational approach. Since the graph is already constructed the models are ready saved, the integration focuses on deployment, retrieval, and feedback loops.
<br>
<br>
__Step 1__: Model Deployment and Environment Setup
<br>
Before the system can serve recommendations, the serialized models must be accessible to the application server. This involves moving the large graph and embedding files to a cloud storage bucket or a dedicated directory on the production server. The environment must be configured with specific graph-processing libraries to ensure the relational structure of the data is preserved when loaded into memory.
<br>
<br>
__Step 2__: User-to-Graph Mapping
<br>
When a request for a recommendation is made, the system must first identify the user within the Knowledge Graph. If the user is an existing member of the dataset, the system maps their unique identifier to a node in the graph. If the user is new (a "cold start" scenario), the system must have a logic bridge to map them to the graph through their initial preferences or by connecting them to general "Category" nodes instead of specific news history.
<br>
<br>
__Step 3__: Semantic Interest Profiling
<br>
Once the user is identified, the system traverses the graph to find all "Neighbor" nodes. It looks at the news articles the user has clicked and extracts the associated entities (like specific people or organizations) and categories. By accessing the pre-loaded embeddings, the system calculates a central "Interest Vector" that represents the user's current semantic focus in a multi-dimensional space.
<br>
<br>
__Step 4__: Candidate Generation and Ranking
<br>
The system does not score every article in the database, as this would be too slow. Instead, it uses the Knowledge Graph to find candidates through "path-walking." It identifies new articles that are one or two steps away from the user's interests (e.g., articles mentioning the same entities). These candidates are then ranked by calculating the distance between the article's entity vectors and the user's profile vector.
<br>
<br>
__Step 5__: Metadata Enrichment and Delivery
<br>
After the top results are ranked by their numerical scores, the system replaces the raw identifiers (like News IDs) with human-readable metadata. It pulls the titles, categories, and image URLs from the metadata storage to format a clean response. This structured information is then sent back to the front-end for the user to view.
<br>
<br>
__Step 6__: The Feedback Loop (Real-time Updates)
<br>
To remain accurate, the system must be integrated with your telemetry data. Every time a user clicks a recommended article, that interaction should be sent back to the Knowledge Graph. This creates a new edge in the graph, ensuring that the user's profile evolves in real-time. Periodically, the entire graph is re-saved to ensure that new news articles and new user connections are persistently stored.
