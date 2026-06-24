# Week 4 Problem Statement: The "Cost of Being Wrong" (Asymmetric Optimization)

## The Context & Core Problem
Not all errors cost the company equally. Throwing away an overstocked banana might cost \$1, but a customer churning because of a stockout costs \$10. Traditional machine learning models treat these errors with equal weight, aiming for overall accuracy rather than commercial efficiency. 

## Your Mission
Mathematically bias your algorithm to account for this asymmetric "Cost of Being Wrong". Participants must tune their models to aggressively protect against stockouts while strictly keeping wastage under a 5% ceiling across SwiftCart's network.

## Final Deliverable
An optimized model that demonstrates capital efficiency by balancing the see-saw of bleeding cash on spoiled food versus losing high-value customers to competitors.

---

## LEARNING MATERIAL & RESOURCES

This compiled list of concepts and resources will guide you away from standard accuracy metrics and introduce you to business-driven optimization techniques in Python.

### 1. Cost-Sensitive Learning & Class Weights
* **Your Goal:** Learn how to assign financial penalties directly into standard algorithms so they inherently prioritize the "expensive" mistake (stockouts).
* **Documentation:** Review the Scikit-Learn documentation regarding the `class_weight` and `sample_weight` parameters, specifically for models like Random Forest or Logistic Regression.
* **Video Tutorial:** *"How to handle imbalanced datasets in Machine Learning"*
  * **Link:** [Watch here](https://www.youtube.com/watch?v=flhjn6e6wnY)

### 2. Custom Loss Functions
* **Your Goal:** Write custom mathematical functions that force advanced models to penalize under-predicting much harder than over-predicting.
* **Documentation:** Search for the official XGBoost or LightGBM documentation on writing "Custom Objective Functions" in Python.
* **Video Tutorial:** *"Create Your Custom Loss Function - Catboost"*
  * **Link:** [Watch here](https://www.youtube.com/watch?v=Kw9unYRV27w)

### 3. Decision Threshold Tuning
* **Your Goal:** Move away from the default 50% confidence threshold and manually adjust it to trigger restock orders earlier, mathematically balancing the \$10 versus \$1 error costs.
* **Video Tutorial 1:** *"ML Classification Threshold Tuning: Pick by Cost"*
  * **Link:** [Watch here](https://www.youtube.com/watch?v=-bUMpnaCTL4)
* **Video Tutorial 2:** *"predict() vs. predict_proba() – Understanding ML Model Predictions"*
  * **Link:** [Watch here](https://www.youtube.com/watch?v=qfsb9OmvB8s)

---

## Technical Specifications & Constraints

### Total Cost Scoring Formula
Your optimization performance is evaluated dynamically using the following baseline logic:

$$\text{Total Business Cost} = (\text{Total Units Spoiled} \times \$1.00) + (\text{Total Stockouts} \times \$10.00)$$

* **Goal:** Achieve the lowest possible Total Business Cost on the testing dataset, provided the total spoilage rate remains strictly under 5% of all inventory ordered.

### Validation Constraint
* **Data Splitting:** You must split your data sequentially. Train your model algorithms on the first 9 months of operations, and test your final Total Business Cost calculations exclusively on the last 3 months. 
* **Reporting:** You must report the calculated cost savings based only on this unseen test data.

---

## Submission Guidelines

Submit a **1-Page Business Memo** that includes:
* **Compare the Total Business Cost:** Contrast the financial output using a standard 50% classification threshold versus your newly tuned asymmetric model.
* **Explain Your Mathematical Approach:** Detail your specific implementation of class weights, custom loss functions, or threshold tuning configurations.
* **Provide a Spoilage Check:** Include a definitive baseline statement proving mathematically that your overall wastage rate stayed strictly under the 5% ceiling.
