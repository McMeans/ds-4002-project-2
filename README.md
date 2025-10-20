# Predicting Stock Movements Using Twitter Sentiment Analysis

## Overview
This project explores how public sentiment on X (formerly Twitter) can be used to predict stock price movements. By combining **natural language processing (NLP)** and **financial market data**, the project seeks to quantify the relationship between investor opinions and next-day stock performance.

**Goal Statement:** Build a supervised machine learning model that predicts end-of-day stock trends based on tweets from the prior day, targeting an accuracy of **at least 85%**.

**Research Question:** Can NLP of tweets containing stock ticker symbols (e.g., `$AAPL`) be used to forecast next-day market performance?

## Contents of the Repository
The repository includes:
- **Software and platform section** – the type(s) of software used for the project, names of any add-on packages that need to be installed with the software, and the platform (e.g., Windows, Mac, or Linux) used
- **A map of our documentation** – an outline or tree illustrating the hierarchy of folders and subfolders contained in your Project Folder and the files stored in each folder or subfolder
- **Instructions for reproducing our results** – explicit step-by-step instructions to reproduce the Results of our study

## Section 1: Software and Platform Information
**Programming Language:** Python 3.10+  
**Primary Platform:** Windows 11 (reproducible on macOS and Linux)  

### Core Libraries and Packages
- `pandas` — data manipulation and cleaning  
- `numpy` — numerical operations  
- `matplotlib`, `seaborn` — data visualization  
- `vaderSentiment` — sentiment analysis tool  
- `yfinance` — financial data collection  
- `requests`, `json` — API calls and response parsing  
- `scikit-learn` — supervised learning and model evaluation  


### Installation
All dependencies can be installed by running:

```
pip install -r requirements.txt
```

## Section 2: Map of the Documentation
### Folder Hierarchy
```
Top Level Directory
│
├── README.md .................. Project overview and replication guide
├── LICENSE.md ................. MIT open-source license
│
├── DATA/
│   ├── <ticker>_tweets.csv .... Tweets collected for that stock
│   ├── <ticker>_prices.csv .... Historical price data from yfinance
│   └── ...
│
├── SCRIPTS/
│   ├── data_collection.py ..... Collects raw data via APIs
│   ├── data_cleaning.py ....... Cleans tweets & merges datasets
│   ├── sentiment_analysis.py .. Calculates sentiment scores using VADER
│   ├── modeling.py ............ Trains supervised ML models
│   ├── visualization.py ....... Creates plots for EDA & results
│   └── run_all.sh ............. Shell script to reproduce everything
│
├── OUTPUT/
│   ├── sentiment_vs_price.png . Example visualization
│   ├── model_results.csv ...... Evaluation metrics
│   └── final_model.pkl ........ Saved machine learning model
│
└── requirements.txt ........... List of dependencies
```

## Section 3: Instructions for Reproducing the Results
Follow these steps to replicate the full analysis and reproduce the model results.

### Step 1: Clone the Repository
```
git clone https://github.com/<your-username>/Predicting-Stock-Movements-Twitter-Sentiment.git
cd Predicting-Stock-Movements-Twitter-Sentiment
```

### Step 2: Install Dependencies
Ensure Python 3.10+ is installed, then run:
```
pip install -r requirements.txt
```

### Step 3: Collect Data
Run the script that pulls both stock price data and tweet data via APIs:
```
python SCRIPTS/data_collection.py
```
- This script uses `yfinance` to fetch daily stock prices.
- It also uses `twitterapi.io` to retrieve tweets containing ticker symbols (e.g., `$AAPL`).

### Step 4: Clean and Prepare Data
```
python SCRIPTS/data_cleaning.py
```
This removes irrelevant columns, non-English tweets, links, and emojis, and merges datasets by date.

### Step 5: Conduct Sentiment Analysis
```
python SCRIPTS/sentiment_analysis.py
```
Uses the VADER package to compute positive, negative, and neutral sentiment scores for each tweet, then aggregates them into a daily sentiment score per stock.

### Step 6: Train and Evaluate Models
```
python SCRIPTS/modeling.py
```
- Builds supervised learning models (Linear Regression, Random Forest, Gradient Boosting)
- Evaluates models using accuracy, precision, recall, and F1 score
- Saves the best-performing model (`final_model.pkl`) in the `OUTPUT/` folder.

### Step 7: Generate Visualizations
```
python SCRIPTS/visualization.py
```
Creates plots for:
- Average sentiment vs. daily stock price change
- Tweet engagement vs. volatility
Outputs are saved to `/OUTPUT/`.


### Step 8: Automate Full Workflow
To reproduce the entire pipeline in one step:
```
bash SCRIPTS/run_all.sh
```