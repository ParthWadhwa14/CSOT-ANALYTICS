# Week 3: Building the Baseline Predictor (Initial Modeling)

## 1. Where We Stand: Shifting from Analysis to Action
In Week 1, we looked closely at the numbers and quantified the financial "bleed" happening across SwiftCart’s network of 50 urban dark stores. The findings were clear: relying on store managers to manually estimate daily inventory results in a 12% perishable waste rate and an 8% peak-hour stockout rate. Humans simply aren't built to calculate complex demand patterns mentally on the fly.

In Week 2, we took a major step forward by looking beyond past sales. We engineered a data schema packed with external triggers, proving that things like weather shifts, the day of the week, and local neighborhood demographics deeply influence customer buying behavior.

Now, it’s time to put those insights to work. Your goal for Week 3 is to build the first real iteration of our Automated Demand Predictor. We aren't trying to build a mathematically flawless, perfect model on the first try. Instead, we want to create a stable, working predictive pipeline that delivers a 10% to 15% improvement in forecasting accuracy over manual human guesswork. This baseline model will become the engine that takes the cognitive load off store managers and automates daily inventory orders.

---

## 2. The Technical Challenge
Your task is to build a  localized, SKU-level regression pipeline. Your model will ingest the historical, time-based, weather, and location features we organized last week, and use them to predict our continuous target variable: Daily Demand (`Actual_Units_Demanded`).

As you build this pipeline, keep these three practical challenges in mind:
* **Avoiding Data Leakage:** Supply chain data is naturally chronological. If you use a standard, random train-test split, you'll accidentally leak future data into past predictions. You need to use a clean, time-based split to keep your validation honest.
* **Handling Varied Demand Velocities:** Perishable categories like Dairy and Produce experience sudden spikes and drops based on a single rainy afternoon or a weekend morning. On the other hand, Pantry staples see steady, slow-moving baselines. Your model needs to be flexible enough to handle both without washing out the volatility of fresh goods.
* **Explaining the "Why":** Before we hand over the procurement keys to an algorithm, leadership needs to trust it. You'll need to pull feature importance metrics to visually prove that your model is making logical decisions based on real-world operational factors.

---

## 3. Data Dictionary: The Unified Schema
To train your baseline models, you will use the integrated dataset generated at the end of Week 2. This file merges SwiftCart's daily store transactions with historical local weather metrics and spatial census data.

| Column Name | Data Type | Variable Type | What It Means in Plain English |
| :--- | :--- | :--- | :--- |
| `Date` | Datetime | Temporal Index | The specific operating date (YYYY-MM-DD). |
| `Store_ID` | String / Categorical | Spatial Identifier | The unique ID for each of our 50 dark stores (e.g., ST-001 to ST-050). |
| `SKU_Category` | String / Categorical | Product Feature | The product department (Produce, Dairy, Bakery, Pantry, Snacks). |
| `Unit_Cost` | Float | Financial Feature | The wholesale price SwiftCart pays to buy one unit of this product. |
| `Retail_Price` | Float | Financial Feature | The shelf price shown to consumers on the mobile app. |
| `Lag_1_Sales` | Integer | Historical Feature | Exactly how many units of this SKU category sold at this store yesterday (t-1). |
| `Lag_7_Sales` | Integer | Historical Feature | How many units of this SKU category sold at this store exactly one week ago (t-7). Captures weekly patterns. |
| `Rolling_Avg_3d` | Float | Historical Feature | The average daily sales over the trailing 3 days. Helps smooth out random daily blips. |
| `Day_of_Week` | Integer (0-6) | Temporal Feature | Mapped from 0 (Monday) to 6 (Sunday). |
| `Weekend_Flag` | Binary (0 or 1) | Temporal Feature | 1 if the day is Saturday or Sunday; 0 if it's a weekday. |
| `Holiday_Flag` | Binary (0 or 1) | Temporal Feature | 1 if it's a public or national holiday; 0 otherwise. |
| `Temperature_C` | Float | Weather Feature | The average local temperature recorded that day in degrees Celsius. |
| `Rainfall_mm` | Float | Weather Feature | Total daily rainfall in millimeters. Essential for flagging rainy delivery surges. |
| `Humidity_Pct` | Integer (0-100) | Weather Feature | The average relative humidity percentage recorded around the store. |
| `Population_Density` | Integer | Spatial Feature | Residents per square kilometer within the store's 15-minute delivery radius. |
| `Avg_Household_Income` | Float | Spatial Feature | The median annual household income of the surrounding neighborhood. |
| `Actual_Units_Demanded` | Integer | Target Variable | The real market demand for the day, calculated as: Units_Sold + Est_Lost_Sales. This is what your model is trying to predict. |

