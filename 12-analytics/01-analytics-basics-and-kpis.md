# Analytics Basics and KPIs

> Placement-focused notes covering the **most important analytics concepts and KPIs** for fresher and entry-level Data Analyst, Business Analyst, and Data/Analytics roles.

---

# 1. What is Data Analytics?

### Answer

Data analytics is the process of collecting, cleaning, transforming, analyzing, and interpreting data to find useful insights and support decision-making.

Basic flow:

```text
Raw Data
   ↓
Data Cleaning
   ↓
Data Transformation
   ↓
Data Analysis
   ↓
Insights
   ↓
Business Decision
```

### Example

An e-commerce company notices that sales have decreased.

An analyst can analyze:

- Sales by month
- Sales by product
- Sales by region
- Customer behavior
- Conversion rate

The goal is to identify **why sales decreased and what action should be taken**.

---

# 2. Why is Data Analytics Important?

### Answer

Data analytics helps organizations:

- Make data-driven decisions
- Identify trends
- Understand customers
- Measure business performance
- Find problems
- Reduce costs
- Improve processes
- Increase revenue

Instead of relying only on assumptions, businesses can use data to support decisions.

---

# 3. What is a Dataset?

### Answer

A dataset is a collection of related data organized in a structured form.

Example:

| Customer_ID | Age | City | Purchase |
|---|---:|---|---:|
| 101 | 22 | Hyderabad | 500 |
| 102 | 25 | Chennai | 800 |
| 103 | 29 | Bangalore | 1200 |

Here:

```text
Rows    → Records
Columns → Variables/Features
```

---

# 4. What is a Metric?

### Answer

A metric is a measurable value used to evaluate something.

Examples:

```text
Revenue
Profit
Orders
Users
Sales
Conversion Rate
Customer Retention
```

For example:

```text
Monthly Revenue = ₹10,00,000
```

is a metric.

---

# 5. What is a KPI?

### Answer

KPI stands for **Key Performance Indicator**.

A KPI is a measurable value used to evaluate how effectively a business, team, or process is achieving an important objective.

Examples:

```text
Revenue Growth
Profit Margin
Customer Retention Rate
Conversion Rate
Customer Acquisition Cost
Average Order Value
```

---

# 6. Metric vs KPI

### Answer

A **metric** is any measurable value.

A **KPI** is a metric that is specifically important for measuring progress toward a business objective.

Example:

```text
Number of website visitors
→ Metric

Conversion Rate
→ KPI if the business goal is increasing purchases
```

### Easy Interview Answer

> "Every KPI is a metric, but not every metric is a KPI. A KPI is a metric that is directly connected to an important business objective."

---

# 7. What is a Business KPI?

### Answer

A business KPI measures the performance of an important business objective.

Example:

### Objective

Increase sales.

### Possible KPIs

```text
Revenue
Revenue Growth Rate
Number of Orders
Average Order Value
Conversion Rate
```

---

# 8. What makes a good KPI?

### Answer

A good KPI should generally be:

```text
Specific
Measurable
Relevant
Actionable
Time-bound
```

The KPI should help answer:

> "Are we moving toward our business goal?"

---

# 9. What is a Target?

### Answer

A target is the desired value that an organization wants to achieve.

Example:

```text
Current Conversion Rate = 3%

Target Conversion Rate = 5%
```

The target provides a benchmark for measuring performance.

---

# 10. KPI vs Target

### Answer

```text
KPI
→ What are we measuring?

Target
→ What value do we want to achieve?
```

Example:

```text
KPI:
Customer Retention Rate

Target:
80%
```

---

# 11. What is a Dimension?

### Answer

A dimension is a descriptive attribute used to categorize or group data.

Examples:

```text
Country
City
Product
Category
Customer
Date
Department
```

Example:

```text
Revenue by City
```

Here:

```text
Revenue → Metric
City    → Dimension
```

---

# 12. What is a Measure?

### Answer

A measure is a numerical value that can generally be aggregated or analyzed.

Examples:

```text
Revenue
Quantity
Profit
Cost
Orders
```

Example:

```text
Revenue by Region
```

```text
Revenue → Measure
Region  → Dimension
```

---

