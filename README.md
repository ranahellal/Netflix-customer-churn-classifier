# **Netflix Customer Churn Classifier**
A data science project applying the CRISP-DM methodology to analyze and predict Netflix customer churn.
The goal was to identify which user behavior factors influence churn and ensure that the insights drawn are both statistically valid and business-relevant.

## __1. Business Understanding__

Customer churn represents users who stop using or cancel their Netflix subscription.
Reducing churn is critical for sustained revenue, customer retention, and business growth.

Project Objective:
- Predict which customers are likely to churn.
- Identify behavioral and usage patterns that influence churn.
- Provide interpretable insights that Netflix could use to improve user engagement and retention.

## __2. Data Understanding__

Dataset Source: Kaggle - Netflix Customer Churn Dataset (https://www.kaggle.com/datasets/abdulwadood11220/netflix-customer-churn-dataset)

File used: netflix_customer_churn.csv

Target variable: churn (1 = churned, 0 = retained)

Key Feature	Description:
- avg_watch_time_per_day:	Average daily watch time (hours)
- number_of_profiles:	Number of user profiles under an account
- subscription_type:	Subscription tier (Basic, Standard, Premium)
- activity_status:	Engineered feature reflecting activity engagement
- usage_rate:	Engineered feature quantifying usage intensity
- watch_hours: Total hours watched on user account
- last_login_days: How many days it has been since the customer last used their account
- age, region, device, gender, favorite_genre: Generic customer demographic information

Data Validation:
- No missing values were found.
- Invalid values detected: avg_watch_time_per_day had unrealistic maximums (up to 98 hours).

  These rows were corrected by recalculating the watch time as:
      avg_watch_time_per_day = $\frac{watch hours}{30}$

  (​assuming a 30-day month)

## __3. Data Preparation__

Notebook: Netflix customer churn preprocessing.ipynb

Data Cleaning:
- Removed irrelevant identifiers.
- Corrected invalid avg_watch_time_per_day entries as described above.

Feature Engineering:
- activity_status — represents user engagement (engineered from behavioral data).
- usage_rate — ratio-based metric reflecting how actively a user consumes content.

Encoding:
- Label-encoded engineered columns.
- One-hot encoded all other categorical variables.

No feature scaling was applied since Random Forest models are scale-invariant.

Saved the cleaned dataset as netflix_customer_churn_preprocessed.csv.

## __4. Modeling__

Notebook: Netflix customer churn modeling.ipynb

Algorithm: Random Forest Classifier

Hyperparameters: conventional parameters

Training Process:
- Split the preprocessed dataset into train and test sets.
- Fitted a Random Forest model to predict churn.
- Evaluated performance using a classification report and confusion matrix.

Performance Summary: 
| Class | Precision | Recall | F1-Score |
|:------|:----------:|:-------:|:--------:|
| 0 (Retained) | 0.96 | 0.95 | 0.95 | 
| 1 (Churned)  | 0.95 | 0.96 | 0.95 | 
| Accuracy |   |   | 0.95 | 
| Macro Avg | 0.95 | 0.95 | 0.95 | 
| Weighted Avg | 0.95 | 0.95 | 0.95 | 

The model achieved 95% accuracy, showing excellent and balanced precision–recall performance across both churned and retained classes.

## __5. Evaluation & Insights__

__To ensure the model captured genuine relationships rather than noise or multicollinearity:__

Feature Importance Analysis revealed the top predictors:

- avg_watch_time_per_day
- activity_status
- usage_rate
- number_of_profiles

Heatmap Correlation:
- Checked correlation among the top four features — confirmed that they are not strongly multicollinear.

Engineered Feature Validation:
- Tested the impact of activity_status and usage_rate — confirmed that both improved predictive accuracy.

Confusion Matrix + Classification Report:
- Showed balanced true positives/negatives → no overfitting detected.

__Key Takeaways:__
- Customers with lower average daily watch time or inconsistent activity are much more likely to churn.
- Users with multiple profiles or higher usage rates are less likely to churn — indicating stronger household engagement.
- Insights were statistically validated through feature importance, correlation, and performance consistency across runs.

## __6. Deployment & Business Relevance__

This model can be integrated into Netflix’s customer analytics pipeline to:
- Identify at-risk users for early retention interventions.
- Design targeted marketing campaigns for inactive customers.
- Guide pricing and content personalization strategies.

Even without full deployment, the analysis demonstrates how machine learning can translate customer behavior data into actionable retention insights.

## __7. Results Summary__
The Random Forest model achieved strong predictive performance with interpretable, business-relevant insights.

It reliably highlights engagement behavior as the strongest churn determinant, validating that user activity and content consumption patterns are crucial for predicting retention.


## __8. Setup & Usage__

To run the project locally:

```bash
# Clone the repository
git clone https://github.com/<your-username>/Netflix-customer-churn-classifier.git

# Navigate into the project folder
cd Netflix-customer-churn-classifier

# Install dependencies
pip install -r requirements.txt
```
---
### **This project is for educational and portfolio purposes.**
