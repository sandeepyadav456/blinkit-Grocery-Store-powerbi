# 🛒 Blinkit Sales & Outlet Performance Analysis | Power BI Case Study

An end-to-end **Power BI** analysis of Blinkit retail data, built as a business case study for the **VP of Merchandising**. The report is split into three dashboards that connect outlet format, location, item attributes, ratings and outlet age to sales, so that assortment planning and outlet-expansion budgets can be set with evidence instead of assumptions.

> **TL;DR:** Supermarket Type1 drives ~65% of sales, Grocery Stores sell ~40% less per outlet, Tier 3 locations lead, shelf visibility doesn't translate into sales, and ratings are a weak predictor of sales.

---

## 📌 Business Problem

Assortment planning and outlet-expansion budgets are currently being set without data to back them. The VP of Merchandising needs answers to four questions:

| # | Question |
|---|----------|
| 1 | Which **outlet formats and locations** drive the most sales? |
| 2 | Which **item categories** are over- or under-performing relative to **shelf visibility**? |
| 3 | Do **item ratings** actually predict sales? |
| 4 | How does **outlet age** (establishment year) affect performance? |

---

## 🗂️ Dataset

The report is built on a single table, **`BlinkIT_Grocery_Data_Raw`**, covering **10 outlets** and **16 item categories**, with about **1.20M** in total sales.

| Column | Description |
|--------|-------------|
| `outlet_identifier` | Unique outlet ID (e.g. OUT010) |
| `outlet_type` | Grocery Store, Supermarket Type1 / Type2 / Type3 |
| `outlet_location_type` | City tier (Tier 1 / 2 / 3) |
| `outlet_size` | Small, Medium or High |
| `outlet_establishment_year` | Year the outlet was established |
| `item_type` | Item category (16 categories) |
| `item_fat_content` | Low Fat or Regular |
| `item_visibility` | Share of display area allocated to the item |
| `rating` | Customer rating of the item (1–5) |
| `sales` | Sales value |

### DAX Measures

| Measure | Purpose |
|---------|---------|
| `Total_Sales` | Overall sales |
| `Total_Items` | Count of items |
| `Total_Outlets` | Number of outlets |
| `Total_Categories` | Number of item categories |
| `Avg_Rating` | Average customer rating |
| `Avg_Visibility` | Average shelf visibility |
| `Avg_Weight` | Average item weight |
| `Avg_Sales_Per_Outlet` | Total sales divided by number of outlets |

