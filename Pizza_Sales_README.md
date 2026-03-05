# 🍕 Pizza Sales — SQL Analysis Project

> *Analyzing pizza sales data using MySQL to uncover business insights across orders, revenue, products, and customer behavior.*

---

## 📌 Business Problem

The stakeholder — a pizza restaurant — wanted to understand their sales data better to make smarter operational and menu decisions. The key questions they needed answered were:

- How many total orders were placed and what was the total revenue?
- Which pizza is the most expensive on the menu?
- What size do customers order the most?
- Which pizza types and categories sell the most?
- When during the day are orders the highest?
- Which pizzas generate the most revenue?
- How does each category contribute to overall revenue?
- What does the cumulative revenue growth look like over time?
- Which are the top 3 revenue-generating pizzas within each category?

The goal was to write structured SQL queries — from basic aggregations to advanced window functions — and extract actionable insights from raw transactional data.

---

## 📂 Dataset

| Detail | Info |
|---|---|
| **Source** | Pizza Sales dataset (2015) |
| **Time Period** | Full Year 2015 |
| **Total Tables** | 4 |
| **Database** | pizzasales (MySQL) |

### Table Structure

| Table | Rows | Key Columns |
|---|---|---|
| `orders` | 21,350 | order_id, order_date, order_time |
| `orders_details` | 48,620 | order_details_id, order_id, pizza_id, quantity |
| `pizzas` | 96 | pizza_id, pizza_type_id, size, price |
| `pizza_types` | 32 | pizza_type_id, name, category, ingredients |

---

## 🛠 Tools Used

- **MySQL** — Database creation, data import, and all query execution
  - `CREATE TABLE`, `LOAD DATA INFILE` for setup
  - `JOIN`, `GROUP BY`, `ORDER BY`, `LIMIT` for aggregations
  - Subqueries for percentage calculations
  - Window Functions (`RANK() OVER`, `SUM() OVER`) for advanced analysis

---

## 🔍 Analysis & Insights

**Q1. Retrieve the total number of orders placed.**
→ **21,350 total orders** were placed in 2015 — averaging approximately 58 orders per day throughout the year.

---

**Q2. Calculate the total revenue generated from pizza sales.**
→ Total revenue for 2015 came to **$817,860.05** — roughly $2,241 in revenue generated every single day.

---

**Q3. Identify the highest-priced pizza.**
→ **The Greek Pizza** is the most premium item on the menu at **$35.95**, significantly higher than the average pizza price.

---

**Q4. Identify the most common pizza size ordered.**
→ **Large (L)** is the most popular size with **18,526 orders** — nearly 39% of all orders. XXL was barely ordered with just 28 orders all year.

| Size | Order Count |
|---|---|
| Large (L) | 18,526 |
| Medium (M) | 15,385 |
| Small (S) | 14,137 |
| XL | 544 |
| XXL | 28 |

---

**Q5. List the top 5 most ordered pizza types along with their quantities.**
→ The top 5 pizzas are remarkably close — only 82 units separate rank 1 from rank 5, showing near-equal demand across the board.

| Rank | Pizza | Units Sold |
|---|---|---|
| 🥇 1 | The Classic Deluxe Pizza | 2,453 |
| 🥈 2 | The Barbecue Chicken Pizza | 2,432 |
| 🥉 3 | The Hawaiian Pizza | 2,422 |
| 4 | The Pepperoni Pizza | 2,418 |
| 5 | The Thai Chicken Pizza | 2,371 |

---

**Q6. Find the total quantity ordered for each pizza category.**
→ **Classic** dominates in quantity with 14,888 units. All four categories are reasonably balanced, suggesting a well-rounded menu.

| Category | Units Sold |
|---|---|
| Classic | 14,888 |
| Supreme | 11,987 |
| Veggie | 11,649 |
| Chicken | 11,050 |

---

**Q7. Determine the distribution of orders by hour of the day.**
→ There are two clear peak windows — **Lunch (12 PM–1 PM)** and **Dinner (5 PM–6 PM)**. 12 PM is the single busiest hour with 2,520 orders. Before 11 AM, the shop is nearly empty.

---

**Q8. Find the category-wise distribution of pizza types.**
→ Supreme and Veggie have the most variety (9 types each). Chicken has the fewest types (6) but still moves 11,050 units — showing the highest demand per type ratio.

---

**Q9. Calculate the average number of pizzas ordered per day.**
→ On average, **138 pizzas** were ordered every day in 2015. This is a reliable benchmark for daily prep, staffing, and inventory planning.

---

**Q10. Determine the top 3 most ordered pizza types based on revenue.**
→ Chicken pizzas dominate revenue despite not leading in quantity. This tells us Chicken pizzas are priced higher and generate more money per order.

| Rank | Pizza | Revenue |
|---|---|---|
| 🥇 1 | The Thai Chicken Pizza | $43,434.25 |
| 🥈 2 | The Barbecue Chicken Pizza | $42,768.00 |
| 🥉 3 | The California Chicken Pizza | $41,409.50 |

---

**Q11. Calculate the percentage contribution of each pizza category to total revenue.**
→ Revenue is strikingly balanced across all four categories — no single category dominates. Classic leads with 26.91%, but Veggie is just 3.23 percentage points behind.

| Category | Revenue Share |
|---|---|
| Classic | 26.91% |
| Supreme | 25.46% |
| Chicken | 23.96% |
| Veggie | 23.68% |

