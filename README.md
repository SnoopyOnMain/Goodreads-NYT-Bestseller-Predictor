# Goodreads NYT Bestseller Predictor

An end-to-end Machine Learning pipeline that uses Sentiment Analysis on reader reviews to predict whether a book will become a New York Times Bestseller.

## Project Overview
This project processes over 6 million book reviews using **VADER Sentiment Analysis** and trains a **LightGBM Classifier** to identify commercial success based on community engagement and sentiment volatility.

### Handling Temporal Leakage
A common pitfall in bestseller prediction is "Data Leakage"—where the model uses future information to predict the past. To ensure the integrity of our results, I implemented the following:

1. **Leave-One-Out (LOO) Encoding for Author Reputation:** Instead of using the author's total bestseller count, I calculated a "Leave-One-Out" feature. This ensures that for any book $X$, the reputation feature only considers the author's *other* successful titles, preventing the target variable from leaking into the training features.

2. **Sentiment Proxy:** We acknowledge that review sentiment and volume are collected over the book's lifetime. In a production environment, this model would be used as a "Post-Launch Monitor" (30-60 days after release) to predict long-term NYT list endurance.

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

## Repository Structure
- `01_Data_Acquisition.ipynb`: Memory-efficient data loading and cleaning.
- `02_Merging_and_Sentiment.ipynb`: Matching Goodreads data with NYT lists.
- `03_Sentiment_Analysis.ipynb`: Chunked NLP processing using VADER.
- `04_Modeling_and_Evaluation.ipynb`: Gradient Boosting and model metrics.

## Data Source
Due to file size constraints, the raw data is not included in this repository. You can download the datasets here:
- **UCSD Book Graph:** [Link to Dataset](https://sites.google.com/eng.ucsd.edu/ucsdbookgraph/home)
- Required files: `goodreads_books.json.gz` and `goodreads_reviews_dedup.json.gz`.

## Installation & Usage
1. Clone the repo: `git clone https://github.com/SnoopyOnMain/Goodreads-NYT-Bestseller-Predictor`
2. Install dependencies: `pip install -r requirements.txt`
3. Place the downloaded `.gz` files into the `data/` folder.
4. Run the notebooks in sequential order.