<!-- Optional: paste your DAX formulas here in a ```DAX code block -->

### 🧹 Data Cleaning
- **Item fat content:** standardised inconsistent labels (e.g. "LF", "low fat", "reg") into two clean categories, **Low Fat** and **Regular**.
- **Outlet size:** handled missing values so that each outlet has a single, consistent size.

<!-- Add any other steps you did, e.g. zero visibility values, duplicates, data types. -->

---

## 📊 Dashboards

### 1. Executive Summary
High-level view of the business.
- **KPIs:** Total Sales (1.20M), Total Items (34), Avg Rating (3.92), Total Outlets (10)
- **Visuals:** Top performing product categories, Total Sales by outlet location type (donut), Total Sales by outlet established year (line)
- **Slicers:** Outlet establishment year, outlet size, outlet location type, item fat content

![Executive Summary](images/executive-summary.png)

### 2. Product & Outlet Analysis
Connects item attributes to sales.
- **KPIs:** Avg Rating (3.92), Avg Visibility (0.07), Avg Weight (10.65), Total Categories (16)
- **Visuals:** Sales by outlet type, Sales by rating, Sales by item fat content, Sales by outlet size, Sales by item type vs item visibility (bubble/scatter)
- **Slicers:** Fat content, location type, outlet size, establishment year, outlet type

![Product & Outlet Analysis](images/product-outlet-analysis.png)

### 3. Outlet Performance
Outlet-level drill-down.
- **KPIs:** Avg Sales per Outlet (120.17K), Avg Rating (3.92), Total Categories (16), Total Outlets (10)
- **Visuals:** Sales by outlet identifier, Sales by outlet type, Sales by establishment year, detailed outlet table (sales, items, rating, visibility, weight, size)
- **Slicers:** Location type, outlet size, establishment year

![Outlet Performance](images/outlet-performance.png)

---

## 🔍 Key Insights

### 1️⃣ Which outlet formats and locations drive the most sales?
- **Supermarket Type1 is the sales engine**: about **0.79M of 1.20M (~65%)**, versus 0.15M for Grocery Stores and 0.13M each for Supermarket Type2 and Type3.
- That lead comes mostly from **outlet count** (6 of the 10 outlets are Type1). Per outlet, the supermarket formats perform about the same (~130K each).
- **Grocery Stores are the weak format**: roughly 74K–78K per outlet, around **40% below** the supermarket formats.
- **Tier 3 locations lead** with **472K (39.3%)**, followed by Tier 2 at 393K (32.7%) and Tier 1 at 336K (28.0%).

### 2️⃣ Which categories over/under-perform relative to shelf visibility?
- The top five item categories generate between **101K and 178K** in sales.
- Sales activity is concentrated among items with **low visibility (roughly 0–0.10)** and tapers off as visibility rises. More shelf visibility does **not** translate into more sales, so visibility allocation looks misaligned with demand.
- Items with high visibility but low sales are candidates for **re-allocating shelf space**.

### 3️⃣ Do ratings predict sales?
- Sales peak at **rating 4 (0.98M, ~82% of total sales)** and are much lower at rating 5 (0.10M).
- Because most items are rated around 4 (average 3.92), this chart mostly reflects **how many items sit in each rating band**, not that higher ratings drive more sales.
- **Takeaway:** rating alone is a weak predictor of sales and shouldn't be the only input for assortment decisions.

### 4️⃣ How does outlet age affect performance?
- Sales are **flat at about 130K per establishment year** from 2012 to 2022, so newer outlets don't perform worse than older ones.
- The oldest cohort (2011) is the exception at **78K**, which is a Grocery Store.
- The 2018 spike (**205K**) is not one strong outlet. It adds up to two outlets (OUT018 at ~131K and OUT019 at ~74K) that share that establishment year, so the chart shows **total** sales per year, not per outlet.
- **Takeaway:** **format matters more than age** in explaining performance.

### Other observations
- **Regular** fat-content items drive **64.6%** of sales versus 35.4% for Low Fat.

---

## 💡 Recommendations
1. **Prioritise Supermarket formats in expansion budgets**; Grocery Store outlets deliver markedly lower sales per outlet.
2. **Invest in Tier 3 and Tier 2 locations**, which together account for ~72% of sales.
3. **Rebalance shelf visibility** toward categories that sell well but get little visibility, and reduce space for high-visibility, low-sales items.
4. **Don't use ratings as the only assortment filter**; combine them with sales velocity and visibility.
5. **Plan expansion by format, not by outlet age.**

---

## ⚠️ Limitations & Next Steps
- **Small sample:** only 10 outlets, so format and age comparisons are based on very few data points per group.
- **No time dimension:** there is no date field, so seasonality and sales trends can't be analysed.
- **Totals vs averages:** the rating and establishment-year charts show total sales. Average sales per item or per outlet would remove the effect of group size.
- **Single flat table:** a star schema (separate outlet and item dimension tables) would make the model easier to scale.
- **Next steps:** add per-outlet averages by cohort, a visibility-vs-sales ratio by category, and a forecasting view if date data becomes available.

---

## 🛠️ Tools & Skills Used
- **Power BI Desktop**: data modelling, DAX measures, interactive dashboards
- **Power Query**: data cleaning and transformation
- **DAX**: KPI measures (Total Sales, Total Items, Avg Rating, Avg Visibility, Avg Weight, Total Categories, Total Outlets, Avg Sales per Outlet)
- **Data storytelling**: slicers, drill-down visuals, executive summary page

---

## 📁 Repository Structure
```
├── Blinkit_Grocery_Store.pbix   # Power BI report file
├── images/                      # Dashboard screenshots
│   ├── executive-summary.png
│   ├── product-outlet-analysis.png
│   └── outlet-performance.png
├── data/                        # Dataset (CSV/Excel)
└── README.md
```

> Update the file names above to match your repository.

## ▶️ How to Use
1. Clone or download this repository.
2. Open the `.pbix` file in **Power BI Desktop**.
3. Use the slicers (outlet size, location type, establishment year, fat content, outlet type) to explore each dashboard.

---

## 👤 Author
**Sandeep Gollar**
B.E. Computer Science & Engineering, Government Engineering College, Hassan
🔗 [LinkedIn](https://linkedin.com/in/sandeep-yadav-21161a379) | 💻 [GitHub](https://github.com/sandeepyadav456)

⭐ If you found this project useful, consider starring the repo!
