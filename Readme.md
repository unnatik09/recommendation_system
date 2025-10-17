# Boomm Post Recommendation System

## Overview
This project implements a **hybrid post recommendation system** for Boomm, a social platform focused on finance and community. The system suggests relevant posts to users using a combination of:

- **Content-based filtering** (semantic similarity between user interests and post content)  
- **Collaborative filtering** (based on similar users’ interactions)  
- **Popularity and recency metrics** (engagement and freshness)

---

## Datasets
- `Assessment data - users.csv`: Contains user information and interests (`user_id`, `interested_in`)  
- `Assessment data - posts.csv`: Contains post metadata (`post_id`, `content`, `likes`, `shares`, `reports`, `created_at`, `like_user_ids`, `topics`)

---

## Methodology

### 1. Data Preprocessing
- Filled missing user interests and post engagement metrics
- Lowercased and cleaned text
- Converted `created_at` to datetime

### 2. Feature Engineering
- **Popularity Score**: Weighted sum of likes, shares, and reports  
- **Recency Score**: Normalized post age  
- **Semantic Score**: Cosine similarity of BERT embeddings between user interests and post content  
- **Collaborative Score**: Weighted recommendations from similar users’ likes

### 3. Hybrid Recommendation
- **Final Score** per user-post: final_score = 0.5semantic + 0.25popularity + 0.15recency + 0.1collaborative
- Users with no interests get higher weight on popularity and recency  
- Top 10 posts per user are selected based on final score

---

## Outputs
- `boomm_recommendations.csv`: Recommended post IDs (comma-separated) for each user  
- Visualizations (Plotly) for semantic, popularity, recency, and final scores  

---

## Usage
1. Clone the repository
2. Install required packages:
```bash
pip install pandas numpy plotly sentence-transformers scikit-learn
