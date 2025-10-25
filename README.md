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
**Primary Platform:** Windows and macOS (reproducible on Linux)  

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

```bash
pip install -r requirements.txt
```

## Section 2: Map of the Documentation
### Folder Hierarchy
```
ds-4002-project-2
│
├── README.md .... Project overview and replication guide
├── LICENSE.md ... MIT open-source license
│
├── data/
│   ├── <ticker>/ (for each)
│   ├──── <ticker>_tweets_raw.csv ... Tweets collected for that stock
│   ├──── <ticker>_market_raw.csv ... Historical price data from yfinance
│   ├──── <ticker>_tweets_clean.csv . Cleaned tweets for EDA
│   ├──── <ticker>_market_clean.csv . Cleaned price data for EDA
│   ├──── <ticker>_sentiment.csv .... Historical price data from yfinance
│   ├── README.md ................... Metadata
│   ├── eda_plot1.png ............... Plot for metadata
│   └── eda_plot2.png ............... Plot for metadata
│
├── scripts/
│   ├── stock_data_retrieval.ipynb ... Collects raw price data
│   ├── twitter_data_retrieval.ipynb . Collects raw X data
│   ├── cleaning_eda.ipynb ........... Cleans datasets & does basic plots
│   ├── sentiment_analysis.ipynb ..... Calculates sentiment scores using VADER
│   └── stock_prediction.ipynb ....... Modeling, prediction, and visualization
│
├── output/
│   ├── <ticker> (for each)
│   ├──── <ticker>_best_model.joblib .... Saved best performing model
│   ├──── <ticker>_confusion_matrix.png . Best model's confusion matrix
│   ├──── <ticker>_model_metadata.json .. Metadata of saved model
│   ├──── <ticker>_prediction.csv ....... Final dataset with predictions
│   ├──── <ticker>_pred_vs_actual.png ... Plot of predicted vs actual values
│   └──── <ticker>_scaler.joblib ........ Pre-processing scaler for best model
│
└── requirements.txt ... List of dependencies
```

## Section 3: Instructions for Reproducing the Results
Follow these steps to replicate the full analysis and reproduce the model results.

### Step 1: Clone the Repository
```bash
git clone https://github.com/McMeans/ds-4002-project-2.git
cd ds-4002-project-2
```

### Step 2: Install Dependencies
Ensure Python 3.10+ is installed, then run:
```bash
pip install -r requirements.txt
```

### Step 3: Collect Data

**NOTE**: We recommend you to use the provided data in the `data` folder.`twitterapi.io` requires you to use an API key, and this process will cost you both money and time. (It took us over three hours to get the raw twitter data for each stock).

If you still wish to proceed, create a `.env` file inside `scripts` and set `TWITTERAPI_API_KEY` to your API key. Run the data retrieval notebooks that pulls stock price data and tweet data via APIs:
- `stock_data_retrieval.ipynb` uses `yfinance` to fetch daily stock prices.
- `twitter_data_retrieval.ipynb` uses `twitterapi.io` to retrieve tweets containing ticker symbols (e.g., `$AAPL`).

In the configuration file, you can set which stocks you want to retrieve data from. Adjust as desired.

### Step 4: Clean and Prepare Data
Run all cells in `scripts/cleaning_eda.ipynb` for each stock (update `ticker` variable for each iteration).

This prepares data for sentiment analysis, removing irrelevant columns and non-English tweets.

### Step 5: Conduct Sentiment Analysis
Run all cells in `scripts/sentiment_analysis.ipynb` for each stock (update `ticker` variable for each iteration).

Uses the VADER package to compute positive, negative, and neutral sentiment scores for each tweet, then aggregates them into a daily sentiment score per stock. Also saves the closing, next opening, and difference of the stock price during this period.

### Step 6: Train and Evaluate Models
Run all cells in `scripts/stock_prediction.ipynb` for each stock (update `stock` variable for each iteration).
- Builds supervised learning models (Logistic Regression, Random Forest, Gradient Boosting, etc.)
- Evaluates models using accuracy, precision, recall, and F1 score
- Saves the best-performing model, final dataset, and relevant plots in the `output/` folder (see folder hierarchy above).