# 13. Dimension vs Measure

### Answer

| Dimension | Measure |
|---|---|
| Describes or categorizes data | Numerical value used for analysis |
| Usually used for grouping | Usually used for calculations |
| Example: City | Example: Revenue |
| Example: Product | Example: Quantity |

Example:

```text
Sales by Product

Product → Dimension
Sales   → Measure
```

---

# 14. What is a Trend?

### Answer

A trend is the general direction in which a metric changes over time.

Example:

```text
January   → ₹1 lakh
February  → ₹1.2 lakh
March     → ₹1.5 lakh
April     → ₹1.8 lakh
```

This indicates an **upward sales trend**.

---

# 15. What is Seasonality?

### Answer

Seasonality refers to a predictable pattern that repeats during specific time periods.

Example:

```text
E-commerce sales increase every year during:
→ Diwali
→ Christmas
→ Black Friday
```

This is seasonal behavior.

---

# 16. Trend vs Seasonality

### Answer

```text
Trend
→ Long-term direction of a metric.

Seasonality
→ Repeating pattern at specific time periods.
```

A dataset can contain both.

---

# 17. What is Growth Rate?

### Answer

Growth rate measures how much a value has increased or decreased compared with a previous period.

Formula:

```text
Growth Rate (%) =
((New Value - Old Value) / Old Value) × 100
```

### Example

Previous revenue:

```text
₹1,00,000
```

Current revenue:

```text
₹1,20,000
```

Growth:

```text
((1,20,000 - 1,00,000) / 1,00,000) × 100
= 20%
```

So revenue increased by **20%**.

---

# 18. What is MoM Growth?

### Answer

MoM means **Month-over-Month**.

It compares a metric with the previous month.

Example:

```text
January Revenue = ₹10 lakh
February Revenue = ₹12 lakh
```

MoM growth:

```text
((12 - 10) / 10) × 100
= 20%
```

---

# 19. What is YoY Growth?

### Answer

YoY means **Year-over-Year**.

It compares a metric with the same period in the previous year.

Example:

```text
2025 Revenue = ₹10 crore
2026 Revenue = ₹12 crore
```

YoY growth:

```text
((12 - 10) / 10) × 100
= 20%
```

---

# 20. MoM vs YoY

### Answer

| MoM | YoY |
|---|---|
| Compares consecutive months | Compares same period across years |
| Useful for short-term changes | Useful for yearly comparison |
| Can be affected by seasonality | Better for many seasonal businesses |

Example:

```text
MoM:
March vs February

YoY:
March 2026 vs March 2025
```

---

# 21. What is Revenue?

### Answer

Revenue is the total income generated from selling products or services before deducting expenses.

Simple example:

```text
100 products × ₹500
= ₹50,000 Revenue
```

---

# 22. What is Profit?

### Answer

Profit is the amount remaining after subtracting expenses from revenue.

Basic formula:

```text
Profit = Revenue - Total Costs
```

Example:

```text
Revenue = ₹1,00,000
Costs   = ₹70,000

Profit  = ₹30,000
```

---

# 23. Revenue vs Profit

### Answer

```text
Revenue
→ Money generated from sales.

Profit
→ Money remaining after costs are deducted.
```

A company can have high revenue but low profit if its costs are high.

---

# 24. What is Profit Margin?

### Answer

Profit margin shows what percentage of revenue becomes profit.

Formula:

```text
Profit Margin (%) =
(Profit / Revenue) × 100
```

Example:

```text
Revenue = ₹1,00,000
Profit  = ₹20,000

Profit Margin
= (20,000 / 1,00,000) × 100
= 20%
```

---

# 25. What is Average Order Value (AOV)?

### Answer

AOV represents the average amount spent per order.

Formula:

```text
AOV = Total Revenue / Number of Orders
```

Example:

```text
Revenue = ₹1,00,000
Orders  = 500

AOV = 1,00,000 / 500
    = ₹200
```

---

# 26. What is Conversion Rate?

### Answer

Conversion rate measures the percentage of users who complete a desired action.

For an e-commerce website:

```text
Conversion Rate (%) =
(Number of Purchases / Number of Visitors) × 100
```

Example:

