**Retail Data Analytics - Demand Forecasting & Inventory Optimisation**
**Forecasting Weekly Sales and Optimising Inventory Across 45 Stores**

**Project Overview**
This project analyzes sales performance across 45 retail stores and multiple departments using real-world data from Kaggle's Retail Data Analytics dataset. The goal is to:
1. **Forecast weekly sales** at store-department level
2. **Understand key demand drivers** (seasonality, lags, holidays, store/dept effects)
3. **Translate forecast uncertainty into inventory decisions** (safety stock & reorder points)

The project demonstrates an end-to-end analytics workflow in Python: data integration, feature engineering, time series forecasting with XGBoost, model evaluation, and **business-facing inventory recommendations**.

This repository is part of my data analytics portfolio and focuses on bridging **predictive modeling with operational decision-making**.

**Problem Statement**
Retail chains face persistent challenges in:
1. Accurately **predicting weekly demand** across many stores and departments
2. Accounting for **seasonality, holidays, and historical trends**
3. **Balancing inventory** to avoid both stockouts (lost sales) and overstock (high holding costs)

**Objective**
Build a **robust forecasting model** that predicts weekly sales and converts forecaset uncertainity into:
1. **Safety stock recommendations**
2. **Reorder points per store-department**
3. Actionable insights to improve **supply chain and inventory planning**

**Data Sources**
This project uses three CSV files from Kaggle's **Retail Data Analytics (45 Stores)** dataset:
1. sales data-set.csv - weekly sales by store and department
2. Features data set.csv - external factors (holidays, CPI, tempeature, etc.)
3. stores data-set.csv - store metadata (type, size)

**Data Pipeline**
Kaggle CSV Files
   ↓
Python (pandas)
   ↓
Merge sales + features + stores
   ↓
Weekly aggregation (store, dept, week_start, IsHoliday)
   ↓
Feature engineering:
   - Lag features (lag_1, lag_2, lag_3, lag_4, lag_12)
   - Rolling mean (rolling_4)
   - Calendar features (month)
   - Encoded store & department IDs
   ↓
Train/Test split (time-based)
   ↓
XGBoost Regression Model
   ↓
Forecast Evaluation (MAE, RMSE)
   ↓
Inventory Logic:
   - RMSE → demand uncertainty
   - Safety stock (z=1.65, lead time=2 weeks)
   - Reorder point = avg demand × lead time + safety stock

**Tech Stack**
1. **Python**
2. **pandas, numpy** - Data wrangling & feature engineering
3. **matplotlib** - Exploratory analysis & visualizations
4. **scikit-learn** - Metrics & preprocessing
5. **XGBoost** - Time series regression model
6. **joblib** - Model persistence

**Analysis Performed**
1. **Expoloratory Data Analysis (EDA)**
   - Aggregated raw transactions to weekly sales per store-department
   - Identified:
     1. Top stores by total revenue
     2. Top departments by total revenue
   - Visualized:
     1. Overall weekly sales trends (seasonality)
     2. Department-level seasonality patterns
     3. Holiday vs non-holiday sales impact

   2. **Feature Engineering**
      -Time-series features:
      1. lag_1, lag_2, lag_3, lag_4, lag_12
      2. rolling_4 (4-week rolling mean)
      3. month
      - Encoided categorical indentifiers:
        1. store_enc, dept_enc

   3. **Forecasting Model**
   - Model: XGBoost Regressor
   - Train/Test split: **time-based split** (last 12 weeks as test horizon)
   - Evaluation metrics:
     1. MAE (Mean Absolute Error)
     2. RMSE (Root Mean Squared Error)

    Result from run:
   1. MAE = 2252
   2. RMSE - 4739

4. **Feature Importance**
  - Top drivers of demand:
    1. lag_1 (most recent week) - dominant predictor
    2. lag_2, lag_3, rolling_4 - strong short-term momentum signals
    3. month - captures seasonality
    4. store_enc, dept_enc - structural differences across stores/departments
   
**Business Questions Answered**
1. What are the **top-performing stores and departments** by revenue?
2. What **seasonal patterns** exist in weekly sales?
3. How **accurately** can weekly sales be forecasted using historical demand?
4. Which **features drive demand the most**?
5. How can forecast uncertainty be converted into **safety stock and reorder points**?
6. Which store-department combinations require **higher inventory buffers**?

**KPIs Produced / Affected**
- **Forecast Accuracy
  1. MAE (Mean Absolute Error)
  2. RMSE (Root Mean Squared Error)

- **Inventory Planning Metrics**
  1. Average weekly demand
  2. Demand uncertainty (RMSE per store-dept)
  3. **Safety stock**
  4. **Reorder point**

- **Business Performance Views**
  1. Top stores by total sales
  2. Top departments by total sales
  3. Holiday vs non-holiday sales impact

**Inventory Recommendations Logic**
Using forecast errors:
1. Compute RMSE per store-department as demand uncertainty
2. Apply standard inventory formula:
   Safety Stock = z × RMSE × √(lead_time)
Reorder Point = (Average Weekly Demand × Lead Time) + Safety Stock
where:
z = 1.65 (~95% service level)
Lead time = 2 weeks

This prodcues **practical, operations-ready inventory thresholds** per store and department.

**Key Insights**
1. Recent sales history (lag features) dominates demand prediction
2. Strong seasonality exists at both global and department level
3. Forecast uncertainty varies widely across store-department pairs → inventory buffers should be differentiated, not uniform
4. A single global inventory rule would **overstock some locations and understock others**

**Business Recommendations**
1. Use **store-department level forecasts** instead of global averages
2. Apply **dynamic safety stock** based on forecast uncertainty (RMSE)
3. Increase buffer stock for:
   - High-variance departments
   - High-revenue stores
4. Integrate this pipeline into:
   - Weekly replenishment planning
   - Promotion & seasonal planning cycles
  
**How to Run**
git clone https://github.com/imayakehelkaduwa99-design/Retail_Data_Analytics_Supermarket_Chain.git
cd Retail_Data_Analytics_Supermarket_Chain
pip install -r requirements.txt
jupyter notebook

Open: Retail Data Analytics.ipynb and run all cells

**Dataset Acknowledgment**
- Source: Kaggle - Retail Data Analytics (45 Stores)


**Final Takeaway**
This project goes beyond "just forecasting":
- **What will sell?** - Time series forecasting
- **Why?** - Feature importance & seasonality analysis
- **So What?** - Inventory safety stock & reorder points
- **Business value** - Fewer stockouts, lower overstock, better working capital efficiency

It demonstrates how **data science + analytics can directly drive operational decisions** in retail supply chains. 

**Author - Imaya Kehelkaduwa (Analytics and Data Engineering Portfolio**)
   
