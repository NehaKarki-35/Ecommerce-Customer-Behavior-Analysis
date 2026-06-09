# E-commerce Customer Churn Analysis

## Introduction

This project performs an exploratory data analysis on an e-commerce customer dataset to understand why customers stop using a platform — a behavior commonly referred to as churn. The analysis works through patterns in customer activity, purchasing history, support interactions, and satisfaction to identify signals that precede churn.

The notebook is structured progressively: starting from a literature review, moving through data cleaning, univariate and bivariate analysis, and finally into pattern recognition and feature importance using a Random Forest model.

---

## Problem Statement

E-commerce platforms face a persistent challenge in retaining customers. Churn — when a customer stops purchasing from or engaging with the platform — develops gradually rather than suddenly. The problem is that businesses often react to churn after it has already happened, rather than identifying at-risk customers in advance.

This project investigates the behavioral and transactional signals that are associated with customer churn, with the goal of understanding which factors most strongly predict it.

---

## Project Objective

- Identify key behavioral patterns that precede customer churn.
- Understand the relationship between engagement, satisfaction, discount dependency, support usage, and churn.
- Use feature importance from a Random Forest classifier to rank which variables most influence churn.
- Generate actionable insights from the data that could inform retention strategies.

---

## Technologies Used

| Tool / Library | Purpose |
|---|---|
| Python | Core programming language |
| Jupyter Notebook | Development and analysis environment |
| Pandas | Data loading, cleaning, and manipulation |
| NumPy | Numerical operations |
| Matplotlib | Plotting and visualization |
| Seaborn | Statistical visualizations |
| Scikit-learn | Random Forest classifier and feature importance |

---

## Project Structure

    Ecommerce-Customer-Behavior-Analysis/
    │
    ├── data/
    │   └── e commerce.csv
    │
    ├── notebooks/
    │   └── E-ecomerce dataset  .ipynb
    │
    ├── LICENSE
    └── README.md

---

## Dataset Information

The dataset contains **6,000 customer records** with **16 columns** (15 after dropping the identifier column).

**File:** e commerce.csv

| Column | Type | Description |
|---|---|---|
| Customer_ID | object | Unique customer identifier (dropped before analysis) |
| account_age_months | int64 | How long the customer has had an account |
| avg_order_value | float64 | Average value of the customer's orders |
| total_orders | int64 | Total number of orders placed |
| days_since_last_purchase | int64 | Days elapsed since the most recent purchase |
| discount_usage_rate | float64 | Rate at which the customer uses discounts (0-1) |
| return_rate | float64 | Rate of product returns (0-1) |
| customer_support_tickets | int64 | Number of support tickets raised |
| loyalty_member | object | Whether the customer is in the loyalty program |
| browsing_frequency_per_week | float64 | Average browsing sessions per week |
| cart_abandonment_rate | float64 | Rate at which the customer abandons carts |
| product_review_score_avg | float64 | Average score given in product reviews (1-5) |
| engagement_score | float64 | Overall platform engagement metric |
| satisfaction_score | float64 | Customer satisfaction score |
| price_sensitivity_index | float64 | Sensitivity to price changes |
| churned | object | Target variable — whether the customer churned |

Observed class distribution: Approximately 85% of customers are retained; around 15% have churned.

No missing values or duplicate rows were found in the dataset after inspection.

---

## Methodology

The analysis follows a structured EDA approach:

**1. Literature Review**
The notebook opens with a written review of e-commerce churn research, identifying key factors: inactivity (recency), low engagement, poor satisfaction, high return rates, and discount dependency.

**2. Hypothesis Formulation**
Four hypotheses were defined before analysis:
- H1 (Recency): Customers inactive for longer periods are more likely to churn.
- H2 (Engagement + Satisfaction): Low scores on both metrics are associated with higher churn.
- H3 (Service Issues): High support tickets and return rates increase churn probability.
- H4 (Price Sensitivity): Highly price-sensitive customers are less loyal.

**3. Data Cleaning**
- Checked and confirmed no null values or duplicates.
- Dropped Customer_ID as it carries no analytical value.

**4. Univariate Analysis**
Distribution plots (histograms, KDE, count plots) were generated for all 13 numerical features and the two categorical columns (loyalty_member, churned).

**5. Bivariate Analysis**
Scatter plots, regression plots, and box plots were used to explore relationships between pairs of variables — for example, account age vs. total orders, discount usage vs. average order value, and return rate vs. satisfaction.

**6. Correlation Heatmap**
A full correlation matrix across all numerical features was visualized to identify linear relationships between variables.

**7. Pattern Analysis**
Eight named behavioral patterns were identified and visualized with churn as the hue variable:

| Pattern | Description |
|---|---|
| Silent Friction | High engagement but low satisfaction — hidden dissatisfaction |
| Browse Trap | High browsing but low orders — interest without conversion |
| Support Paradox | More support tickets correlate with higher churn, but effective service can recover users |
| Discount Addiction Loop | Heavy discount users churn more, driven by offers rather than loyalty |
| Slow Decay Churn | Gradual increase in inactivity and engagement drop before eventual churn |
| False Loyalty Trap | Loyalty membership alone does not prevent churn if experience is poor |
| Price Sensitivity Amplifier | Price-sensitive customers churn more when engagement declines |
| Satisfaction Final Trigger | Low satisfaction is the strongest final signal before churn |

**8. Feature Importance**
A RandomForestClassifier was fitted on the 13 behavioral features against the churned target variable to rank which features most influence the model's predictions.

---

## Results

- **Churn rate:** Around 15% of the 6,000 customers have churned; 85% are retained.
- **Most customers** make relatively few orders, with average order values concentrated in the lower range (0-200).
- **Browsing activity:** Most customers browse 2-4 times per week. Higher browsing does not reliably predict higher purchases (Browse Trap pattern).
- **Discount usage:** The majority of discount usage falls in the 0.1-0.3 rate range. Customers who rely heavily on discounts are more likely to churn.
- **Return rates:** Generally low across the dataset (0.0-0.03 for most customers).
- **Support tickets:** Most customers do not raise support tickets. Those who do are more likely to churn, though effective service can partially offset this.
- **Satisfaction and engagement:** These two variables are closely related to churn outcomes. Low scores on both are the strongest combined signal of churn risk.
- **Loyalty program:** Only a small portion of customers are loyalty members (approximately 17%). Loyalty membership reduces but does not eliminate churn risk.
- **Feature importance:** Satisfaction score, engagement score, and days since last purchase were among the primary contributors to the Random Forest model's churn predictions.

---

## Future Improvements

- Replace the hardcoded file path with a relative path so the notebook runs without modification after cloning.
- Add a requirements.txt file to make dependency installation straightforward.
- Build a formal churn prediction pipeline with train/test split, evaluation metrics (accuracy, precision, recall, F1, ROC-AUC), and cross-validation.
- Add customer segmentation using K-Means clustering to group at-risk customers and tailor retention strategies per segment.
- Encode categorical columns (loyalty_member, churned) more explicitly and document label encoding steps in the notebook.
- Write all cell-level insights in English throughout for wider readability, as some commentary is currently written in Hindi/Urdu.

---

## Author

**Neha Karki**

GitHub: [NehaKarki-35](https://github.com/NehaKarki-35)

---

Licensed under the MIT License.