---

## 4. Step-by-Step Workflow

### Step 4.1: Prep the Data & Hold Out the Future
* **Handle Text Categories:** Convert your categorical text columns (like SKU_Category and Store_ID) into numbers. Use one-hot encoding for categories with a few values, or target encoding if high cardinality threatens to add too many dimensions.
* **Scale Your Numbers:** For models that are sensitive to scale, normalize continuous columns (like Population_Density or Avg_Household_Income) using a standard scaler so high-magnitude values don't warp your model weights.
* **Split by Time:** Do not use a random shuffle. Reserve the final 14 to 21 days of your dataset as a strict out-of-time test window. Train your model entirely on data from before this period.

### Step 4.2: Choose Your Quality Checkers
Because we are predicting a raw number of units demanded, evaluate your models through three lenses:
1. **Mean Absolute Error (MAE):** Tells you exactly how many units your predictions are off by on average (e.g., "Our model is off by an average of 4 loaves of bread").
2. **Root Mean Squared Error (RMSE):** Heavily penalizes large, dramatic misses. If your RMSE is much higher than your MAE, it means the model is making occasional catastrophic errors.
3. **Mean Absolute Percentage Error (MAPE):** Looks at the error relative to the store's size, allowing you to compare high-volume and low-volume stores fairly.

### Step 4.3: Train, Test, and Compare
Train three different types of models to see how they handle our operational constraints:
* **Model Alpha (Linear Regression):** Run a regularized linear model (like Ridge or Lasso). This gives you an easily explainable, straightforward baseline.
* **Model Beta (Decision Tree Regressor):** Introduce non-linear capabilities. Trees are excellent at picking up basic threshold rules (e.g., IF Weekend_Flag is 1 AND Rainfall_mm is greater than 5, THEN lift demand).
* **Model Gamma (Random Forest / Ensemble Regressor):** Group an ensemble of trees to smooth out variance and prevent overfitting. This structure usually provides the most stable predictions across highly volatile perishable items.

### Step 4.4: Run a Sanity Check on Features
Extract the feature importance scores from your best-performing model. Plot the top 10 factors driving its predictions and make sure they match basic supply chain common sense.

---

## 5. Hand-Picked Learning Resources
If you're new to coding regression pipelines or evaluating model errors in Python, these beginner-friendly, practical video tutorials will show you exactly how to write the code using the scikit-learn library:

### Topic 1: Supervised Regression Basics
* **Linear Regression Deep Dive**
  * *Visual guide to predicting continuous variables and fitting lines:* [Watch Video](https://www.youtube.com/watch?v=2ODZvZLurrs)
* **StatQuest: Linear Regression**
  * *Intuitive breakdown of regression equations and residuals without the jargon:* [Watch Video](https://www.youtube.com/watch?v=aFDOzpTeg0s)

### Topic 2: Writing the Code (Scikit-Learn)
* **Machine Learning Project from Scratch**
  * *End-to-end workflow for train-test splits, model fitting, and predictions:* [Watch Video](https://www.youtube.com/watch?v=On1M1d30PFQ)
* **Scikit-Learn Tutorial**
  * *Developer guide to scaling data, encoding labels, and using the sklearn ecosystem:* [Watch Video](https://www.youtube.com/watch?v=-IvNzmrcyUM)

### Topic 3: Reading Your Accuracy Scores
* **MAE, MSE, RMSE, and R-Squared Explained**
  * *How to calculate and interpret regression error metrics:* [Watch Video](https://www.youtube.com/watch?v=w1RySTwe6Dk)
* **Model Evaluation Basics**
  * *How to spot model overfitting and test accuracy on unseen data:* [Watch Video](https://www.youtube.com/watch?v=6dbrR-WymjI)

---

## 6. Week 3 Deliverable: Baseline Performance Report
Submit a concise executive memo and codebase containing:
* **Performance Matrix:** A comparison table tracking your three models across validation metrics.
* **Overfitting Diagnostic:** A brief check on model generalization and how the timeline split was handled.
* **Code Submission:** A clickable link to your Google Colab notebook or GitHub repository containing the complete, reproducible Python script.