# Data-Modeling-Sales-Dashboard
## 📌 Project Overview
The project began with an **unnormalized dataset**.  
This table contained repeating groups, redundant information, and mixed attributes such as:

- Customer information (ID, Country) repeated for every transaction  
- Product details (Description, UnitPrice) repeated for every order line  
- Dates stored in raw format without a proper calendar dimension  

This design caused redundancy, inconsistency risks, and inefficiency for querying.

### Step 1 – Normalization
**Database normalization rules** (1NF → 2NF → 3NF) were applied to separate the data into logical tables:
- **Customers** → `CustomerID`, `Country`  
- **Products** → `StockCode`, `Description`, `UnitPrice`  
- **Orders** → `InvoiceNo`, `CustomerID`, `InvoiceDate`  
- **OrderDetails** → `InvoiceNo`, `StockCode`, `Quantity`  

This removed redundancy and ensured data integrity, resulting in a **3NF schema** suitable for operational use.

### Step 2 – Star Schema Transformation
To enable analytics and BI reporting, we **denormalized** the schema into a **Star Schema**:
- **FactSales** → `InvoiceNo`, `CustomerID`, `ProductID`, `DateID`, `Quantity`, `Revenue`  
- **DimCustomer** → `CustomerID`, `Country`  
- **DimProduct** → `ProductID`, `Description`, `UnitPrice`  
- **DimDate** → `DateID`, `Day`, `Month`, `Year`  

### Why the Transformation?
- **Unnormalized data**: messy, redundant, hard to query.  
- **Normalized (3NF)**: clean, consistent, efficient for transactions (OLTP).  
- **Star Schema**: optimized for analytics (OLAP), supports aggregations, filtering, and Power BI dashboards.  

➡️ Final BI pipeline:  
**Unnormalized Data ➝ 3NF (Normalized) ➝ Star Schema ➝ Power BI Dashboard.**

---

## 🛠 Tools & Technologies
- **Python (Pandas, SQLite)** → ETL and schema transformation  
- **Power BI** → Data visualization  
- **DAX** → Measures (Revenue, Orders, AOV, YTD Sales, etc.)  

---

## 📊 Dashboard Features
- **KPI Cards**:  
  - Total Revenue  
  - Total Quantity Sold  
  - Total Orders  
  - Average Order Value (AOV)  
  - Distinct Customers  

- **Line Chart**: Revenue trend by Year and Month  
- **Bar Chart**: Top 10 products by revenue   
- **Slicers**: Filter by Country  

---