```text
Visitors  = 10,000
Purchases = 500

Conversion Rate
= (500 / 10,000) × 100
= 5%
```

---

# 27. What is Customer Acquisition Cost (CAC)?

### Answer

CAC is the average cost of acquiring a new customer.

Formula:

```text
CAC =
Total Customer Acquisition Cost / Number of New Customers
```

Example:

```text
Marketing + Sales Cost = ₹1,00,000
New Customers = 500

CAC = ₹1,00,000 / 500
    = ₹200
```

---

# 28. What is Customer Lifetime Value (CLV/LTV)?

### Answer

Customer Lifetime Value estimates the total value a customer is expected to generate during their relationship with a business.

A simple approximation can be:

```text
LTV ≈ Average Order Value
      × Purchase Frequency
      × Customer Lifespan
```

Example:

```text
AOV = ₹1,000
Purchases per year = 4
Customer lifespan = 3 years

LTV ≈ 1,000 × 4 × 3
    = ₹12,000
```

Actual business formulas can be more detailed.

---

# 29. CAC vs LTV

### Answer

```text
CAC
→ How much does it cost to acquire a customer?

LTV
→ How much value does that customer generate over their lifetime?
```

Businesses often compare the two to evaluate customer acquisition economics.

---

# 30. What is Retention Rate?

### Answer

Retention rate measures the percentage of customers or users that remain active during a specified period.

A common customer-retention formula is:

```text
Retention Rate (%) =
((Ending Customers - New Customers) / Starting Customers) × 100
```

Example:

```text
Starting Customers = 1,000
New Customers      = 200
Ending Customers   = 900

Retention Rate
= ((900 - 200) / 1,000) × 100
= 70%
```

---

# 31. What is Churn Rate?

### Answer

Churn rate measures the percentage of customers or users who leave during a specified period.

A simple formula is:

```text
Churn Rate (%) =
Customers Lost / Customers at Start × 100
```

Example:

```text
Starting Customers = 1,000
Customers Lost     = 50

Churn Rate
= (50 / 1,000) × 100
= 5%
```

---

# 32. Retention Rate vs Churn Rate

### Answer

```text
Retention
→ Percentage of customers who stay.

Churn
→ Percentage of customers who leave.
```

In a simple situation:

```text
Retention Rate + Churn Rate ≈ 100%
```

The exact relationship depends on how the metrics are defined.

---

# 33. What is DAU?

### Answer

DAU stands for **Daily Active Users**.

It measures the number of unique users who are active during a day according to the product's defined activity criteria.

---

# 34. What is MAU?

### Answer

MAU stands for **Monthly Active Users**.

It measures the number of unique users who are active during a month according to the product's defined activity criteria.

---

# 35. What is DAU/MAU?

### Answer

DAU/MAU is commonly used as an engagement ratio.

Formula:

```text
DAU/MAU (%) =
DAU / MAU × 100
```

Example:

```text
DAU = 20,000
MAU = 100,000

DAU/MAU
= 20%
```

A higher value generally indicates that monthly active users are returning more frequently, but the metric must be interpreted according to the product and its usage pattern.

---

# 36. What is a Funnel?

### Answer

A funnel represents the stages users go through before completing a desired action.

Example:

```text
Website Visitors
       ↓
Product Viewers
       ↓
Add to Cart
       ↓
Checkout
       ↓
Purchase
```

At each stage, some users drop out.

---

# 37. What is Funnel Conversion Rate?

### Answer

It measures the percentage of users who move from one stage of a funnel to the next or from the beginning to the final conversion.

Example:

```text
Visitors = 10,000
Purchases = 500

Overall Conversion Rate
= 500 / 10,000 × 100
= 5%
```

---

# 38. What is Drop-off Rate?

### Answer

Drop-off rate measures the percentage of users who leave a process before completing the next desired step.

Example:

```text
Checkout Started = 1,000
Purchases        = 800

Drop-off
= 200 users
```

The corresponding drop-off rate is:

```text
200 / 1,000 × 100
= 20%
```

---

# 39. What is Cohort Analysis?

### Answer

Cohort analysis groups users based on a shared characteristic or event and tracks their behavior over time.

A common example is grouping users by signup month.

