# Goodreads NYT Bestseller Predictor

An end-to-end Machine Learning pipeline that uses Sentiment Analysis on reader reviews to predict whether a book will become a New York Times Bestseller.

## Project Overview
This project processes over 6 million book reviews using **VADER Sentiment Analysis** and trains a **LightGBM Classifier** to identify commercial success based on community engagement and sentiment volatility.

### Handling Temporal Leakage
A common pitfall in bestseller prediction is "Data Leakage"—where the model uses future information to predict the past. To ensure the integrity of our results, I implemented the following:

1. **Leave-One-Out (LOO) Encoding for Author Reputation:** Instead of using the author's total bestseller count, I calculated a "Leave-One-Out" feature. This ensures that for any book $X$, the reputation feature only considers the author's *other* successful titles, preventing the target variable from leaking into the training features.

2. **Sentiment Proxy:** We acknowledge that review sentiment and volume are collected over the book's lifetime. In a production environment, this model would be used as a "Post-Launch Monitor" (30-60 days after release) to predict long-term NYT list endurance.

<<<<<<< HEAD
## Performance & Results
The tuned **LightGBM Classifier** significantly outperformed the Logistic Regression baseline, specifically in its ability to identify the "top" commercial successes.

- **AUC-ROC:** 0.8282
- **Precision@100:** 0.96 (96 of the top 100 predicted books were actual NYT bestsellers)
- **F1-Score Improvement:** 88% increase over the baseline model.

### **Top Predictive Features:**
1. **Author Reputation:** (LOO-encoded historical success)
2. **Average Sentiment:** (VADER compound scores)
3. **Engagement Volume:** (Ratings and review counts)
4. **Series Status:** (Whether the book is part of a series)
=======
## Advanced Modeling Features
This notebook has been updated to include rigorous academic standards:
* **Handling Extreme Imbalance:** Implemented **Focal Loss** objective and **SMOTE** oversampling to manage the 1:47 bestseller class imbalance.
* **Multimodal Feature Set:** A 117-feature model combining TF-IDF text features, VADER/TextBlob sentiment metrics, and book metadata.
* **Statistical Rigor:** Included **VIF (Variance Inflation Factor)** checks for multicollinearity and **Ablation Studies** to justify feature selection.
* **Performance at Scale:** Evaluation focused on **P@K (Precision at K)** curves, showing 97% precision at the Top 500 recommendation level.

## 📈 Performance & Key Insights
The final model was evaluated using **Stratified 5-Fold Cross-Validation** to ensure stability across the imbalanced classes.

* **AUC-ROC:** 0.8646 (Exceeds report baseline of 0.8282)
* **Precision@100:** 97% (Highly reliable top-tier predictions)
* **Precision@500:** 97% 
* **F1 Macro:** 0.5777 (Significantly improved via Focal Loss)

### Key Predictors of Success
1. **Engagement Momentum:** `ratings_count` and `review_count` are the primary drivers, confirming that community volume is a prerequisite for NYT status.
2. **Sentiment Volatility (`vader_std`):** Higher variance in review sentiment is a strong signal for bestsellers, suggesting that "polarizing" books generate more commercial "buzz."
3. **Institutional Power (`is_big5`):** Publication by a "Big 5" publisher remains a statistically significant advantage even when controlling for reader sentiment.
4. **Thematic Signals:** TF-IDF analysis of descriptions revealed that specific genre-linked keywords (captured in the top 100 features) provide critical thematic context that sentiment alone misses.
>>>>>>> f85ec24 (Final: Advanced modeling with Focal Loss, VIF check, and P@K evaluation)

## Repository Structure
- `01_Data_Acquisition.ipynb`: Memory-efficient data loading and cleaning.
- `02_Merging_and_Sentiment.ipynb`: Matching Goodreads data with NYT lists.
- `03_Sentiment_Analysis.ipynb`: Chunked NLP processing using VADER.
- `04_Modeling_and_Evaluation.ipynb`: Gradient Boosting and model metrics.

## Data Source
Due to file size constraints, the raw data is not included in this repository. You can download the datasets here:
- **UCSD Book Graph:** [Link to Dataset](https://sites.google.com/eng.ucsd.edu/ucsdbookgraph/home)
- Required files: `goodreads_books.json.gz` and `goodreads_reviews_dedup.json.gz`.

<<<<<<< HEAD
## Installation & Usage
1. Clone the repo: `git clone https://github.com/SnoopyOnMain/Goodreads-NYT-Bestseller-Predictor`
2. Install dependencies: `pip install -r requirements.txt`
3. Place the downloaded `.gz` files into the `data/` folder.
4. Run the notebooks in sequential order.
=======
## Installation and Usage
1. Clone the repo: `git clone https://github.com/YOUR_USERNAME/Goodreads-Predictor.git`
2. Create and activate a virtual environment:
   - Windows: `python -m venv venv; .\venv\Scripts\activate`
   - Mac/Linux: `python3 -m venv venv; source venv/bin/activate`
3. Install dependencies: `pip install -r requirements.txt`
4. Place the downloaded `.gz` files into a `/data` folder in the root directory.
5. Run the notebooks in sequential order.
>>>>>>> f85ec24 (Final: Advanced modeling with Focal Loss, VIF check, and P@K evaluation)
