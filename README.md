# DAX Processes for PhoneNow: Customer Churn

Following the data import, cleaning, and transformation processes in PostgreSQL, the cleaned and transformed data has been successfully connected to Power BI. All data types are correctly formatted. The DAX processes are designed to provide clear insights into customer churn and its drivers. The goal is to identify the factors contributing to churn and to support strategies for improving retention. 

Simple DAX measures are used to answer key questions. These measures include:
1. [Calculated Columns](#calculated-columns) 
2. [DAX Measures](#dax-measures)

## Calculated Columns
These columns categorize or calculate values at the row level before aggregating data:

- **Tenure Level**: Categorizes customer tenure into specific ranges to analyze customer loyalty.
```DAX
Tenure Level = IF('Customer Churn'[tenure] >= 0 && 'Customer Churn'[tenure] <= 12, "0-12 Months", IF('Customer Churn'[tenure] >= 13 && 'Customer Churn'[tenure] <= 24, "13-24 months", IF('Customer Churn'[tenure] >= 25 && 'Customer Churn'[tenure] <= 48, "25-48 Months", IF('Customer Churn'[tenure] > 48, "48+ Months"))))
```

- **Age Segment**: Classifies customers into Senior or Youth categories based on their age.
```DAX
Age Segment = IF('Customer Churn'[seniorcitizen] = "1", "Senior", "Youth")
```

## DAX Measures
These measures summarize data to answer key business questions related to churn and performance.

- **Total Customers**: Counts all customers.
```DAX
Total Customers = COUNT('Customer Churn'[customerid]) 
```

- **Total Subscribed**: Counts all subscribed services.
```DAX
Total Subscribed = COUNT('Service Type'[service])  
```

- **Total Tech Tickets**: Sums technical support tickets.
```DAX
Total Tech Tickets = SUM('Customer Churn'[numtechtickets])
```

- **Total Admin Tickets**: Sums administrative support tickets.
```DAX
Total Admin Tickets = SUM('Customer Churn'[numadmintickets])
```
 
- **Churn Customers**: Counts the number of customers who have left.
```DAX
Churn Customers = CALCULATE(COUNT('Customer Churn'[churn]), FILTER('Customer Churn', 'Customer Churn'[churn] = "Yes"))
```

- **Churn Rate %**: Shows the ratio of churned customers to total customers.
```DAX
Churn Rate % = DIVIDE('Customer Churn Measure'[Churn Customers], [Total Customers], 0)
```
---
These Calculated Column and DAX measures will help generate actionable insights for visualizations, enabling PhoneNow and PwC Switzerland to identify trends and develop strategies for improving customer retention.

<table style="width:100%; border-collapse: collapse; text-align: center;">
  <tr>
    <td style="width:50%; padding:10px; text-align: left;">
      ⏪ <a href="https://mramadhankesapi.github.io/Data-Preparation-Processes_for_PhoneNow...Customer-Churn/" style="text-decoration: none; font-weight: bold; color: #007bff;">Data Preparation on PostgreSQL</a>
    </td>
    <td style="width:50%; padding:10px; text-align: right;">
      <a href="https://mramadhankesapi.github.io/PhoneNow-Customer-Churn-Analytics/" style="text-decoration: none; font-weight: bold; color: #007bff;">📊 PhoneNow: Customer Churn Analytics</a> ⏩
    </td>
  </tr>
</table>
