📊 SME Customer Segmentation Dashboard

An interactive Power BI dashboard that segments Nigerian SME banking customers by value, credit risk, and digital adoption — built to help a bank or fintech move from guessing who their best customers are, to knowing, with data.

🎯 The Problem

SMEs, and the institutions that serve them, often treat all customers the same way, without a clear view of who's high value, who's a credit risk, and who's underusing digital banking channels.

This project analyzes a customer dataset to answer:

Who are the most valuable SME customers?
Which customers carry the highest credit or loan risk?
Which customers are underusing digital banking (upsell opportunity)?
Does location or industry sector affect value or risk?
What is each segment actually worth to the business, in revenue?

🗂️ Dataset

A simulated dataset of 1,000 Nigerian SME banking customers, covering:

Business profile: state, zone, sector, business age, employee count
Financials: annual revenue, monthly transactions, average transaction value
Credit: loan amount, loan status, credit score
Digital behavior: mobile banking, POS usage, internet banking, digital adoption score
Relationship: customer lifetime (years)

⚠️ Note: This is a synthetic/sample dataset built for portfolio and learning purposes, not real bank records.

🧮 Methodology

Since the dataset has no transaction-level dates, I adapted the classic RFM (Recency, Frequency, Monetary) framework to fit the data available, using three dimensions instead:

Value Score (1–5) — combines percentile rank of annual revenue and monthly transaction frequency (replaces Frequency + Monetary)
Risk Level (Low / Medium / High) — based on credit score and loan status (any overdue loan automatically flags High risk)
Digital Level (Low / Medium / High) — based on digital adoption score

These three dimensions combine into five customer segments:

Segment	Description

🏆 Champions	High value, low risk, high digital adoption
💼 Loyal Traditional	High value, low risk, but low digital adoption
🌱 Growth Potential	Medium value, developing
⚠️ At-Risk	High credit/loan risk, regardless of value
😴 Low Engagement	Low value, low activity

All scoring was built with live formulas in Excel (not hardcoded), so the logic recalculates automatically if the underlying data changes.

💡 Key Insights

49% of SME customers fall into the At-Risk segment — the single biggest finding, driven by overdue loans and low credit scores. This should be the bank's top priority for credit review.
Champions make up only 3.5% of customers but contribute a disproportionate share of revenue — a small, high-value group worth protecting with dedicated relationship management.
Loyal Traditional customers (10%) are high-value but low on digital adoption — the clearest upsell opportunity for mobile and internet banking products.
Revenue and risk vary noticeably across zones and sectors (explore this live in the dashboard using the slicers).

✅ Recommendations

Champions: Assign relationship managers, offer premium products, prioritize retention.
Loyal Traditional: Target with digital banking onboarding campaigns. High value customers who aren't yet using digital channels are the fastest ROI opportunity.
Growth Potential: Offer working capital products or transaction incentives to move them toward Champion status.
At-Risk: Immediate priority for credit review, loan restructuring conversations, or tighter monitoring.
Low Engagement: Investigate whether these are dormant accounts to re-engage, or churn candidates.

🧑‍💻 DAX Measures

DAX

Total Customers = COUNTROWS('Cleaned_Data')

Total Revenue (NGN) = SUM('Cleaned_Data'[Annual_Revenue_NGN])

Avg Credit Score = AVERAGE('Cleaned_Data'[Credit_Score])

At Risk % = 
DIVIDE(
    CALCULATE(COUNTROWS('Cleaned_Data'), 'Cleaned_Data'[Risk_Level] = "High"),
    [Total Customers]
)

Champions Count = 
CALCULATE(COUNTROWS('Cleaned_Data'), 'Cleaned_Data'[Customer_Segment] = "Champions")

Avg Digital Score = AVERAGE('Cleaned_Data'[Digital_Adoption_Score])

What each measure does:

Total Customers — counts all rows in the dataset, used on the KPI card and as the denominator for At Risk %

Total Revenue (NGN) — sums annual revenue across all SME customers, custom formatted to display in ₦ billions

Avg Credit Score — average credit score across the full customer base

At Risk % — percentage of customers flagged High risk, calculated by filtering the customer count to only High risk rows and dividing by the total

Champions Count — filtered count used for segment specific reporting

Avg Digital Score — average digital adoption score, used in the segment profile matrix to compare digital maturity across segments

⚠️ Limitations

Synthetic data: segments and insights are based on simulated, not real, customer behavior, so business conclusions are illustrative rather than production ready.

No true "Recency" dimension: the dataset had no transaction dates, so I adapted RFM to Value + Risk + Digital Adoption instead of true Recency/Frequency/Monetary.

No time-series trend: the dashboard is a single snapshot; it doesn't show how customers move between segments over time.

Risk thresholds are simplified: credit score cutoffs (580/700) were chosen using general reference ranges, not validated against real Nigerian banking risk models.

No statistical validation: segments were built using business logic and percentile scoring, not a formal clustering algorithm like K-means, so segment boundaries are rule based rather than data derived.#

💬 Feedback

Feedback is welcome, particularly from anyone working in data analytics or banking. Feel free to open an issue on this repository or reach out via LinkedIn.

🛠️ Tools Used

Excel — data cleaning and segmentation logic (formulas, not hardcoded values)
Power BI — interactive dashboard build, DAX measures, data visualization

📁 Repository Contents

├── SME_Customer_Segmentation_Dashboard.pbix 
├── dashboard_screenshot.png                  
├── README.md                                 




