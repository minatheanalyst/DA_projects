Power BI Project: Café Business Optimization Dashboard
Overview

This Power BI dashboard offers a strategic, data-driven overview of café operations by analyzing revenue performance, product and category trends, customer behavior, promotional effectiveness, and transaction patterns. It enables decision-makers to optimize product offerings, refine marketing efforts, and improve customer value and operational efficiency.
Key Features
Revenue Analysis & Promo Code Effectiveness

    Identifies top-selling product categories such as Coffee-Based and Baked Goods

    Evaluates promotional code usage and impact:

        26% usage rate among transactions

        Promo code users show higher average tip values

    Supports bundling strategies and promotion targeting

Product and Category Performance

    Displays the top and bottom 5 SKUs by both revenue and sales volume

    Highlights opportunities for bundling and cross-selling

    Breaks down performance by major product categories

Customer Insights

    Segments customers into four behavioral categories:

        High-Frequency

        Mid-Value

        Occasional

        At-Risk

    Supports personalized loyalty programs and re-engagement campaigns

Payment Trends

    Analyzes payment method usage:

        Credit Card: 59%

        Cash: 32%

        Mobile Pay: 9%

    Informs strategies to increase mobile pay usage and streamline checkout

Business Objectives

    Improve sales of underperforming SKUs (e.g., Matcha Latte, Macchiato)

    Extend average basket size through product pairing and recommendations

    Increase customer lifetime value through loyalty initiatives

    Drive adoption of digital payments

    Inform decisions for café expansion based on performance trends

Dashboard Structure

The report consists of two main pages:

    Executive Overview
    Summarizes key business metrics, revenue insights, promotional effectiveness, and customer segmentation.

    Product and Category Breakdown
    Detailed analysis of SKU performance, category trends, units sold, and product-level promo usage.

Custom DAX Measures

-- Revenue and Transaction Metrics
TotalRevenue = SUM('Transactions'[Revenue])

TotalTransactions = DISTINCTCOUNT('Transactions'[TransactionID])

UniqueTransactions = DISTINCTCOUNT('Transactions'[TransactionID])

AvgBasketSize = 
AVERAGEX(
    VALUES(Transactions[TransactionID]),
    CALCULATE(COUNTROWS(Transactions))
)

AvgRevPerTransaction = 
AVERAGEX(
    VALUES('Transactions'[TransactionID]),
    CALCULATE(SUM('Transactions'[Revenue]))
)

-- Promotion Metrics
PromoSales = 
CALCULATE(
    SUM('Transactions'[Revenue]),
    'Transactions'[PromoCode] <> "NONE"
)

PromoUsageRate = 
DIVIDE(
    CALCULATE(COUNTROWS(Transactions), Transactions[PromoCode] <> "NONE"),
    COUNTROWS(Transactions)
)

PromoUsageRatioByProduct = 
DIVIDE(
    CALCULATE(COUNTROWS(Transactions), Transactions[PromoCode] <> "NONE"),
    COUNTROWS(Transactions)
)

-- Customer Metrics
Repeat Transactions = 
CALCULATE(
    DISTINCTCOUNT('Transactions'[TransactionID]),
    'Transactions'[CustomerType] = "Repeat"
)

RepeatRate = 
DIVIDE([Repeat Transactions], [TotalTransactions])

CustomerRepeatRate = 
DIVIDE(
    CALCULATE(DISTINCTCOUNT('Transactions'[CustomerID]), Transactions[CustomerType] = "Repeat"),
    CALCULATE(DISTINCTCOUNT('Transactions'[CustomerID]))
)

-- Volume Metrics
Units Sold = COUNTROWS('Transactions')

Data Sources

    POS Transactional Data (CSV / SQL extracts)

    Promo Code Redemptions and Usage Logs

    Customer Segmentation Model Output

    Product Category Mapping Table

Technical Setup

    Power BI Desktop (latest version)

    Python for Exploratory Data Analysis (EDA):

    import pandas as pd
    import numpy as np
    import sqlite3
    import matplotlib.pyplot as plt
    import seaborn as sns

    Microsoft Excel for product mapping and preprocessing

    Data Refresh Schedule: Daily via Power BI Gateway (8:00 AM CET)

Target Users

    Business Owners & General Managers – Strategic oversight and performance tracking

    Marketing Teams – Campaign development, promotions, and loyalty planning

    Operations Managers – Inventory, staffing, and process improvements

    Data Analysts – Trend analysis and advanced exploration

Planned Enhancements

    Predictive churn modeling

    Weekday vs. weekend behavior analysis

    Demographic segmentation (pending data availability)

    Integration with email marketing engagement data