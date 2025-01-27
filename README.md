# SQL_Coffee_Sales_Analysis

# ☕ Coffee Sales Analysis Dashboard  

## 📖 Overview  
We analyzed transaction data for **Maven Roasters**, a fictitious coffee shop with three NYC locations, to derive actionable insights. This project demonstrates data cleaning, transformation, and visualization techniques using **SQL** and **Excel**.

---

## 🎯 Objectives  
- 🔍 Understand sales trends by day, hour, and month.  
- 🏆 Identify top-performing products and categories.  
- 📈 Optimize operational efficiency and pricing strategy.  
- 🎨 Present insights through a dynamic Power BI dashboard.

---

## 📊 Data Model  

The dataset contains a single table with transaction data.

## 🛠️ Tools Used  
- 🗄️ **SQL**: Data cleaning and transformation.  
- 📑 **Excel**:: Interactive visualizations and insights.

- ## 🎯 SQL Highlights  

### **Key Queries & Functions**  
The project makes extensive use of advanced SQL techniques, including:  
- **Aggregations:** `SUM()`, `COUNT()`, `MAX()`, `MIN()` for revenue, transactions, and price analysis.  
- **Date & Time Functions:** `DAYNAME()`, `MONTHNAME()`, `HOUR()` to analyze trends across time dimensions.  
- **Ranking:** `RANK()` for identifying top products and low-revenue hours across stores.  
- **Window Functions:** `SUM() OVER()`, `RANK() OVER()` for revenue percentage calculations and performance ranking.  
- **CTEs & Views:** Modularized queries for simplifying complex logic, e.g., `Storewise_hourly_sales`.
- 
## ⚙️ Database Setup and Data Loading  

### **Step 1: Create the Database and Table**  
Run the following SQL commands to set up the database and table structure in your SQL environment (e.g., MySQL, MariaDB):  

```sql
-- Create the database
CREATE DATABASE COFFEE_SALES;

-- Switch to the created database
USE COFFEE_SALES;

-- Create the table structure
CREATE TABLE coffee_sales_analysis (
    transaction_id INT,
    transaction_date VARCHAR(50),
    transaction_time VARCHAR(50),
    transaction_qty INT,
    store_id INT,
    store_location VARCHAR(50),
    product_id INT,
    unit_price DOUBLE,
    product_category VARCHAR(50),
    product_type VARCHAR(50),
    product_detail VARCHAR(50),
    product_size VARCHAR(50),
    CONSTRAINT pk PRIMARY KEY (transaction_id)
);

### Step 2: Loading Data

```bash
# Log in to MySQL
mysql -u [username] -p

# Use the COFFEE_SALES database
USE COFFEE_SALES;

# Load data into the table
LOAD DATA INFILE '/path/to/coffee_sales_data.csv' 
INTO TABLE coffee_sales_analysis 
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"' 
LINES TERMINATED BY '\n'
IGNORE 1 ROWS 
(transaction_id, transaction_date, transaction_time, transaction_qty, store_id, store_location, product_id, unit_price, product_category, product_type, product_detail, product_size);

### Step 3: Update and Modify Table Data

```sql
-- Convert the transaction_date to proper date format
UPDATE coffee_sales_analysis
SET transaction_date = STR_TO_DATE(transaction_date, '%d-%m-%Y');

-- Modify the transaction_time column to TIME data type
ALTER TABLE coffee_sales_analysis
MODIFY transaction_time TIME;


## 📌 Key Business Questions  

### 1️⃣ **How do total orders vary by day of the week?**  
- **Insights:**
  - Friday is the busiest day, followed by Monday and Thursday, each with over 21.5K transactions.
  - Saturday is the slowest day. Weekend transactions are generally low.  

### 2️⃣ **What are the peak ordering hours?**  
- **Insights:**
  - Morning hours (7 AM - 11 AM) see the most transactions, peaking between 10 AM and 11 AM.  
  - Post-7 PM, transactions drop sharply across all locations except Astoria.  

### 3️⃣ **What is the monthly sales trend?**  
- **Insights:**
  - Revenue rises consistently after February, with summer months contributing the highest sales due to increased outdoor activities.

### 4️⃣ **What are the best-performing categories?**  
- **Insights:**
  - Coffee and Tea dominate sales.  
  - Flavors and Packaged Chocolates generate only ~$37K and should be reevaluated for menu optimization.  

### 5️⃣ **What is the price range for each category?**  
- **Insights:**
  - Coffee Beans have the highest price range.  
  - Flavors show no price variation, indicating potential pricing inefficiency.  

### 6️⃣ **What are the top 10 products?**  
- **Insights:**
  - *Barista Espresso* generates the highest revenue, followed by *Brewed Chai Tea* and *Hot Chocolate*.  
  - These top 10 products contribute 80% of total revenue. Inventory for these items should be prioritized.  

### 7️⃣ **Are there exceptions in top products across locations?**  
- **Insights:**
  - Top products are consistent across locations, except Astoria, where Herbal Tea ranks higher.  

### 8️⃣ **What are the slow hours across stores?**  
- **Insights:**
  - After 8 PM, Hell’s Kitchen and Lower Manhattan see a significant revenue drop.  
  - Astoria performs well even during slow hours.  

### 9️⃣ **What is the sales scenario post-5 PM?**  
- **Insights:**
  - Astoria’s revenue remains high until closing at 8 PM.  
  - Hell’s Kitchen and Lower Manhattan remain open longer but with low sales.

## 📈 Recommendations  

1. **📅 Daily Operations**  
   - Focus inventory on Mondays, Thursdays, and Fridays.  
   - Introduce summer weekend promotions to boost footfall on slower weekend days.  

2. **🏢 Location-Specific Changes**  
   - Extend Astoria’s operating hours beyond 8 PM to capitalize on evening revenue.  
   - Reduce staffing at Hell’s Kitchen and Lower Manhattan after 8 PM.  

3. **💵 Pricing Strategy**  
   - Slightly increase prices for Coffee and Tea to enhance profitability without losing demand.  
   - Reevaluate underperforming high-priced items like Civet Cat Coffee.  

4. **📋 Menu Optimization**  
   - Remove low-performing categories like Flavors and Packaged Chocolates.  
   - Streamline the menu to improve customer experience and reduce inventory complexity.  

5. **📦 Inventory Management**  
   - Prioritize inventory for top-performing products (*Barista Espresso*, *Brewed Chai Tea*, etc.).  
   - Reduce stock for slow-moving and high-cost items.  