```text
January Cohort
February Cohort
March Cohort
```

Then compare their retention or revenue over subsequent months.

---

# 40. Why is Cohort Analysis Useful?

### Answer

It helps answer questions such as:

```text
Are newer customers retaining better?
Which signup month had the best retention?
How does customer behavior change over time?
```

It is especially useful for analyzing retention and customer behavior.

---

# 41. What is Segmentation?

### Answer

Segmentation divides data or customers into meaningful groups.

Examples:

```text
Age
Location
Customer Type
Purchase Frequency
Income
Product Category
```

Example:

```text
Customers
   ↓
New Customers
Returning Customers
High-Value Customers
Low-Value Customers
```

---

# 42. Why is Segmentation Important?

### Answer

Segmentation helps businesses understand that different groups may behave differently.

For example:

```text
Customer Segment A
→ High purchases

Customer Segment B
→ Low purchases
```

The company can create different strategies for different groups.

---

# 43. What is Correlation?

### Answer

Correlation measures the strength and direction of association between two variables.

Example:

```text
Advertising Spend ↑
Sales ↑
```

If they tend to move together, they may have positive correlation.

Correlation is commonly represented using a value between:

```text
-1 and +1
```

---

# 44. Does Correlation Mean Causation?

### Answer

No.

**Correlation does not prove causation.**

Two variables can move together because of:

- A third variable
- Coincidence
- Selection effects
- Other underlying factors

Example:

```text
Ice cream sales ↑
Sunglasses sales ↑
```

This does not mean ice cream causes sunglasses sales.

A third factor such as hot weather may influence both.

---

# 45. What is an Outlier?

### Answer

An outlier is a data point that is unusually far from the general pattern of the data.

Example:

```text
10
12
11
13
12
150
```

Here, `150` may be an outlier.

Outliers should be investigated rather than automatically removed.

---

# 46. Why are Outliers Important in Analytics?

### Answer

Outliers can represent:

```text
Data entry errors
Fraud
Unusual customer behavior
Exceptional business events
Genuine extreme values
```

An analyst should determine the reason before deciding how to handle them.

---

# 47. What is an Average?

### Answer

The arithmetic mean is calculated as:

```text
Average =
Sum of Values / Number of Values
```

Example:

```text
10, 20, 30

Average = 60 / 3
        = 20
```

---

# 48. Mean vs Median

### Answer

### Mean

```text
Sum of values / Number of values
```

### Median

The middle value after sorting the data.

Example:

```text
10, 20, 30, 40, 1000
```

Mean is heavily affected by `1000`.

Median is:

```text
30
```

Therefore, median can be more representative when the data contains strong outliers or is highly skewed.

---

# 49. What is a Distribution?

### Answer

A distribution describes how values are spread across a dataset.

It helps us understand:

```text
Center
Spread
Skewness
Frequency
Outliers
```

---

# 50. What is a Dashboard?

### Answer

A dashboard is a visual interface that presents important metrics, KPIs, charts, and trends in one place.

Example:

```text
------------------------------------
| Revenue | Orders | Profit | CAC |
------------------------------------
|        Revenue Trend             |
------------------------------------
| Sales by Region | Product Sales |
------------------------------------
```

Tools commonly used for dashboards include:

```text
Power BI
Tableau
Excel
Looker
```

---

# 51. What makes a good dashboard?

### Answer

A good dashboard should:

- Focus on important KPIs
- Be easy to understand
- Avoid unnecessary charts
- Show useful trends
- Use appropriate visualizations
- Provide relevant filters
- Help users make decisions

The dashboard should answer business questions rather than simply display as much data as possible.

---

# 52. What is Data-Driven Decision Making?

### Answer

Data-driven decision making means using analyzed data and evidence to support business decisions.

Example:

Instead of saying:

```text
"I think customers prefer Product A."
```

An analyst can examine:

```text
Sales
Customer ratings
Repeat purchases
Conversion rate
```

and use the evidence to make a decision.

---

# 53. What is Descriptive Analytics?

### Answer

Descriptive analytics answers:

> **What happened?**

Examples:

```text
Last month's revenue was ₹50 lakh.
Sales decreased by 10%.
1,000 new customers joined.
```

