# Customer-Churn-Prediction-Project

<img src="./dataviz/odds_ratios.png">

## I. Project Background
**What is customer churn and why it matters?**
+ Churn is the rate at which customers stop using a service, and it matters because high churn directly reduces revenue, increases acquisition costs, and signals issues with customer satisfaction and loyalty.
### Business Question:
+	Why do some subscribers leave while others stay—and how can we act on it??

## II. Objectives
**1. Analyze customer behavior and churn trends**
+ Identify customer segments with the highest churn rates.
+	Estimate revenue loss from churn and highlight which groups contribute most to it.
+ Uncover overall behavioral patterns linked to customer retention and attrition.
  
**2.	Identify key churn and retention drivers**
+	Determine the top factors that strongly influence whether customers stay or leave.
+	Provide insights into customer behaviors that signal loyalty versus churn risk.
  
**3. Build a predictive churn model**
+	Develop and evaluate a logistic regression model using scikit-learn to predict customer churn, with performance assessed through accuracy, precision, and recall.
  
**4. Translate insights into business actions**
+	Deliver a clear, actionable report with strategies to reduce churn and improve retention.
+	Recommend targeted actions (e.g., engagement campaigns, pricing strategies, support improvements) based on findings.


## III. Executive Summary
This project was conducted to address a critical business question: **Why do some subscribers leave while others stay—and how can we act on it?** **By analyzing customer churn behavior**, we **identified high-risk segments**, **quantified the revenue impact**, **uncovered the key drivers of churn**, and **built a predictive model to flag customers at risk**.
<br>
<br>
Key findings show that **churn is concentrated** among **new/early customers** (**0-20 months**) and **Basic-plan users**, resulting in an **estimated revenue loss of approximately $600k**. The analysis also revealed the **top behavioral factors driving churn** such as ```MonthlyCharges```, ```SupportsTicketPerMonth```, ```WatchlistSize```, and ```UserRating```, enabling us to focus retention strategies more effectively. A **predictive churn model** was developed with **82% accuracy**, **56% precision** and **11% recall**, providing the business with a tool **to identify at-risk customers** efficiently. Together, these insights and tools allow for targeted interventions to **reduce churn**, **protect revenue**, and **improve customer lifetime value**.

## IV. Insights Deep-Dive
### Exploratory Data Analysis (EDA)
•	**Churn Count by Subscription** - Premium user(**13,044**) are less likely to churn than Basic(**15,804**) and Standard users(**14,997**). 
<img src="./dataviz/churn_substype.png">

•	**Monthly Charges vs Churn** - Churned customers generally pay slightly higher (**$13.4 avg.** vs. **non-churned = $12.3 avg.**) monthly charges. 
<img src="./dataviz/churn_monthlycharges.png">

•	**Account Age Distribution by Churn** - Higher churn in early months (**0–20 months**).
<img src="./dataviz/churn_accage_distri.png">

•	**Correlation Heatmap (Numeric Features)** - The churn **correlations are weak** (**absolute values < 0.20**), meaning churn is **multi-factorial** rather than driven by one numeric feature alone. **No strong single predictor of churn**.
<img src="./dataviz/churn_corrheatmap.png">

### Segmentation & Analysis
<br>
<img src="./dataviz/churnrate_substype_chart.png">
<br>
<img src="./dataviz/churnrate_substype.PNG">

**Churn rates by Subscription Type** - Premium user (**16%** churn rate) are less likely to churn than Basic (**20%**) and Standard users (**18%**)
<br>
<img src="./dataviz/churnrate_tenure_chart.png">

**Churn Rates by Tenure Segment** - New subscriber are the **most vulnerable**, churn declines steadily with tenure and **rentention improves with customer longevity**.

+ **New Subscribers are the most vulnerable:**
  + The **churn rate** is **highest** among **new subscribers** (**33%**), followed by those with **less than 1 year** (**30%**).
  + This indicates that **the first year is the most critical period** for customer retention.

