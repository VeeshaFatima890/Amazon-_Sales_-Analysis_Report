# 📊 Amazon Sales Analysis Report

## 📌 Project Overview
This project implements a **Python-based ETL (Extract, Transform, Load) pipeline** to process Amazon sales data and load it into **SQL Server** for analysis.  
The cleaned dataset is then used to answer business questions and build dashboards in **Power BI**.  

---

## ⚙️ Features
- Extract sales data from raw CSV file  
- Transform data:
  - Clean and format columns  
  - Handle missing/NULL values  
  - Convert dates and numeric fields  
- Load cleaned data into SQL Server  
- Run SQL queries for analytics  
- Visualize results with **Power BI**  

---

## 📂 Project Structure
Sales_Analytics/
│
├── Amazon Sale Report.csv # Raw sales dataset
├── Sales analytics.ipynb # Python ETL notebook
├── .gitignore # Git ignore rules
└── README.md # Project documentation



---

## 🛠️ Tech Stack
- **Python** → pandas, numpy, pyodbc/sqlalchemy  
- **SQL Server** → data storage & analytics  
- **Power BI** → visualization & dashboarding  

---

## 🚀 ETL Workflow
### 1️⃣ Extract
- Load raw sales data from `Amazon Sale Report.csv` using `pandas`.

### 2️⃣ Transform
- Clean text columns (trim spaces, lowercase normalization).  
- Replace missing values (`NaN`, `NA`, `null`) with `NULL` in SQL.  
- Convert dates into proper `datetime` objects.  
- Ensure numeric columns are properly cast.  

### 3️⃣ Load
- Use **pyodbc/sqlalchemy** to connect with SQL Server.  
- Load cleaned data into a SQL table `sales_data`.  

```python
import pandas as pd
import numpy as np
import pyodbc

# Extract
df = pd.read_csv("Amazon Sale Report.csv")

# Transform
df = df.replace(["", "NA", "NaN", "nan"], np.nan)
df['Date'] = pd.to_datetime(df['Date'], errors='coerce')
df.columns = df.columns.str.strip()

# Load
conn = pyodbc.connect(
    "DRIVER={SQL Server};SERVER=localhost;DATABASE=SalesAnalytics;Trusted_Connection=yes;"
)
cursor = conn.cursor()

for index, row in df.iterrows():
    cursor.execute("""
        INSERT INTO sales_data (Date, City, Category, Amount, Profit)
        VALUES (?, ?, ?, ?, ?)
    """, row.Date, row.City, row.Category, row.Amount, row.Profit)

conn.commit()
cursor.close()
conn.close()

Analytics & Business Questions

The dataset helps answer key questions such as:

Which cities contribute the most to sales?
→ Visualized using a bar chart in Power BI.

What is the average profit margin per category?
→ Group by category, calculate profit margin.

Which product categories generate the highest sales?
→ Category-wise sales totals.

Which month has the highest sales volume?
→ Time-series monthly aggregation.

📈 Sample Dashboard (Power BI)

Sales by City

Profit Margin by Category

Monthly Sales Trends

Top Product Categories

ow to Run the Project

Clone the repo:

git clone https://github.com/VeeshaFatima890/Amazon-_Sales_-Analysis_Report.git
Open Sales analytics.ipynb in Jupyter Notebook or VS Code.

Install dependencies:
pip install pandas numpy pyodbc sqlalchemy

Update your SQL Server connection string.

Run the notebook to load cleaned data into SQL.

Open Power BI, connect to SQL Server, and create dashboards.

Author
👩‍💻 Veesha Fatima
Data Analytics & AI Enthusiast
---


