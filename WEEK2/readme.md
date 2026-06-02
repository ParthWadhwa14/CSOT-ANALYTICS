# Week 2 Problem Statement: Feature Engineering (Beyond Historical Data)

## The Context
In Week 1, you quantified the financial impact of inventory guesswork across SwiftCart's network of dark stores. By analyzing wastage and stockouts, you established the baseline operational losses caused by manual procurement decisions and demonstrated how these inefficiencies directly affect profitability. While this analysis explained how much the company is losing, it did not explain why demand fluctuates so dramatically from one day to another.

As SwiftCart continues to scale its ultra-fast delivery operations, leadership now wants to move beyond measuring losses and begin understanding the drivers of customer demand. If demand were perfectly stable, forecasting inventory requirements would be straightforward. In reality, customer purchasing behavior changes constantly in response to factors that store managers cannot reliably predict through intuition alone.

## The Core Problem
SwiftCart's current forecasting approach relies primarily on historical sales data. Although previous sales provide valuable information about customer behavior, they often fail to capture the external conditions that cause sudden changes in demand. As a result, managers may continue making inventory decisions based on patterns that no longer reflect current circumstances.

Some examples of these external demand drivers include:
* Unusually hot weather increasing ice cream and cold beverage sales.
* Weekend shopping patterns leading to higher demand for household essentials.
* Friday evening spikes in bakery and ready-to-eat products.
* Rainy conditions encouraging more customers to place delivery orders.

A forecasting system that only considers historical sales remains blind to these influences and therefore struggles to accurately anticipate future demand.

## Your Mission
Your objective this week is to perform a Feature Engineering Analysis using SwiftCart's operational data. Rather than focusing solely on historical sales, you will investigate which additional variables can help explain customer purchasing behavior and improve forecasting performance.

Your analysis should explore the impact of factors such as:
* Day of the week and weekend effects
* Weather conditions including temperature, rainfall, and humidity
* Store location characteristics
* Other variables that may influence customer demand

The goal is not simply to collect more data, but to identify the right data. By understanding which external factors consistently influence demand, you will help transform SwiftCart's forecasting process from reactive guesswork into a structured, data-driven system.

### Exemplary Additional Dataset Variables

| Temporal Features | Weather Features | Location Features |
| :--- | :--- | :--- |
| `Day_of_Week` | `Temperature` | `Store_City` |
| `Weekend_Flag` | `Rainfall_mm` | `Population_Density` |
| `Holiday_Flag` | `Humidity` | `Avg_Household_Income` |

## Final Deliverable
At the end of the week, you will submit a Feature Engineering Report that documents your findings and recommendations. The report should contain four key components:

1. **Feature Inventory:** Identify and justify the set of variables that should be incorporated into the forecasting model. This should include both existing operational metrics and newly introduced external variables.
2. **Correlation Analysis:** Investigate the relationships between these variables and customer demand. Using statistical analysis and visualizations, provide evidence showing how specific factors influence purchasing behavior.
3. **Feature Schema:** Design a structured dataset that combines historical sales data with temporal, weather-based, and store-level features. This schema will serve as the foundation for the predictive model developed in Week 3.
4. **Business Recommendation:** Conclude with a short recommendation explaining why historical sales data alone is insufficient for accurate forecasting and how the inclusion of external demand drivers can help SwiftCart reduce wastage, minimize stockouts, and improve operational efficiency.

---

## LEARNING MATERIAL

To complete this task, you will need a basic understanding of feature engineering, correlation analysis, and dataset preparation.

### 1. Feature Engineering Fundamentals
Feature engineering is the process of creating meaningful variables from raw data that help explain patterns in customer demand. In a real-world forecasting system, historical sales alone rarely provide enough information to accurately predict future demand. Participants should understand how additional variables can be derived from existing data and how business context plays a crucial role in deciding which features are likely to improve forecasting performance.

### 2. Time-Based Features
Customer purchasing behavior often follows recurring patterns based on time. Certain products may experience higher demand on weekends, while others may see spikes during specific days of the week or around holidays. Participants should learn how to extract useful information from date-related data and understand how temporal patterns can influence grocery demand across different stores and product categories.

### 3. Weather-Based Features
External factors such as weather can significantly impact purchasing decisions. Temperature, rainfall, and humidity often influence what customers buy and when they place orders. For example, hot weather may increase demand for cold beverages and ice cream, while rainy conditions can lead to a rise in online grocery orders. Participants should explore how weather data can be incorporated into a forecasting system and how these variables may help explain fluctuations in demand.

### 4. Correlation Analysis
Before including a feature in a forecasting model, it is important to determine whether it has a meaningful relationship with demand. Correlation analysis helps identify which variables are likely to be useful predictors and which provide little value. Participants should learn how to measure relationships between variables, interpret correlation matrices, and use visualizations such as heatmaps to support their analysis.

### 5. Feature Encoding
Many useful variables, such as product categories, store locations, and days of the week, are stored as text rather than numbers. Since machine learning models require numerical inputs, these categorical variables must be converted into an appropriate numerical format. Participants should understand common encoding techniques and learn how to prepare categorical data for use in predictive models.

### 6. Building a Forecasting Dataset
The final step is combining historical sales data with the newly engineered features into a structured dataset that can be used for modeling. Participants should understand how to organize input variables, define a target variable, and create a clean dataset that captures both historical demand patterns and external demand drivers. This dataset will serve as the foundation for the forecasting model developed in Week 3.

---

## LEARNING RESOURCES

### Feature Engineering Fundamentals
* **Krish Naik — Feature Engineering Playlist**
  * [Search on YouTube](https://www.youtube.com/results?search_query=krish+naik+feature+engineering)

### Working with Date & Time Features
* **Datetime Feature Engineering in Python**
  * [Search on YouTube](https://www.youtube.com/results?search_query=datetime+feature+engineering+python)

### Correlation Analysis & Heatmaps
* **Alex The Analyst — Correlation Matrix Tutorial**
  * [Search on YouTube](https://www.youtube.com/results?search_query=alex+the+analyst+correlation+matrix)

### Encoding Categorical Variables
* **One-Hot Encoding & Label Encoding Tutorial**
  * [Search on YouTube](https://www.youtube.com/results?search_query=one+hot+encoding+label+encoding+python)

### Demand Forecasting Concepts
* **Demand Forecasting with Machine Learning**
  * [Search on YouTube](https://www.youtube.com/results?search_query=demand+forecasting+machine+learning)