+ **Churn declines steadily with tenure:**
  + **1–3** Years: **27%**
  + **3–5** Years: **20%**
  + **5+** Years: only **12%**
  + Customers who stay **beyond 3 years are much more loyal**, and the **churn rate drops by nearly two-thirds** compared to new subscribers.

+ **Retention improves with customer longevity:**
  + The data clearly demonstrates a **loyalty effect**: the longer a customer remains subscribed, the less likely they are to leave.
<br>

<img src="./dataviz/churn_revenueloss_substype.png">

**Churn Revenue Loss by Subscription Type** - Basic Plan has the highest revenue loss, Standard Plan is close behind and Premium Plan has the lowest churn revenue loss.
+ **Basic Plan has the highest revenue loss:**
  + About **$211,573** in lost revenue comes from churned Basic-plan customers.
  + This suggests that although the Basic plan may have lower pricing per customer, the **high churn volume** makes it the largest contributor to revenue leakage.
    
+ **Standard Plan is close behind:**
  + Standard plan customers account for **$201,347** in churn revenue loss.
  + This indicates that mid-tier customers also churn in significant numbers, making them a crucial group to retain.

+ **Premium Plan has the lowest churn revenue loss:**
  + At **$174,782**, the Premium segment shows lower revenue loss compared to Basic and Standard.
  + This could mean Premium customers are **more loyal**, or that higher-paying customers churn less frequently.

## V. Prediction Model
+ **Preparation for Modeling:**
  + Separate ```CustomerID``` and ```Churn``` columns and use variable names ```custid``` and ```target``` respectively.
  + Identify and set a list for **Categorical** and **Numerical** variables.
  + Transform Categorical variables using **One-hot encoding**.
  + Transform and fit Numerical variables using **StandardScaler**.
  + Merge ```custid```, ```target```, **Categorical** and **Numerical** variables into ```df_merged``` DataFrame.
  + Export to a new csv file ```df_merged```.

+ **ML Modeling (Logistic Regression):**
  + Import **df_merged.csv** to dataFrame ```subs1``` then split data into **train** and **test**.
  + Store column names from ```subs1``` excluding ```target``` variable and ```custid```.
  + Extract **training features** and **target**.
  + Extract **testing features** and **target**.
  + Import the **Logistic Regression classifier**, **initialize**, and **fit** the model. 
  + Predict **churn values** on test data.
  + Print test **accuracy score**.
    
+ **Evaluation of the Model:**
  + Accuracy Testing = **82%**
  + Precision = **55%**
  + Recall = **11%**
 
+ **Model Interpretation and Explainability:**
  + Explore and plot the coefficients of the logistic regression to understand what is driving churn to go up or down: 

<img src="./dataviz/odds_ratios.png">

✅ **Positive drivers of churn (increase churn risk)** 

+ ```MonthlyCharges``` (**OR ≈ 1.3**) – Customers paying **higher monthly fees** are more likely to churn. Possibly due to **price sensitivity**.
+ ```SupportTicketsPerMonth```  (**OR ≈ 1.25**) – **Frequent issues reported** = ***dissatisfaction*** → higher churn.
+ ```WatchlistSize``` & ```UserRating``` (**OR ≈ 1.05**) – Slightly increases churn, suggesting that even **engaged users may leave** if other factors (**price**, **experience**) frustrate them.

❌ **Negative drivers of churn (reduce churn risk)**

+ ```AccountAge``` (**OR ≈ 0.6**) – **Longer-tenured customers** are less likely to churn (**loyalty effect**).
+ ```AverageViewingDuration```, ```ContentDownloadsPerMonth```, ```ViewingHoursPerWeek``` (**OR ≈ 0.65–0.7**) – **More engaged users** are less likely to churn. Engagement strongly protects retention.
+ ```SubscriptionType```: **Premium** (**OR ≈ 0.85**) – **Premium users are less likely to leave** compared to **Basic plan** holders (**perceived higher value**).
+ ```PaymentMethod```: **Credit Card** (**OR ≈ 0.9**) – **Auto-renewal** makes churn less likely.
+ ```ParentalControl``` & ```SubtitlesEnabled``` (**OR ≈ 0.95–0.98**) – Slightly reduce churn, probably tied to **better personalization features**.


