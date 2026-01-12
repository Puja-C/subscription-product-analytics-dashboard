This dashboard uses custom DAX measures to calculate key product and business metrics. These include Active Subscribers, Churn Rate, Monthly Recurring Revenue (MRR), Retention Rate, and Feature Usage. The measures were designed to reflect common subscription product KPIs, enabling analysis of user growth, churn patterns, cohort retention, and behavioural differences between retained and churned users. The focus was on using clear, business-relevant metrics to support decision-making rather than complex technical modelling.

# Key DAX Measures (Power BI)

## Active Subscribers
DAX:
Active Subscribers = CALCULATE(DISTINCTCOUNT(subscriptions[user_id]), subscriptions[status] = "Active")


## Churned Subscribers
DAX:
Churned Subscribers = CALCULATE(DISTINCTCOUNT(subscriptions[user_id]),subscriptions[status] = "Churned")


## Total Subscribers
DAX:
Total Subscribers = DISTINCTCOUNT(subscriptions[user_id])


## Churn Rate
DAX:
Churn Rate = DIVIDE([Churned Subscribers],[Total Subscribers])


## MRR (Monthly Recurring Revenue)
DAX:
MRR =SUMX(FILTER(subscriptions,subscriptions[status] = "Active"),subscriptions[monthly_price])


## Signup Month (Calculated Column in subscription_users)
DAX:
Signup Month =FORMAT(subscription_users[signup_date], "YYYY-MM")


## Users per Cohort
DAX:
Users per Cohort = DISTINCTCOUNT(subscription_users[user_id])


## Retained Users
DAX:
Retained Users =CALCULATE(DISTINCTCOUNT(subscriptions[user_id]),subscriptions[status] = "Active")


## Retention Rate 
DAX:
Retention Rate = DIVIDE([Retained Users],[Users per Cohort])


## Total Events
DAX:
Total Events = COUNT(subscription_events[event_id])