---

# 54. What is Diagnostic Analytics?

### Answer

Diagnostic analytics answers:

> **Why did it happen?**

Example:

```text
Revenue decreased by 10%.

Analysis:
→ Product A sales decreased.
→ Region B had fewer orders.
→ Website conversion also decreased.
```

The goal is to identify possible reasons for the observed result.

---

# 55. What is Predictive Analytics?

### Answer

Predictive analytics answers:

> **What is likely to happen?**

It uses historical data and statistical or machine-learning methods to estimate future outcomes.

Example:

```text
Expected sales next month
Expected customer churn
Expected demand
```

---

# 56. What is Prescriptive Analytics?

### Answer

Prescriptive analytics answers:

> **What should we do?**

Example:

```text
Sales are expected to decrease.

Possible recommendation:
→ Increase marketing for Product A.
→ Offer targeted discounts.
→ Improve the checkout process.
```

---

# 57. Descriptive vs Diagnostic vs Predictive vs Prescriptive

### Answer

| Type | Main Question |
|---|---|
| Descriptive | What happened? |
| Diagnostic | Why did it happen? |
| Predictive | What is likely to happen? |
| Prescriptive | What should we do? |

Easy memory:

```text
What happened?
      ↓
Why?
      ↓
What next?
      ↓
What should we do?
```

---

# 58. What is an Insight?

### Answer

An insight is a meaningful finding from data that helps explain a situation or support a decision.

Weak observation:

```text
Sales decreased by 10%.
```

More useful insight:

```text
Sales decreased by 10%, mainly because mobile conversion
dropped significantly after the checkout change.
```

A good insight connects:

```text
Data → Finding → Business Meaning → Possible Action
```

---

# 59. What is Root Cause Analysis?

### Answer

Root cause analysis attempts to identify the underlying reason for a problem rather than only describing the symptom.

Example:

```text
Problem:
Sales decreased.

Possible investigation:
Sales ↓
   ↓
Orders ↓
   ↓
Conversion Rate ↓
   ↓
Checkout failures ↑
   ↓
Payment service issue
```

The payment issue may be closer to the root cause than simply saying "sales decreased."

---

# 60. What is A/B Testing?

### Answer

A/B testing compares two versions of something to determine which performs better against a defined metric.

Example:

```text
Group A → Old checkout page
Group B → New checkout page
```

Suppose:

```text
A Conversion Rate = 4%
B Conversion Rate = 5%
```

The company can analyze whether the observed difference supports choosing the new version.

---

# 61. Why is A/B Testing Useful?

### Answer

A/B testing can help evaluate changes using controlled comparisons.

Examples:

```text
Website design
Button placement
Pricing
Email subject lines
Landing pages
Product features
```

The success metric should be defined before evaluating the test.

---

# 62. What is a Business Question?

### Answer

A business question is a specific question that analytics is expected to answer.

Bad question:

```text
"Analyze the data."
```

Better question:

```text
"Why did monthly sales decrease by 15%?"
```

Even better:

```text
"Which products and regions contributed most to the
15% decrease in monthly sales?"
```

---

# 63. What is the role of an Analyst?

### Answer

A data analyst typically:

```text
Understand business problem
        ↓
Collect / access data
        ↓
Clean data
        ↓
Analyze data
        ↓
Identify patterns
        ↓
Create reports/dashboards
        ↓
Communicate insights
        ↓
Support decisions
```

An analyst is not only responsible for creating charts or writing SQL queries.

---

# 64. How do you choose the right KPI?

### Answer

I would start with the business objective.

Example:

### Objective

Increase customer retention.

Possible KPIs:

```text
Retention Rate
Churn Rate
Repeat Purchase Rate
Customer Lifetime Value
```

The KPI should directly help measure progress toward the objective.

---

# 65. A KPI decreased suddenly. What would you do?

### Answer

I would investigate systematically:

```text
1. Verify the data.
2. Check whether the KPI definition changed.
3. Compare with previous periods.
4. Break the KPI down by important dimensions.
5. Look for unusual changes or outliers.
6. Check business/product changes.
7. Identify likely drivers.
8. Communicate the finding and possible action.
```

Example dimensions:

