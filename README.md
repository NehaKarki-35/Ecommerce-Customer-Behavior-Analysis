---

## Dataset Information

The dataset contains **6,000 customer records** with **16 columns** (15 after dropping the identifier column).

**File:** `e commerce.csv`

| Column | Type | Description |
|---|---|---|
| Customer_ID | object | Unique customer identifier (dropped before analysis) |
| account_age_months | int64 | How long the customer has had an account |
| avg_order_value | float64 | Average value of the customer's orders |
| total_orders | int64 | Total number of orders placed |
| days_since_last_purchase | int64 | Days elapsed since the most recent purchase |
| discount_usage_rate | float64 | Rate at which the customer uses discounts (0–1) |
| return_rate | float64 | Rate of product returns (0–1) |
| customer_support_tickets | int64 | Number of support tickets raised |
| loyalty_member | object | Whether the customer is in the loyalty program |
| browsing_frequency_per_week | float64 | Average browsing sessions per week |
| cart_abandonment_rate | float64 | Rate at which the customer abandons carts |
| product_review_score_avg | float64 | Average score given in product reviews (1–5) |
| engagement_score | float64 | Overall platform engagement metric |
| satisfaction_score | float64 | Customer satisfaction score |
| price_sensitivity_index | float64 | Sensitivity to price changes |
| churned | object | Target variable — whether the customer churned |

**Observed class distribution:** Approximately 85% of customers are retained; around 15% have churned.

**No missing values or duplicate rows** were found in the dataset after inspection.

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
- Dropped `Customer_ID` as it carries no analytical value.

**4. Univariate Analysis**
Distribution plots (histograms, KDE, count plots) were generated for all 13 numerical features and the two categorical columns (`loyalty_member`, `churned`).

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
A `RandomForestClassifier` was fitted on the 13 behavioral features against the `churned` target variable to rank which features most influence the model's predictions.

---

## Implementation

The analysis was implemented in a single Jupyter Notebook across 90 cells. The key code patterns used:

**Data loading:**
```python
