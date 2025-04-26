# Water Volume Prediction for Lakes and Reservoirs

## Table of Contents
- [Project Overview](#project-overview)
- [Problem Context](#problem-context)
- [Dataset Collection](#dataset-collection)
  - [Lake and Reservoir Data](#lake-and-reservoir-data)
  - [Weather Data](#weather-data)
- [Data Cleaning and Preprocessing](#data-cleaning-and-preprocessing)
- [Feature Selection](#feature-selection)
- [Model Selection and Evaluation](#model-selection-and-evaluation)
  - [Multiple Linear Regression](#multiple-linear-regression)
  - [Polynomial Regression](#polynomial-regression)
  - [Neural Network Regression](#neural-network-regression)
  - [Random Forest Regression](#random-forest-regression)
  - [Decision Tree Regression](#decision-tree-regression)
  - [Support Vector Regression (SVR)](#support-vector-regression-svr)
  - [Gaussian Process Regression (GPR)](#gaussian-process-regression-gpr)
  - [Auto-sklearn](#auto-sklearn)
- [Results](#results)
- [How to Run This Project](#how-to-run-this-project)
- [Conclusion](#conclusion)



---

## Project Overview
This project aims to predict the changes in water volume of a lake or reservoir over the next 24 hours based on weather conditions.  
It helps water management authorities make informed decisions to address issues caused by climate change and sudden weather events.

---

## Problem Context
Penang, Malaysia, has faced critical water shortages where reservoirs had only 30 days of water supply left.Additionally, poor response to heavy rainfall 10 years ago in Cameron Highlands caused sudden floods.  
These examples show that weather is a major factor affecting water volume, and better prediction models are necessary.

---

## Dataset Collection
Since no public historical water level data for Malaysia was found, we sourced our data internationally.

### Lake and Reservoir Data
- **Source:** [Watershed Connection](https://www.watershedconnection.com/)
- **Data Collection Method:** Web Scraping using BeautifulSoup and requests
- **Features extracted:**
  - Location
  - Full_%
  - Current_Elevation_ft
  - Current_Storage_af
  - Remaining_Elevation_ft
  - Available_Storage_af
  - 24hr.Change
  - Rain_inches
  - Date
  - Highest_temperature
  - Lowest_temperature
  - Highest_humidity
  - Lowest_humidity
- **Dataset Size:** 10 years of data (~36,530 rows)

### Weather Data
- **Nearest Weather Station:** Falcon Field Airport, Phoenix, AZ
- **Source:** [Visual Crossing](https://www.visualcrossing.com/)
- **Collection Method:** API access (with a free daily limit of 1000 records)

---

## Data Cleaning and Preprocessing
- Handling missing values
- Removing duplicates
- Data type conversion
- Feature engineering (e.g., creating 'Previous_Storage_af' column by shifting storage values)
- Data integration from multiple sources
- Scaling and normalizing features

---

## Feature Selection
Selected features for model training:
- Previous_Storage_af (previous day's storage volume)
- Rain_inches (rainfall in the last 24 hours)

Target variable:
- 24hr.Change (change in water volume)

Unnecessary features like snow data, redundant identifiers, and unrelated climate attributes were dropped to improve model performance.

---

## Model Selection and Evaluation

### Multiple Linear Regression
A baseline model assuming a linear relationship between features and the target.

### Polynomial Regression
Extended linear regression to capture non-linear relationships.

### Neural Network Regression
Used to model complex relationships with multiple hidden layers.

### Random Forest Regression
An ensemble model combining multiple decision trees to improve accuracy and reduce overfitting.

### Decision Tree Regression
A simple tree-based model splitting data based on feature thresholds.

### Support Vector Regression (SVR)
A regression model that uses support vectors to predict within a margin of tolerance.

### Gaussian Process Regression (GPR)
A probabilistic model useful for capturing uncertainty in predictions.

### Auto-sklearn
An automated machine learning library that automatically selects and tunes the best model.

---

## Results
Performance was evaluated using:
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- R-squared (R²)

Key findings:
- Random Forest Regression performed the best among manually trained models.
  - MSE: 0.009902
  - RMSE: 0.099508
  - R²: 0.690128
- Auto-sklearn produced an ensemble model with better performance:
  - R²: 0.731670
- When limited to a single model, Auto-sklearn also selected Random Forest Regression, but our tuned model performed better than Auto-sklearn’s individual model.
  
---
## How to Run This Project

1. Clone the Repository
```bash
git clone https://github.com/ngzhiwei517/Water-Volume-Prediction-for-Lakes-and-Reservoirs.git
cd water-volume-prediction

 ```

2. Install required dependencies (assuming you have Python and pip installed):

    ```bash
    pip install -r requirements.txt
    ```
3. Open the Jupyter notebook (`water_volume_prediction.ipynb`) in Google Colab or any Jupyter notebook environment.

4. Follow the instructions within the notebook to:
     - Data scraping
     - Data preprocessing
     - Model training
     - Model evaluation
---

## Conclusion

Machine learning models, especially ensemble methods like Random Forest Regression, can greatly assist in proactive water resource management.Predictions allow authorities to better prepare for abnormal weather events, optimize water usage, and prevent disasters like floods and shortages.While machine learning improves decision-making, human judgment remains crucial due to the inherent uncertainty in predictions.

