# Customer Churn Analysis Using MySQL

## Project Overview

Customer Churn Analysis is a database analytics project that explores customer subscriptions, payments, support interactions, and churn events using MySQL. It is designed to demonstrate how relational data can be organized, validated, and queried to understand customer retention and identify patterns associated with customers leaving a service.

The project uses a small **fictional dataset of 12 customers**. It is intended for learning and demonstration; its results should not be treated as statistically representative of real customers or as production business findings.

## Project Objectives

- Organize customer and service information in a relational database.
- Measure the historical proportion of customers with recorded churn events.
- Summarize active subscription revenue and average revenue per active customer.
- Compare churn across subscription plans and review recorded churn reasons.
- Examine payment failures and customer-support activity.
- Explore monthly churn patterns and simple rule-based customer-risk indicators.
- Demonstrate reusable database objects, data validation, and audit concepts.

## Data Model

The database contains five related tables:

| Table | Purpose |
|---|---|
| `customers` | Stores customer details and signup dates. |
| `subscriptions` | Stores each customer's plan, contract type, monthly charge, dates, and subscription status. |
| `payments` | Records payment dates, amounts, payment methods, and payment outcomes. |
| `support_tickets` | Stores customer issues, priority, resolution status, and resolution time. |
| `churn_events` | Records churn dates, reasons, and customer feedback. |

Primary keys identify records, while foreign keys connect related records. Additional constraints help protect data quality, including required fields, unique values, valid ranges, and permitted status values.

## Main Analysis Areas

### Customer and Subscription Overview
Review customer records, subscription plans, contract types, and subscription statuses. Data-validation queries help identify missing subscription records and inconsistencies between subscription status and churn-event records.

### Churn Metrics
Calculate the historical churn proportion for the sample and compare churn counts and percentages across subscription plans. These metrics describe the supplied dataset only and are not a period-specific or industry-standard churn rate.

### Churn Reasons and Trends
Summarize recorded reasons for churn and group churn events by month to make patterns easier to inspect.

### Revenue and Payments
Calculate monthly recurring revenue from active subscriptions, count active customers, estimate average revenue per active customer, and summarize successful and failed payments.

### Customer Support
Analyze support-ticket volume, priority, and resolution time. Compare support indicators across churn outcomes while aggregating ticket data carefully to avoid duplicate counts caused by joins.

### Rule-Based Risk Indicators
Combine support-ticket and payment indicators to classify eligible customers into illustrative risk categories. These are transparent demonstration rules, **not machine-learning predictions** and not validated risk scores.

## SQL Concepts Demonstrated

- Database and table design
- Primary keys, foreign keys, unique constraints, check constraints, and required fields
- Insert, update, delete, and data-validation operations
- Filtering, sorting, aggregate functions, grouping, and conditional expressions
- Inner joins and left joins
- Subqueries and common table expressions (CTEs)
- Date-based grouping and formatting
- Indexes and query-plan inspection with `EXPLAIN`
- Views for reusable summaries
- Stored procedures for date-range reporting
- Triggers for maintaining related status information and recording audit changes
- Transactions and rollback-based demonstrations

## Views, Stored Procedure, and Triggers

### Views
Reusable views provide customer-level churn summaries and consolidated customer-service indicators, reducing the need to repeatedly write the same joins.

### Stored Procedure
A date-range churn-reporting procedure summarizes churn events within a requested period, including the number of events, unique customers, and the first and last churn dates in that period.

### Triggers
The trigger examples demonstrate two database automation concepts:

- **Churn synchronization:** when a churn event is inserted, the related subscription status is synchronized with the churn outcome.
- **Audit logging:** changes to subscription status are recorded in an audit table so that changes can be reviewed.

The project includes demonstration steps to inspect the trigger behavior. Run these only in a test database and review any data-changing statements before execution.

## Indexing and Query Review

Indexes are included on selected columns commonly used for joins, date filters, and location-based or status-related analysis. `EXPLAIN` is used to inspect how MySQL plans to execute a query. Indexes can improve selected read operations, although their benefit depends on data size, query patterns, and the database environment.

## Technology

- **Database:** MySQL 8.0+
- **Recommended client:** MySQL Workbench or the MySQL command-line client
- **Language:** SQL

## How to Run the Project

1. Install or open MySQL 8.0 or later and connect using MySQL Workbench or the command-line client.
2. Review the database setup section of the companion SQL project file before executing it.
3. Be aware that the setup script includes a database-drop operation for a clean rebuild. Do not run it against a database containing data you need to keep.
4. Execute the SQL script in order so the tables and relationships exist before sample data and database objects are created.
5. Review the query results, then run the view, stored-procedure, and trigger demonstrations in a test environment.
6. Re-run validation queries after demonstrations to confirm the database is in the expected state.

## Limitations

- The dataset is synthetic and contains only 12 customers, so it is suitable for SQL practice rather than reliable business forecasting.
- The churn ratio is calculated from the supplied sample and should not be generalized to other populations or time periods.
- The risk categories use manually defined rules and are not trained or validated predictive models.
- Results can change if the sample data or demonstration operations are modified.
- Index performance depends on the database engine, data volume, and query workload.

## Future Enhancements

- Expand the dataset with more customers and a longer observation period.
- Add historical subscription changes and more detailed customer activity.
- Analyze churn by customer tenure, contract type, payment behavior, and support experience.
- Add automated data-quality checks and richer audit history.
- Build a dashboard that presents churn, retention, revenue, and support metrics.
- If predictive modeling is introduced, evaluate it with an appropriate validation process and clearly separate predictions from descriptive SQL analysis.

## Conclusion

This project demonstrates an end-to-end relational database workflow: structuring customer data, enforcing relationships and constraints, analyzing churn-related indicators, creating reusable database objects, and using triggers and transactions to illustrate data consistency and auditing. It provides a practical foundation for learning MySQL and presenting a database analytics project on GitHub.
