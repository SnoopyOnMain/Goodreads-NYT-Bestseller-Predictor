# Goodreads NYT Bestseller Predictor

An end-to-end Machine Learning pipeline that uses Sentiment Analysis on reader reviews to predict whether a book will become a New York Times Bestseller.

## Project Overview
This project processes over 6 million book reviews using **VADER Sentiment Analysis** and trains a **LightGBM Classifier** with a **Custom Focal Loss** objective to identify commercial success despite extreme class imbalance (1:47).

### Handling Temporal Leakage
To ensure the integrity of our results, I implemented:
1. **Leave-One-Out (LOO) Encoding:** For any book $X$, author reputation only considers *other* titles by that author, preventing the target from leaking into features.
2. **Post-Launch Framework:** This model acts as a "30-60 Day Monitor" to predict long-term NYT list endurance based on initial community momentum.

## Advanced Modeling Features
This pipeline incorporates rigorous academic standards discussed in the project report:
* **Handling Extreme Imbalance:** Implemented **Focal Loss** and **SMOTE** oversampling.
* **Multimodal Feature Set:** A 117-feature model combining TF-IDF, VADER/TextBlob sentiment, and metadata.
* **Statistical Rigor:** Performed **VIF (Variance Inflation Factor)** checks for multicollinearity and **Ablation Studies**.
* **Performance at Scale:** Evaluation focused on **P@K (Precision at K)** curves, showing near-perfect accuracy for the top predicted books.

## Performance & Key Insights
The model was evaluated using **Stratified 5-Fold Cross-Validation**.

* **AUC-ROC:** 0.8646 (Exceeds baseline of 0.8282)
* **Precision@100:** 97% 
* **Precision@500:** 97% 
* **F1 Macro:** 0.5777 (Significantly improved via Focal Loss)

### Key Predictors of Success
1. **Engagement Momentum:** `ratings_count` and `review_count` are the strongest prerequisite signals.
2. **Sentiment Volatility (`vader_std`):** Higher variance in review sentiment suggests "polarizing" books generate more commercial buzz.
3. **Institutional Power (`is_big5`):** Publication by a "Big 5" publisher remains a statistically significant advantage.

## Repository Structure
- `01_Data_Acquisition.ipynb`: Memory-efficient data loading and cleaning.
- `02_Merging_and_Sentiment.ipynb`: Matching Goodreads data with NYT lists.
- `03_Sentiment_Analysis.ipynb`: Chunked NLP processing using VADER.
- `04_Modeling_and_Evaluation.ipynb`: Gradient Boosting, Focal Loss, and P@K metrics.

## Data Source
Due to file size constraints, raw data is not included. 
- **Source:** [UCSD Book Graph](https://sites.google.com/eng.ucsd.edu/ucsdbookgraph/home)
- **Required Files:** `goodreads_books.json.gz` and `goodreads_reviews_dedup.json.gz` (Place in a `/data` folder).

## Installation & Usage
1. Clone the repo: `git clone https://github.com/SnoopyOnMain/Goodreads-NYT-Bestseller-Predictor`
2. Create and activate a virtual environment:
   - Windows: `python -m venv venv; .\venv\Scripts\activate`
   - Mac/Linux: `python3 -m venv venv; source venv/bin/activate`
3. Install dependencies: `pip install -r requirements.txt`
4. Run notebooks in sequential order.
