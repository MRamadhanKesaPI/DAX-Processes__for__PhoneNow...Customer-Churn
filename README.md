# DAX Measures for PhoneNow: Customer Churn

Cleaned data from PostgreSQL is now connected to Power BI. All numeric and monetary values are correctly formatted. the DAX measures are designed to provide clear insights into customer churn and its drivers. The goal is to identify the factors contributing to churn and to support strategies for improving retention. 

Simple DAX measures are used to answer key questions without relying on date information. These measures include:
1. **Calculated Columns**: Defined at the row level to classify and compute new fields.
2. **DAX Measures**: Aggregate data for analysis and visualization.

## Calculated Columns
These columns categorize or calculate values at the row level before aggregating data:

- **Delivery Type**: Categorizes orders as either Delivery or Pick Up based on order activity.
```DAX
Delivery = IF(order_activity[delivery_1] = "True", "Delivery", "Pick Up")
```

- **Stock Remaining**: Calculates the proportion of remaining stock in relation to total inventory.
```DAX
Stock Remaining = DIVIDE(inventory_management_2[inventory_balance], inventory_management_2[total_inventory], 0)
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

These Calculated Column and DAX measures will help generate actionable insights for visualizations, enabling PhoneNow and PwC Switzerland to identify trends and develop strategies for improving customer retention.
