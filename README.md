# Goodreads NYT Bestseller Predictor

An end-to-end Machine Learning pipeline that uses Sentiment Analysis on reader reviews to predict whether a book will become a New York Times Bestseller.

## Project Overview
This project processes over 6 million book reviews using **VADER Sentiment Analysis** and trains a **LightGBM Classifier** to identify commercial success based on community engagement and sentiment volatility.

## Performance
- **AUC-ROC:** 0.82 (approx)
- **Precision@100:** 96%
- **Key Features:** Average Sentiment, Sentiment Volatility, and Engagement Metrics.

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
1. Clone the repo: `git clone https://github.com/YOUR_USERNAME/Goodreads-Predictor.git`
2. Install dependencies: `pip install -r requirements.txt`
3. Place the downloaded `.gz` files into the `data/` folder.
4. Run the notebooks in sequential order.