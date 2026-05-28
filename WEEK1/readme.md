# Week 1: Learning Resources & Problem Statement

## LEARNING MATERIAL

To complete this task, you will need foundational skills in data manipulation, basic visualization, and business analytics. 

---

## Core Competencies

### 1. Exploratory Data Analysis (EDA) with Python
* **Pandas Fundamentals:** Learn to import datasets, inspect rows, and calculate summary statistics using functions like `read_csv()`, `head()`, `info()`, and `describe()`.
* **Handling Missing Data:** Practice identifying null values with `isna()` and determining whether to imputes missing numbers or drop incomplete rows to maintain accurate baseline calculations.
* **Data Aggregation:** Utilize the `groupby()` function to isolate wastage and stockout metrics by specific store locations, days of the week, or product categories.

### 2. Data Visualization Basics
* **Matplotlib & Seaborn:** Learn to translate raw data into clear visuals for business stakeholders.
* **Categorical Comparisons:** Practice building bar charts to compare wastage volume across different perishable categories (e.g., produce vs. dairy).
* **Trend Spotting:** Create line graphs to map out stockout spikes during specific peak hours.

### 3. Translating Data into Business Impact
* **Defining KPIs:** Understand how to translate a technical data point into a financial metric, such as multiplying the volume of unsold goods by unit cost to find the daily capital loss.
* **Annualized Forecasting:** Practice calculating daily financial losses across multiple locations and projecting those figures over a 365-day timeline to present the total annualized impact.

---

## Recommended Learning Resources
Here are some excellent, beginner-friendly YouTube videos that you can use to learn the specific skills required for the Week 1 task. We have broken them down by the core competencies they will need to complete the exploratory data analysis (EDA).

### 1. Exploratory Data Analysis (EDA) Basics in Pandas
These videos are perfect for those who need to understand the fundamentals of importing datasets, checking for missing values, and getting a high-level overview of their data.

* **Exploratory Data Analysis in Pandas | Python Pandas Tutorials (by Alex The Analyst)**
  * **What it covers:** This is a fantastic, straightforward walkthrough of how to read data, use functions like `info()` and `describe()`, find null values, group data, and even create some basic visualizations.
  * **Link:** [Watch here](https://www.youtube.com/watch?v=Liv6eeb1VfE)

* **Exploratory Data Analysis with Python | PANDAS (by Mo Chen)**
  * **What it covers:** A comprehensive guide on exploring a CSV dataset, cleaning data (like dropping duplicates), and systematically asking and answering questions about the data using Pandas functions.
  * **Link:** [Watch here](https://www.youtube.com/watch?v=hA0qyW-w3pQ)

### 2. Hands-on Pandas Projects (Data Cleaning & Aggregation)
To calculate the annualized losses, you will need to manipulate and aggregate specific columns (like finding the total spoiled items by store or category).

* **Pandas Project for Beginners | CSV Dataset Cleaning & Analysis in Google Colab**
  * **What it covers:** An excellent project-based video that walks through loading a CSV file, grouping data with `groupby()`, and handling missing values using `isna()`, `dropna()`, and `fillna()`. It uses Google Colab, which is a highly recommended, free, web-based tool for your participants to use.
  * **Link:** [Watch here](https://www.youtube.com/watch?v=GD10MkJjyhk)

* **Analysis of Data Science Dataset using Python**
  * **What it covers:** This video takes a dataset and focuses heavily on manipulating and grouping the data to find specific business insights, such as distributions and averages over time.
  * **Link:** [Watch here](https://www.youtube.com/watch?v=hT12wn1IeTs)

### 3. Data Visualization (Translating Numbers to Insights)
Once you have calculated the raw cost of the wasted goods and stockouts, you will need to visualize these trends for the baseline report.

* **Matplotlib and Seaborn Tutorial for Beginners | Barplot**
  * **What it covers:** A quick, targeted tutorial on how to use Seaborn to create bar plots. This is directly applicable to comparing the volume of wastage across different perishable categories (e.g., Produce vs. Dairy).
  * **Link:** [Watch here](https://www.youtube.com/watch?v=S1f_zbqr-QQ)

* **Matplotlib and Seaborn Tutorial for Beginners | Lineplot**
  * **What it covers:** A brief guide on plotting trend lines using Matplotlib and Seaborn, which is ideal for mapping out peak-hour stockout trends over time.
  * **Link:** [Watch here](https://www.youtube.com/watch?v=ZWm3a3HFIjA)

---

## Week 1 Problem Statement: Quantifying the Bleed

### The Context
SwiftCart operates a network of 50 dark stores focused on delivering daily essentials in under 15 minutes. Because the business relies on tight margins and ultra-fast commerce, efficiency is critical.

### The Core Problem
Currently, store managers rely on manual inventory guesswork to stock daily goods. This manual approach is causing the company to lose margin at both ends of the supply chain through two costly errors:
* **Mistake A (Overstocking):** Buying too much to be safe results in spoiled food, generating a 12% perishable wastage rate across the network.
* **Mistake B (Understocking):** Buying too little to save money results in an 8% stockout rate during peak hours, causing high-value customers to switch to competitors.

### Your Mission
Perform an Exploratory Data Analysis (EDA) on SwiftCart’s current operations dataset. Your objective is to move beyond the percentages and quantify the exact annualized financial losses caused by this manual procurement. Calculate the raw cost of the wasted perishable goods and the estimated revenue lost from peak-hour stockouts. Your final deliverable should establish the baseline "bleed," proving mathematically why human managers cannot accurately predict demand.

---

## The Dataset
Since analyzing 50 stores over a full year requires a robust dataset, I have provided a sample CSV snippet you can use immediately to understand the schema.

* **Dataset Link:** [Access the synthetic dataset here](https://drive.google.com/drive/folders/130qonOkAeVlz1bUYg4L3GTuLnMrhwUJA?usp=share_link)

### The Data Dictionary (What the columns mean)
* **Date:** The specific date of operations.
* **Store_ID:** Identifies which of the 50 dark stores the data belongs to (e.g., ST-001).
* **SKU_Category:** The type of product (Produce, Dairy, Bakery, Pantry, Snacks). Perishables will have higher wastage.
* **Unit_Cost:** What SwiftCart pays for the item.
* **Retail_Price:** What the customer pays for the item.
* **Units_Ordered:** The number of items the manager guessed they needed.
* **Units_Sold:** The actual number of items purchased by customers.
* **Units_Spoiled:** Items that expired and were thrown away (Mistake A).
* **Stockout_Flag:** Binary indicator (1 = ran out of stock, 0 = stayed in stock) (Mistake B).
* **Peak_Hour_Stockout:** Binary indicator showing if the stockout happened during high-demand hours.
* **Est_Lost_Sales:** The estimated number of units customers would have bought if the item wasn't sold out.
