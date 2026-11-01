# Pizza Place Sales Analysis Dashboard | Power BI

## About the Project

This is a Power BI project I created using the Pizza Place dataset from Maven Analytics. The goal was to understand the restaurant's sales performance, identify popular pizza varieties, analyze ordering patterns, and find areas where the business can improve.

I focused on understanding the business questions behind the data rather than just creating visualizations.

## Tools Used

- Power BI – Dashboard and visualizations
- Power Query – Data cleaning and transformation
- DAX – Measures and calculated columns
- CSV – Source datasets

## Dataset Overview

The dataset contains pizza sales records for 2015 across four files:

- `orders.csv` – Order ID, date and time
- `order_details.csv` – Order ID, pizza ID and quantity
- `pizzas.csv` – Pizza ID, size and price
- `pizza_types.csv` – Pizza names, categories and ingredients

**Dataset statistics:**

- 21,350 unique orders
- 49,574 pizzas sold
- 48,620 order-detail records

## Business Questions

1. How much revenue did the restaurant generate?
2. How many orders were placed and pizzas sold?
3. Which months generated the highest revenue?
4. Which weekdays and hours received the most orders?
5. Which pizza categories and sizes generated the most revenue?
6. Which pizza varieties were the most and least popular?
7. How is the product variety distributed across pizza sizes?

## Key DAX Formulas

**1. Total Revenue**

```dax
Total Revenue =
SUMX(
    order_details,
    RELATED(pizzas[price]) * order_details[quantity]
)
```

**2. Total Orders**

```dax
Total Orders =
DISTINCTCOUNT(orders[order_id])
```

**3. Total Pizzas Sold**

```dax
Total Pizzas Sold =
SUM(order_details[quantity])
```

**4. Average Order Value**

```dax
Average Order Value =
DIVIDE([Total Revenue], [Total Orders], 0)
```

**5. Average Pizzas Per Order**

```dax
Avg Pizzas Per Order =
DIVIDE([Total Pizzas Sold], [Total Orders], 0)
```

**6. Average Orders Per Day**

```dax
Avg Orders Per Day =
DIVIDE(
    [Total Orders],
    DISTINCTCOUNT(orders[date]),
    0
)
```

**7. Day Name**

```dax
Day Name =
FORMAT(orders[date], "dddd")
```

**8. Day Number (for sorting)**

```dax
Day Number =
WEEKDAY(orders[date], 2)
```

**9. Order Hour**

```dax
Order Hour =
HOUR(orders[time])
```

**10. Week Start**

```dax
Week Start =
orders[date] - WEEKDAY(orders[date], 2) + 1
```

## Dashboard Features

- KPI cards for overall sales performance.
- Monthly revenue trend.
- Orders by weekday and hour using a heatmap.
- Revenue comparison by pizza category and size.
- Top 10 pizza varieties by revenue.
- Bottom 5 pizza varieties by sales.
- Product count by pizza size.

## Key Insights

- July recorded the highest revenue and order volume in the dataset.
- Ordering activity varies across weekdays and hours.
- Different pizza categories and sizes contribute differently to total revenue.
- Some pizza varieties have lower sales volumes and may need further evaluation.
- Product availability across sizes does not necessarily reflect actual customer demand.

## Business Recommendations

- Plan staff availability around peak ordering hours.
- Review low-selling pizzas by considering their pricing, costs and profit margins.
- Use monthly sales trends to improve inventory planning.
- Evaluate demand for individual pizza sizes before making menu changes.
- Test targeted promotions for selected pizza categories and track their results.

## Dataset Source

Maven Analytics – Pizza Place Sales Dataset
[https://www.mavenanalytics.io/](https://www.mavenanalytics.io/)