---

**Q12. Analyze the cumulative revenue generated over time.**
→ This query uses a **Window Function** (`SUM() OVER ORDER BY`) to calculate a running revenue total from Day 1 to Day 365. By January 10th alone, the shop had already crossed $23,990. Full year ends at $817,860.

---

**Q13. Determine the top 3 most ordered pizza types by revenue for each category.**
→ This uses `RANK() OVER (PARTITION BY category)` — an advanced window function that ranks pizzas independently within each category. Thai Chicken Pizza ($43,434) is the single highest revenue earner across all categories.

---

## 📊 Visualizations

> All visualizations are available in the PowerPoint presentation attached to this repository.

- 📊 **Bar Chart** — Order Count by Pizza Size (Q4)
- 📊 **Horizontal Bar Chart** — Units Sold by Category (Q6)
- 📈 **Line Chart** — Orders by Hour of the Day with peak highlights (Q7)
- 🥧 **Pie Chart** — Revenue Contribution % by Category (Q11)
- 🏆 **Ranked Cards** — Top 5 Pizzas by Quantity (Q5)
- 🏆 **Ranked Cards** — Top 3 Pizzas by Revenue (Q10)

---

## 💡 Recommendations

Based on the analysis, here are actionable suggestions for the business:

1. **Focus staffing on 12 PM and 6 PM** — These are the two peak windows. Understaffing during these hours means lost orders and poor customer experience.

2. **Push Large size combos** — Large is already the most popular size at 39% of all orders. Combo deals or meal bundles around Large pizzas could increase average order value.

3. **Promote Chicken pizzas more aggressively** — They generate the most revenue despite lower quantity sold. Featured placement on the menu or upselling at checkout could significantly lift revenue.

4. **Investigate XXL demand** — Only 28 XXL orders were placed all year. Either promote it or consider dropping it to simplify inventory.

5. **Morning hours need a strategy** — Almost zero orders before 11 AM. A breakfast pizza or early-bird promotion could open a completely new revenue window.

6. **Leverage Veggie category growth** — With the same number of types as Supreme (9 each) and nearly equal revenue share (23.68%), the Veggie category has a strong audience worth targeting with dedicated promotions.

---

## 🗂 SQL Concepts Used

| Concept | Used In |
|---|---|
| `COUNT`, `SUM`, `ROUND` | Q1, Q2, Q9 |
| `JOIN` (multi-table) | Q2, Q3, Q5, Q6, Q10, Q11, Q13 |
| `GROUP BY` + `ORDER BY` | Q4, Q5, Q6, Q7, Q8 |
| `LIMIT` | Q3, Q5, Q10 |
| `HOUR()` function | Q7 |
| Subquery inside `SELECT` | Q11 |
| Subquery inside `FROM` | Q9, Q12, Q13 |
| `SUM() OVER (ORDER BY)` | Q12 |
| `RANK() OVER (PARTITION BY)` | Q13 |

---

## 🚀 How to Run This Project

1. **Install MySQL** (version 8.0 recommended) and open MySQL Workbench or any SQL client.

2. **Create the database** by running `00_general_queries.sql`:
   ```sql
   CREATE DATABASE pizzasales;
   USE pizzasales;
   ```

3. **Create the tables** using the `CREATE TABLE` statements inside `00_general_queries.sql`.

4. **Import the CSV data** — Place the CSV files in your MySQL secure upload directory and run the `LOAD DATA INFILE` commands from `00_general_queries.sql`.
   > Tip: Run `SHOW VARIABLES LIKE 'secure_file_priv';` to find your upload path.

5. **Run the queries** — Each SQL file is numbered and self-contained:
   - `01_total_orders.sql` → Q1
   - `02_total_revenue.sql` → Q2
   - ... and so on up to `13_top3_per_category.sql`

6. **View results** — Each query file has a comment at the top explaining what it does, followed by the query and the expected output.

> **Dataset files required:** `orders.csv`, `order_details.csv`, `pizzas.csv`, `pizza_types.csv`

---

## 📁 Repository Structure

```
Pizza-Sales-SQL/
│
├── datasets/
│   ├── orders.csv
│   ├── order_details.csv
│   ├── pizzas.csv
│   └── pizza_types.csv
│
├── queries/
│   ├── 00_general_queries.sql
│   ├── 01_total_orders.sql
│   ├── 02_total_revenue.sql
│   ├── 03_highest_priced_pizza.sql
│   ├── 04_common_pizza_size.sql
│   ├── 05_top5_pizza_types.sql
│   ├── 06_category_quantity.sql
│   ├── 07_orders_by_hour.sql
│   ├── 08_category_wise_pizzas.sql
│   ├── 09_avg_pizzas_per_day.sql
│   ├── 10_top3_pizzas_revenue.sql
│   ├── 11_percentage_contribution.sql
│   ├── 12_cumulative_revenue.sql
│   └── 13_top3_per_category.sql
│
├── Pizza_Sales_SQL_Analysis.pptx
├── Pizza_Sales_SQL_Report.docx
└── README.md
```

---

## 🙋 About the Analyst

**Ashish Sharma**
Aspiring Data Analyst | SQL Project #3
📧 youremail@example.com
🔗 [LinkedIn Profile](https://linkedin.com)
🐙 [GitHub Profile](https://github.com/RockingAshish)

---

*This project was completed as part of my data analysis learning journey. Feedback and suggestions are always welcome!*
