# E-Commerce-SQL-Data-Analysis
![Banner](https://raw.githubusercontent.com/Prachibansal11/Zepto-SQL-Data-Analysis/a1de34c22ade16aaf7ea1d304ed9422990a2ff24/zepto-banner.jpg)

📌 **Project Overview**  
The goal is to simulate how actual data analysts in the e-commerce or retail industries work behind the scenes to use SQL to:

- ✅ Set up a messy, real-world e-commerce inventory database  
- ✅ Perform Exploratory Data Analysis (EDA) to explore product categories, availability, and pricing inconsistencies  
- ✅ Implement Data Cleaning to handle null values, remove invalid entries, and convert pricing from paise to rupees  
- ✅ Write business-driven SQL queries to derive insights around pricing, inventory, stock availability, revenue, and more  

---

📁 **Dataset Overview**  
The dataset was sourced from Kaggle and originally scraped from Zepto’s official product listings. It mimics what you’d typically encounter in a real-world e-commerce inventory system.

Each row represents a unique SKU (Stock Keeping Unit) for a product. Duplicate product names exist because the same product may appear multiple times in different package sizes, weights, discounts, or categories to improve visibility – exactly how real catalog data looks.

**🧾 Columns:**

| Column               | Description                                                 |
|----------------------|-------------------------------------------------------------|
| sku_id               | Unique identifier for each product entry (Primary Key)      |
| name                 | Product name as it appears on the app                        |
| category             | Product category like Fruits, Snacks, Beverages, etc.       |
| mrp                  | Maximum Retail Price (originally in paise, converted to ₹)  |
| discountPercent      | Discount applied on MRP                                      |
| discountedSellingPrice| Final price after discount (also converted to ₹)            |
| availableQuantity    | Units available in inventory                                 |
| weightInGms          | Product weight in grams                                      |
| outOfStock           | Boolean flag indicating stock availability                   |
| quantity             | Number of units per package (mixed with grams for loose produce) |

---

🔧 **Project Workflow**
### 1. Database & Table Creation  
We start by creating a SQL table with appropriate data types:
<pre> ```sql CREATE TABLE zepto ( sku_id SERIAL PRIMARY KEY, category VARCHAR(120), name VARCHAR(150) NOT NULL, mrp NUMERIC(8,2), discountPercent NUMERIC(5,2), availableQuantity INTEGER, discountedSellingPrice NUMERIC(8,2), weightInGms INTEGER, outOfStock BOOLEAN, quantity INTEGER ); ``` </pre>

### 2.
- Loaded CSV using **pgAdmin's import feature**.  


### 3. 🔍 Data Exploration  
- Counted the **total number of records** in the dataset  
- Viewed a **sample of the dataset** to understand structure and content  
- Checked for **null values** across all columns  
- Identified **distinct product categories** available in the dataset  
- Compared **in-stock vs out-of-stock** product counts  
- Detected **duplicate products** present multiple times, representing different SKUs (e.g., package size or weight variations)

---

### 4. 🧹 Data Cleaning  
- Identified and removed rows where **MRP** or **discounted selling price** was **zero**  
- Converted `mrp` and `discountedSellingPrice` from **paise to rupees** for consistency and readability  
  (e.g., 5000 paise → ₹50.00)

---

### 5. 📊 Business Insights  
- 🏷️ Found **Top 10 best-value products** based on highest discount percentage  
- 🚫 Identified **high-MRP products** that are currently **out of stock**  
- 💰 Estimated **potential revenue** for each product category using:  
  `discountedSellingPrice × availableQuantity`  
- 🧃 Filtered **expensive products (MRP > ₹500)** with minimal discount  
- 🏆 Ranked **Top 5 product categories** offering the **highest average discounts**  
- ⚖️ Calculated **price per gram** to identify **value-for-money products**  
- 📦 Grouped products based on **weight** into:  
  - Low (0–250g)  
  - Medium (251g–750g)  
  - Bulk (750g and above)  
- 🏋️ Measured **total inventory weight per product category** to understand stock volume distribution
