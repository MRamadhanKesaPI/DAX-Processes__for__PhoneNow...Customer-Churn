# DAX Measures for PhoneNow: Customer Churn

Cleaned data from PostgreSQL is now connected to Power BI. All numeric and monetary values are correctly formatted. the DAX measures are designed to provide clear insights into customer churn and its drivers. The goal is to identify the factors contributing to churn and to support strategies for improving retention. 

Simple DAX measures are used to answer key questions without relying on date information. These measures include:

- Total Customers: Counts all customers.
```DAX
Total Customers = COUNT('Customer Churn'[customerid]) 
```

- Total Subscribed: Counts all subscribed services.
```DAX
Total Subscribed = COUNT('Service Type'[service])  
```

- Total Tech Tickets: Sums technical support tickets.
```DAX
Total Tech Tickets = SUM('Customer Churn'[numtechtickets])
```

- Total Admin Tickets: Sums administrative support tickets.
```DAX
Total Admin Tickets = SUM('Customer Churn'[numadmintickets])
```
 
- Churn Customers: Counts the number of customers who have left.
```DAX
Churn Customers = CALCULATE(COUNT('Customer Churn'[churn]), FILTER('Customer Churn', 'Customer Churn'[churn] = "Yes"))
```

- Churn Rate %: Shows the ratio of churned customers to total customers.
```DAX
Churn Rate % = DIVIDE('Customer Churn Measure'[Churn Customers], [Total Customers], 0)
```
These DAX measures will help generate actionable insights for visualizations, enabling PhoneNow and PwC Switzerland to identify trends and develop strategies for improving customer retention.
