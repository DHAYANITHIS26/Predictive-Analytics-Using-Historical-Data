1.Clean Architecture:
Organized into a modular, clean folder layout.
Decoupled data loading/cleaning (data_loader.py), plotting (eda_plots.py), ML models (models.py), time-series forecasting (forecasting.py), and report compilation (report_generator.py).
Robust Setup & Data Quality:
requirements.txt listing production libraries.
generate_sample_data.py generating 5+ years of realistic transactions.
Automagic data cleaning handles duplicates, invalid inputs, clips outliers at the 99th percentile, and handles missing fields.
Advanced Time Series & ML Modeling:
Machine Learning: Linear Regression, Random Forest, and XGBoost regressor predicting future monthly sales, featuring hyperparameter tuning via GridSearchCV and feature importance calculations.
Time Series: ARIMA (SARIMAX), Holt-Winters Exponential Smoothing, and a custom Seasonal decomposition trend fallback for Prophet.
Estimates 95% confidence intervals for future projections.
Interactive Dashboard Pages (Streamlit):
Home: KPI performance summaries (Sales, Profits, Transactions, Average Order Values, MoM Growth Rates) and status metrics.
Dataset: File uploader (CSV/Excel) and automatic sample database generator with structural analysis.
Data Cleaning: Summary counts (before vs. after rows, duplicates, outliers).
EDA: Product analysis, regional splits, purchase recurrence (histograms), Net profit timelines, and heatmaps.
Model Training: Validation comparisons, grid search, and residual plots.
Forecast: Future projection visualizer showing historical values vs predictions with confidence bands.
Reports: One-click downloaders for cleaned datasets, forecasts, and a beautifully compiled PDF report.
File Architecture
All files are located in the workspace: 
/d:/Predictive Analytics Using Historical Data
:


d:\Predictive Analytics Using Historical Data\
├── app.py                      # Streamlit application navigation & views
├── requirements.txt            # Python dependencies (Pandas, Streamlit, Scikit-learn, XGBoost, Statsmodels, Fpdf2)
├── generate_sample_data.py     # Script generating 5+ years of sales history
├── verify_pipeline.py          # Script validating the forecasting pipeline
├── data/
│   └── sample_sales_data.csv   # Automatically generated dataset (8,922 transactions)
└── utils/
    ├── __init__.py
    ├── data_loader.py          # Data ingestion, schema validation, and cleaning functions
    ├── eda_plots.py            # Plotly interactive charting utilities
    ├── models.py               # Supervised regression and recursive forecasts
    ├── forecasting.py          # Time-series models and Prophet fallbacks
    └── report_generator.py     # PDF compiler compiling summaries using fpdf2
Verification Results
We verified the pipeline successfully using our regression testing script: python verify_pipeline.py. Here is a copy of the validation log:

text

🚀 Starting sales forecasting pipeline validation...
✅ Dataset located at data/sample_sales_data.csv
✅ Schema validation: PASSED
✅ Data cleaning: PASSED (8922 raw rows -> 8922 cleaned rows)
✅ Scatter plot generation: PASSED
✅ Monthly data aggregation: PASSED (66 months)
✅ ML Model Training: PASSED
--- ML Metrics ---
                        MAE           MSE      RMSE      R2   MAPE
Linear Regression  10249.16  1.381619e+08  11754.23  0.2945  10.74
Random Forest      11988.50  2.022007e+08  14219.73 -0.0325  11.87
XGBoost            13560.78  2.120163e+08  14560.78 -0.0826  13.56
Best ML Model: Linear Regression
✅ Time Series Models: PASSED
--- Time Series Metrics ---
                                       MAE      RMSE      R2   MAPE
ARIMA                             13350.92  16662.45 -0.4177  14.13
Exponential Smoothing              9781.27  11829.23  0.2855  10.28
Prophet (Fallback: Seasonal Reg)   9775.37  11826.65  0.2858  10.27
✅ PDF Report Generation: PASSED (5578 bytes)
🎉 ALL PIPELINE VERIFICATIONS PASSED SUCCESSFULLY!
Instructions to Run the Application
To run the Streamlit forecasting dashboard on your system:

Verify Dependencies: Open a terminal in the project directory and install the packages listed in requirements.txt:
bash

pip install -r requirements.txt
Start the Dashboard: Run the Streamlit server:
bash

streamlit run app.py
Explore pages:
Access the dashboard in your browser (typically http://localhost:8501).
Go to the 📂 Dataset page and select Generate & Load 5-Year Sample Data to populate the state.
Go through 🧹 Data Cleaning, 📊 EDA, and train the regressors on the 🤖 Model Training page.
Generate future trends on the 📈 Forecast page.
Compile the 📄 Reports page to download the final Executive Forecast Report PDF.
