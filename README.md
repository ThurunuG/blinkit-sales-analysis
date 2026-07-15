# 🛒 Blinkit Sales Analysis - SQL & Power BI

## 📌 Project Overview

The **Blinkit Sales Analysis** project focuses on analysing grocery retail sales data to identify business insights related to product performance, outlet performance, customer preferences, and sales trends.

This project uses **SQL for data cleaning, transformation, and analysis** and can be visualized using **Power BI dashboards** to provide interactive business intelligence.

The analysis helps understand sales patterns, product categories, outlet characteristics, and key performance indicators (KPIs) to support data-driven decision-making.

---

# 🎯 Project Objectives

The main objectives of this project are:

- Clean and standardize raw Blinkit sales data.
- Calculate important business KPIs.
- Analyse sales performance across different categories.
- Identify top-performing product types.
- Compare outlet performance.
- Understand customer purchasing patterns.
- Generate insights for business improvement.

---

# 📂 Dataset Information

The dataset contains retail transaction information including:

- Item details
- Item categories
- Fat content classification
- Outlet information
- Sales values
- Customer ratings
- Product visibility
- Outlet characteristics

---

# 🧹 Data Cleaning

## Item Fat Content Standardization

The `Item_Fat_Content` column contained inconsistent values:

Before cleaning:

```
LF
low fat
Low Fat
reg
Regular
```

These values were standardized into:

```
Low Fat
Regular
```

### SQL Query:

```sql
UPDATE blinkit_data
SET Item_Fat_Content = 
    CASE 
        WHEN Item_Fat_Content IN ('LF', 'low fat') THEN 'Low Fat'
        WHEN Item_Fat_Content = 'reg' THEN 'Regular'
        ELSE Item_Fat_Content
    END;
```

Verification:

```sql
SELECT DISTINCT Item_Fat_Content 
FROM blinkit_data;
```

---

# 📊 Key Performance Indicators (KPIs)

## 1. Total Sales

Calculates the overall revenue generated.

```sql
SELECT CAST(SUM(Total_Sales) / 1000000.0 AS DECIMAL(10,2)) 
AS Total_Sales_Million
FROM blinkit_data;
```

---

## 2. Average Sales

Calculates average sales per transaction.

```sql
SELECT CAST(AVG(Total_Sales) AS INT) 
AS Avg_Sales
FROM blinkit_data;
```

---

## 3. Number of Items Sold

Counts total transactions/items.

```sql
SELECT COUNT(*) AS No_of_Orders
FROM blinkit_data;
```

---

## 4. Average Customer Rating

Calculates average product rating.

```sql
SELECT CAST(AVG(Rating) AS DECIMAL(10,1)) 
AS Avg_Rating
FROM blinkit_data;
```

---

# 📈 Sales Analysis

## 1. Total Sales by Fat Content

Analyses revenue contribution based on product fat category.

```sql
SELECT 
Item_Fat_Content,
CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Item_Fat_Content;
```

---

## 2. Total Sales by Item Type

Identifies best-performing product categories.

```sql
SELECT 
Item_Type,
CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Item_Type
ORDER BY Total_Sales DESC;
```

---

## 3. Fat Content Sales by Outlet Location

Compares Low Fat and Regular product sales across outlet locations.

Analysis includes:

- Outlet Location Type
- Low Fat Sales
- Regular Sales

Uses SQL Pivot for better comparison.

---

## 4. Sales by Outlet Establishment Year

Analyses how outlet age impacts sales performance.

```sql
SELECT 
Outlet_Establishment_Year,
CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Outlet_Establishment_Year
ORDER BY Outlet_Establishment_Year;
```

---

## 5. Percentage Sales Contribution by Outlet Size

Calculates sales contribution from different outlet sizes.

Outlet categories:

- Small
- Medium
- Large

The analysis identifies which outlet sizes generate the highest revenue.

---

## 6. Sales by Outlet Location Type

Analyses sales performance based on geographic outlet classification.

```sql
SELECT 
Outlet_Location_Type,
CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Outlet_Location_Type
ORDER BY Total_Sales DESC;
```

---

## 7. Complete Outlet Performance Analysis

Provides multiple metrics by outlet type:

Metrics:

- Total Sales
- Average Sales
- Number of Items Sold
- Average Rating
- Average Item Visibility

```sql
SELECT 
Outlet_Type,
CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales,
CAST(AVG(Total_Sales) AS DECIMAL(10,0)) AS Avg_Sales,
COUNT(*) AS No_Of_Items,
CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating,
CAST(AVG(Item_Visibility) AS DECIMAL(10,2)) AS Item_Visibility
FROM blinkit_data
GROUP BY Outlet_Type
ORDER BY Total_Sales DESC;
```

---

# 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| SQL Server | Data cleaning and analysis |
| Power BI | Dashboard visualization |
| Excel / CSV | Dataset source |
| DAX | KPI calculations |

---

# 📂 Repository Structure

```
Blinkit-Sales-Analysis/
│
├── Dataset/
│   └── blinkit_data.csv
│
├── SQL/
│   └── blinkit_analysis_queries.sql
│
├── Dashboard/
│   └── Blinkit_Sales_Dashboard.pbix
│
├── Screenshots/
│   └── dashboard_preview.png
│
└── README.md
```

---

# 🔄 Project Workflow

## Step 1: Data Import

Imported raw Blinkit sales data into SQL database.

---

## Step 2: Data Cleaning

Performed:

- Data standardization
- Category correction
- Duplicate checking
- Data validation

---

## Step 3: Exploratory Data Analysis

Analysed:

- Sales trends
- Product categories
- Outlet performance
- Customer ratings

---

## Step 4: Dashboard Development

Created interactive visualizations showing:

- Sales KPIs
- Product performance
- Outlet insights
- Business trends

---

# 📊 Business Insights Generated

The analysis provides insights into:

✅ Overall revenue performance  
✅ Best-selling product categories  
✅ Fat content sales contribution  
✅ Outlet performance comparison  
✅ Outlet size impact on revenue  
✅ Location-based sales trends  
✅ Customer satisfaction levels  

---

# 🚀 Future Improvements

Possible enhancements:

- Sales forecasting using Machine Learning.
- Customer segmentation analysis.
- Real-time Blinkit API integration.
- Automated reporting pipeline.
- Predictive inventory management.

---

# 👨‍💻 Author

**Thurunu Gunarathna**

Computer Science Graduate

Skills:

- SQL
- Power BI
- Data Analytics
- Python
- Machine Learning

---

# 📄 License

This project is created for educational and portfolio purposes.
