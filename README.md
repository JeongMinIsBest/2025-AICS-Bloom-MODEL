# 2025 AICS Bloom AI Stock Model 📈

## 🏗 Project Overview
This project aims to **build a real-time prediction system** that **predicts stock prices of the top 10 KOSPI-listed companies** based on **temperature and precipitation data from Jeonju, Jeollabuk-do**.
For this purpose, **an XGBoost model was used for training**, and a **real-time data collection and prediction system** was implemented.
</br>
</br>

## 🛠 Key Technologies and Libraries
- Data collection: ```FinanceDataReader```, ```Korea Meteorological Administration (KMA) API```
- Data preprocessing and analysis: ```pandas, numpy```, ```scikit-learn```
- Machine learning model: ```XGBoost```
- Visualization: ```matplotlib```, ```seaborn```
</br>
</br>

## 🔍 Process Description

### 1️⃣ Data Collection and Preprocessing

#### 📌 Stock Price Data Collection
- Stock price data for the top 10 KOSPI-listed companies were collected using ```FinanceDataReader```.
- Main columns: Open, High, Low, Close, Volume
- Data period: 2024-01-01 – 2024-12-31

#### 📌 Weather Data Collection
- Temperature (°C) and precipitation (mm) data for Jeonju, Jeollabuk-do were collected using the Korea Meteorological Administration API.
- Data preprocessing was performed using ```pandas```, and the data were merged with stock price data based on date.
</br>

### 2️⃣ Feature Engineering
Various features were added to improve stock price prediction performance.

#### 📌 1. Adding Price Change and Volatility Features
- ```Change```: (Close - Open) → ```Daily stock price change```
- ```ChangeRatio```: (Change / Open) × 100 → ```Price change rate (%)```

#### 📌 2. Creating Features Based on Historical Data
- ```Prev_Close```: Added the previous day’s closing price to enable comparison with the current price.
- ```Price_Change```: (Current close - Previous close) / Previous close → ```Day-over-day price change rate```

#### 📌 3. Adding Volume-Based Features
- ```Prev_Volume```: Added the previous day’s trading volume.
- ```Volume_Change```: (Current volume - Previous volume) / Previous volume → ```Volume change rate```

#### 📌 4. Adding Moving Averages
- ```Moving_Avg_5```: 5-day moving average (short-term trend)
- ```Moving_Avg_10```: 10-day moving average
- ```Moving_Avg_20```: 20-day moving average (long-term trend)

#### 📌 6. Adding Weekday Information
- ```Weekday```: Added weekday information (0: Monday ~ 6: Sunday).
- Enabled the model to learn differences in stock price patterns by weekday.

#### 📌 7. One-Hot Encoding of Stock Tickers
- Stock tickers were converted using One-Hot Encoding so that the model could learn characteristics specific to each stock.

#### 📌 8. Data Normalization (MinMax Scaling)
- All features were normalized to a 0–1 range to optimize model training.
</br>

### 3️⃣ XGBoost Model Training
- ```Input variables```: Stock price data (Open, High, Low, Close, Volume) + temperature + precipitation
- ```Output variable```: Predicted Close price
- Model evaluation was conducted using ```MSE (Mean Squared Error)```, ```RMSE (Root Mean Squared Error)```, and ```R² Score```.
</br>

#### 4️⃣ Real-Time Prediction System Implementation
- Designed to predict stock prices in real time by inputting the latest temperature and precipitation data.
- Structured to allow integration of prediction results with APIs or services.
</br>

## 🧩 Data Sources Used
| Dataset | Period / Region | Source | Link |
|:------:|:---------------:|:------:|:----:|
| Precipitation | 2024.01 – 2024.12 / Jeonju, Jeollabuk-do | KMA Open Data Portal | https://data.kma.go.kr/stcs/grnd/grndRnList.do?pgmNo=69 |
| Temperature | 2024.01 – 2024.12 / Jeonju, Jeollabuk-do | KMA Open Data Portal | https://data.kma.go.kr/stcs/grnd/grndTaList.do?pgmNo=70 |
| Top 10 KOSPI Stocks | 2024.01 – 2024.12 | KRX | FinanceDataReader |
<br/>
<br/>

## 📁 Repository Structure
```
StockPrediction
│
├ main.py
├ requirements.txt
├ 0213_xgboost_stock_model.json
│
├ Data
│   ├ Stock
│   ├ Weather
│   └ 최종데이터셋.csv
│
└ README.md
```
</br>
</br>

## 🚀 How to run the stock prediction model
Before running the server, add your KMA API key in main.py. ```SERVICE_KEY = "YOUR_API_KEY"```
```
git clone <repo>
cd StockPrediction

pip install -r requirements.txt

uvicorn main:app --reload
```
</br>
</br>