```text
Region
Product
Device
Customer Segment
Date
```

---

# 66. Sales increased but profit decreased. Why could this happen?

### Answer

Possible reasons include:

```text
Higher operating costs
Lower profit margins
More discounts
Higher marketing costs
Higher production costs
Change in product mix
Higher shipping costs
```

This is why analyzing only revenue is not enough.

---

# 67. Revenue increased but conversion rate decreased. Is that possible?

### Answer

Yes.

Revenue can increase even when conversion rate decreases if other factors increase sufficiently.

For example:

```text
Website Traffic ↑ significantly
Conversion Rate ↓ slightly
Average Order Value ↑
```

The total number of purchases and revenue can still increase.

This demonstrates why multiple KPIs should be analyzed together.

---

# 68. What would you analyze if sales suddenly dropped?

### Answer

I would examine:

```text
Revenue
Orders
Conversion Rate
Traffic
Average Order Value
Product performance
Region performance
Customer segments
Marketing channels
Returns/cancellations
Website or payment issues
```

Then I would compare the affected period with previous periods and identify where the largest change occurred.

---

# 69. What is KPI Drill-Down?

### Answer

Drill-down means breaking a high-level KPI into smaller dimensions to understand what is driving it.

Example:

```text
Total Revenue
      ↓
Revenue by Region
      ↓
Revenue by Product
      ↓
Revenue by Customer Segment
```

This helps identify the source of a change.

---

# 70. ⭐ Most Important KPIs to Remember

## E-commerce

```text
Revenue
Orders
Average Order Value
Conversion Rate
Cart Abandonment Rate
Customer Acquisition Cost
Customer Lifetime Value
Retention Rate
Churn Rate
```

## Product / App

```text
DAU
MAU
DAU/MAU
Retention Rate
Churn Rate
Conversion Rate
Funnel Drop-off
```

## Marketing

```text
CAC
Conversion Rate
Click-Through Rate
Cost Per Acquisition
Return on Ad Spend
```

## Business / Finance

```text
Revenue
Profit
Profit Margin
Revenue Growth
Cost
Average Order Value
```

---

# 71. ⭐ Important Formulas

## Growth Rate

```text
Growth Rate (%) =
((New Value - Old Value) / Old Value) × 100
```

## Profit

```text
Profit = Revenue - Total Costs
```

## Profit Margin

```text
Profit Margin (%) =
(Profit / Revenue) × 100
```

## Average Order Value

```text
AOV = Revenue / Number of Orders
```

## Conversion Rate

```text
Conversion Rate (%) =
Conversions / Total Visitors × 100
```

## CAC

```text
CAC =
Total Acquisition Cost / New Customers
```

## Churn Rate

```text
Churn Rate (%) =
Customers Lost / Starting Customers × 100
```

## Retention Rate

```text
Retention Rate (%) =
((Ending Customers - New Customers) / Starting Customers) × 100
```

## DAU/MAU

```text
DAU/MAU (%) =
DAU / MAU × 100
```

---

# 72. ⭐ Rapid-Fire Interview Questions

## Q1. What is data analytics?

### Answer

The process of examining data to discover useful information, patterns, and insights that support decision-making.

---

## Q2. What is a KPI?

### Answer

A Key Performance Indicator is a measurable value used to evaluate progress toward an important objective.

---

## Q3. Metric vs KPI?

### Answer

A metric is any measurable value, while a KPI is a metric specifically tied to an important business objective.

---

## Q4. What is a dimension?

### Answer

A descriptive attribute used to categorize or group data, such as region, product, or date.

---

## Q5. What is a measure?

### Answer

A numerical value used for analysis, such as revenue, quantity, or profit.

---

## Q6. What is revenue?

### Answer

The income generated from selling products or services before deducting expenses.

---

## Q7. What is profit?

### Answer

Revenue minus costs.

---

## Q8. What is conversion rate?

### Answer

The percentage of users who complete a desired action.

---

## Q9. What is CAC?

### Answer

Customer Acquisition Cost is the average cost of acquiring a new customer.

---

## Q10. What is LTV?

### Answer

Lifetime Value estimates the value a customer generates over their relationship with a business.

---

## Q11. What is churn?

### Answer

