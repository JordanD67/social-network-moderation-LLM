# Reddit Moderation Solution: Toxicity Scoring and Graph Analysis (DSA Compliance)

## Project Context
This repository contains the final deliverable for the **Graph Theory & Social Network Analysis (2024)** course at IMT Atlantique.  
The project's objective was to develop a proactive system for alerting Reddit community managers to inappropriate and illegal content, primarily driven by the **Digital Services Act (DSA)** regulation (October 19, 2022), which mandates stricter online content regulation.

> ⚠️ Note: Due to their large size, not all datasets used in the analysis are included in this repository. Only representative subsets and scripts are provided.

Our solution provides a **dual analysis**—using **toxicity scores** and **graph theory**—to identify high-risk content and user communities.

---

## Feature Details

| Feature | Detail |
|---------|--------|
| **Primary Goal** | Suggest new ways to alert community managers of inappropriate behavior to ensure DSA compliance |
| **Data Scope** | Reddit posts and comments focused exclusively on climate-related discussions |
| **Toxicity Model** | Pre-trained BERT model (`unitary/toxic-bert`) to score comments from 0 (non-toxic) to 1 (very toxic) |
| **Graph Model** | Undirected, weighted graph representing user interactions (comments/replies) |

---

## Methodology and Data Analysis

### 1. Data Characterization
- The analysis began with four datasets covering climate-focused subreddits, posts, and comments.  
- **Subreddits:** Data covers 64 subreddits, with 24 identified as active (e.g., `climateskeptics`, `climatechange`, `ClimateOffensive`).  
- **Volume:** The comment dataset contains 337,817 comments across multiple languages (English, German, French), requiring a multilingual toxicity model.  
- **Peak Activity:** Posting peaks at 16:00 (4 PM) and commenting peaks at 17:00 (5 PM). Moderation efforts should focus during these peak hours.

### 2. Toxicity Scoring and User Prioritization
- Toxicity scores were computed using the multilingual `unitary/toxic-bert` model.  
- **Distribution:** Most comments have low toxicity, allowing moderators to focus on high-scoring content.  
- **Threshold Selection:** A toxicity threshold of 0.7 filters ~5.21% of comments (≈17,600 comments) for review, made by 8,483 unique users.  
- **Pareto Principle:** A small subset of users is responsible for a disproportionately large share of toxic comments: 50% of all potentially toxic comments (score > 0.7) come from ~1,000 users.  
- **Top Users:** The 6 most toxic users (including one deleted account) contributed significantly more toxic comments, confirming that moderation should focus on high-risk users.

### 3. Graph Theory for Community Detection
- To comply with DSA requirements, interactions were modeled as a graph, as users engaged in illegal activities often cluster together.  
- **Graph Construction:**  
  - **Nodes:** Individual Reddit users  
  - **Edges:** Interactions (comments/replies)  
  - **Weight:** Number of interactions  
  - **Filtering:** Only edges with ≥5 interactions included  
- **Community Detection:** Clusters help moderators identify groups of users sharing similar beliefs or participating in inappropriate activities.  
- **Proactive Intervention:** Linking toxic users to their cluster enables faster identification and potential removal of other dangerous users in the same community.

---

## Conclusion and Recommendations
The implemented dual-analysis model provides a powerful solution for modern social media moderation:

- **Real-time Content Alert:** Provide moderators with toxicity scores immediately after publication, enabling quick intervention.  
- **Targeted User Intervention:** Alert moderators about users with high toxicity and their associated clusters.  
- **Adaptability:** The BERT model can be retrained or replaced (e.g., with LIAR or ETHOS datasets) to detect specific illegal content types, such as fake news or hate speech.

> Reminder: Large raw datasets are not included in this repository due to their size.