## VI. Recommendations

The analysis shows that **customer churn is concentrated among short-tenure**, **Basic-plan**, and **low-engagement customers**, while higher-value **Premium** and **Standard customers** **contribute most to revenue loss when they leave**. **Key churn drivers** include **limited engagement** (**low watch time**, **small watchlists**), **poor onboarding experience**, **dissatisfaction reflected in support tickets**, and **weaker perceived value in lower-tier subscriptions**.
<br>
**To address this, the company should**:

+	**Strengthen onboarding for new users** – **provide guided walkthroughs**, **early incentives**, and **personalized recommendations within the first 6–12 months**.
+	**Boost engagement** – **expand watchlist suggestions**, **highlight trending content**, and **offer rewards** for frequent viewing or downloads.
+	**Reduce support friction** – **analyze ticket patterns**, **fix recurring issues**, and **enhance self-service options** to improve satisfaction.
+	**Differentiate subscription value** – **promote Premium benefits through free trials** or **feature previews** to reduce Basic-plan churn.
+	**Leverage churn prediction models** – **proactively flag** and **intervene with at-risk customers** using **targeted retention offers**.

**Bottom Line**: Reducing churn requires a **dual approach**: **retain more Basic customers through engagement and onboarding**,
while **protecting revenue by preventing Premium churn**. A data-driven retention strategy can lower revenue leakage, improve loyalty, and drive sustainable growth.

## VII. Dataset and Technical Information
The [Predictive Analytics for Customer Churn dataset](https://www.kaggle.com/datasets/safrin03/predictive-analytics-for-customer-churn-dataset/data) by **Safrin S** contains over **250,000 anonymized records of customer subscriptions** and **service interactions**. It includes diverse features such as **subscription type**, **payment method**, **viewing patterns**, **device usage**, **support ticket activity**, and **other variables suitable for preprocessing, exploratory analysis, and predictive modeling**.

**Additional note**: To simulate real-world data quality issues, I used generative AI to inject ~3% duplicate rows, introduce ~1% missing values at random, and insert ~2% inconsistent text entries in fields such as GenrePreference (misspellings, extra white spaces, trailing punctuation) and Gender, providing an opportunity to apply and demonstrate data preprocessing techniques.

### Dataset Schema

| Columns  | Description | 
| :------- | :------: |
| CustomerID | Unique customer identifier  |
| SubscriptionType | Subscription plan (Basic, Standard, Premium) |
| PaymentMethod | Payment method used (Credit Card, Bank transfer, etc.) |
| PaperlessBilling | Whether paperless billing is enabled (Yes/No) |
| ContentType | Content accessed (Movies, TV Shows) |
| MultiDeviceAccess | Multi-device access (Yes/No) |
| DeviceRegistered | Device type (Computer, Mobile, Tablet, TV, etc.) |
| GenrePreference | Preferred content genre (Action, Comedy, Drama, etc.) |
| Gender | Gender of customer (Male/Female) |
| ParentalControl | Whether parental controls are enabled (Yes/No) |
| SubtitlesEnabled | Whether subtitles are enabled (Yes/No) |
| AccountAge | Age of account in months |
| MonthlyCharges | Monthly subscription charges |
| TotalCharges | Total amount billed  |
| ViewingHoursPerWeek | Viewing hours per week |
| SupportTicketsPerMonth | Number of support tickets per month |
| AverageViewingDuration | Avg. viewing session length  |
| ContentDownloadsPerMonth | Number of downloads per month |
| UserRating | Customer rating (1–5)  |
| WatchlistSize | Number of items in watchlist |
| Churn | Whether the customer churned (Yes/No) |

In this project, I applied **Numpy** and **Pandas** for **data cleaning**, **transformation**, and **feature preparation**, **implemented a logistic regression model** in **Scikit-Learn** to **predict churn risk**, and **generated data visualizations** using **Matplotlib**.
### Access full project [here](CompleteProject.ipynb)