The rate at which customers or users leave during a specified period.

---

## Q12. What is retention?

### Answer

The percentage of customers or users who remain active during a specified period.

---

## Q13. What is DAU?

### Answer

Daily Active Users.

---

## Q14. What is MAU?

### Answer

Monthly Active Users.

---

## Q15. What is cohort analysis?

### Answer

Analyzing groups of users who share a common characteristic or event, such as signup month, and tracking their behavior over time.

---

## Q16. What is segmentation?

### Answer

Dividing data or customers into meaningful groups for analysis.

---

## Q17. What is a funnel?

### Answer

A sequence of stages users go through before completing a desired action.

---

## Q18. What is an outlier?

### Answer

A data point that is unusually far from the general pattern of the dataset.

---

## Q19. What is correlation?

### Answer

A measure of the strength and direction of association between two variables.

---

## Q20. Does correlation mean causation?

### Answer

No. Correlation alone does not prove that one variable causes another.

---

## Q21. What is descriptive analytics?

### Answer

Analytics that answers: **What happened?**

---

## Q22. What is diagnostic analytics?

### Answer

Analytics that answers: **Why did it happen?**

---

## Q23. What is predictive analytics?

### Answer

Analytics that estimates **what is likely to happen**.

---

## Q24. What is prescriptive analytics?

### Answer

Analytics that helps determine **what should be done**.

---

## Q25. What is a dashboard?

### Answer

A visual interface that presents important KPIs, metrics, trends, and charts in one place.

---

# 73. ⭐ Top 15 Questions to Prepare First

If you have limited preparation time, focus on these:

```text
1. What is Data Analytics?
2. What is a KPI?
3. Metric vs KPI?
4. Dimension vs Measure?
5. What is Revenue?
6. Revenue vs Profit?
7. What is Conversion Rate?
8. What is CAC?
9. What is LTV?
10. What is Retention and Churn?
11. What are DAU and MAU?
12. What is Cohort Analysis?
13. What is Funnel Analysis?
14. What is Correlation vs Causation?
15. What would you do if a KPI suddenly decreased?
```

---

# 74. Final Placement Revision Checklist

```text
ANALYTICS BASICS
☐ Data Analytics
☐ Dataset
☐ Metric
☐ KPI
☐ Target
☐ Dimension
☐ Measure
☐ Trend
☐ Seasonality
☐ Growth Rate

BUSINESS METRICS
☐ Revenue
☐ Profit
☐ Profit Margin
☐ AOV
☐ Conversion Rate
☐ CAC
☐ LTV
☐ Retention
☐ Churn
☐ DAU
☐ MAU

ANALYSIS
☐ Funnel Analysis
☐ Drop-off
☐ Cohort Analysis
☐ Segmentation
☐ Correlation
☐ Causation
☐ Outliers
☐ Root Cause Analysis
☐ KPI Drill-down

ANALYTICS TYPES
☐ Descriptive
☐ Diagnostic
☐ Predictive
☐ Prescriptive

REPORTING
☐ Dashboard
☐ KPI Selection
☐ Business Questions
☐ Data-driven Decision Making
☐ Communicating Insights

IMPORTANT FORMULAS
☐ Growth Rate
☐ Profit
☐ Profit Margin
☐ AOV
☐ Conversion Rate
☐ CAC
☐ Retention Rate
☐ Churn Rate
☐ DAU/MAU
```

---

# 75. Final Interview Mindset

For analytics interviews, do not only memorize definitions.

For every KPI, understand these four things:

```text
1. What does it measure?
2. What is the formula?
3. Why is it important?
4. What could cause it to increase or decrease?
```

For example:

```text
Conversion Rate

What?
→ Percentage of visitors who convert.

Formula?
→ Conversions / Visitors × 100

Why?
→ Measures how effectively traffic turns into desired actions.

If it decreases?
→ Investigate product, pricing, UX, traffic quality,
   technical issues, and customer segments.
```

> **Placement goal:** Be able to explain the main analytics concepts in simple language, calculate the common KPIs, interpret changes in those KPIs, and connect the numbers to a business problem. For fresher interviews, this practical understanding is more valuable than memorizing a large number of advanced analytics terms.