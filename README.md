# Phone-Brand-Sales-Analysis-Data-Cleaning
The goal of this project was to analyze phone sales data, clean and prepare it for analysis using SQL, and create actionable visualizations in Tableau to identify trends, optimize discounts, and improve customer satisfaction.

# Phone Brand Sales Analysis - Data Cleaning and Visualization


## Dataset Cleaning and Preparation Process

### Tools Used
- **Database Management System:** SQL (for data cleaning and transformation)
- **Data Visualization:** Tableau (for dashboard creation)
- **Data Format:** CSV file (raw dataset)

---

### 1. Understanding the Dataset
The raw dataset was in CSV format and contained the following key fields:
- **Brand Name:** Manufacturer of the phone.
- **Model Name:** Phone model (e.g., iPhone 13 Pro Max).
- **Selling Price:** Final price after discounts.
- **Original Price:** Initial price before discounts.
- **Discount Percentage:** Percentage discount applied to the phone.
- **Ratings:** Customer ratings out of 5.
- **Features:** Product attributes like the presence of a camera, storage capacity, etc.
- and so on

---

### 2. Challenges in the Raw Data
The dataset had the following issues:
- **Missing Values:** Fields like ratings and discount percentages had null values.
- **Inconsistent Formatting:** Brand and model names had variations in spelling and capitalization.
- **Outliers:** Unrealistic values in price and ratings (e.g., negative discounts, ratings above 5).
- **Duplicate Records:** Duplicate entries for certain phone models.
- **Data Type Errors:** Numeric columns like Selling Price were stored as text.

---

### 3. Cleaning Steps in SQL

#### Step 1: Load Data
The CSV file was imported into the database using SQL’s LOAD DATA function.

#### Step 2: Handling Missing Values
- **Ratings**: Replaced missing ratings with the average rating of the respective brand.

- **Discount Percentages**: Recalculated missing discounts using the formula:            

*UPDATE phone_sales
SET Discount_Percentage = ((Original_Price - Selling_Price) / Original_Price) * 100
WHERE Discount_Percentage IS NULL;*

#### Step 3: Standardizing Brand and Model Names
Standardized the brand and model names by converting them to uppercase and trimming whitespace.     

*UPDATE phone_sales
SET Brand = UPPER(Brand),
    Model = TRIM(Model);*

#### Step 4: Removing Duplicates
Used GROUP BY and HAVING clauses to identify and remove duplicate records.        

*DELETE FROM phone_sales
WHERE id NOT IN (
    SELECT MIN(id)
    FROM phone_sales
    GROUP BY Brand, Model, Selling_Price, Original_Price
);*
    
#### Step 5: Handling Outliers
Identified and removed outliers based on:
- Discount percentages > 100% or < 0%
- Ratings > 5 or < 0
- Negative prices

*DELETE FROM phone_sales
WHERE Discount_Percentage > 100 OR Discount_Percentage < 0
   OR Rating > 5 OR Rating < 0
   OR Selling_Price < 0 OR Original_Price < 0;*
   
---

### 4. Export for Visualization
The cleaned dataset was exported to a new CSV file for use in Tableau

---

### 5. Summary of Cleaning Outcomes
**Missing Values Addressed:** Filled null ratings and recalculated missing discount percentages.

**Inconsistent Data Fixed:** Standardized brand/model names and removed duplicates.

**Outluiers Removed:** Unrealistic values in pricee, discount percentages, and ratings were deleted.

**Enhanced Dataset:** Added calculated fields like Profit_Margin and Discount Amount for deeper insights.

### Data Visualization
The cleaned dataset was visualized in Tableau to create the **Phone Brand Sales Dashboard**, highlighting:

1. Total sales by brand
2. Models with the highest discount percentages
3. Customer ratings across price ranges
4. Flagship model performance compared to discounted models


-----

# Phone Brand Sales Analysis

## Objective

The objective of this project is to analyze phone sales data, extract key insights, and provide actionable recommendations for optimizing sales, discounts, and customer satisfaction.

---

## Dashboard Overview
![Phone Brand Dashboard](https://github.com/AyomideOkoya/Phone-Brand-Sales-Analysis-Data-Cleaning/blob/8d53d10d72fdd8debc4aa95883a0566e71c09d3c/Phone%20Analysis%20Dashboard.png)

### Key Metrics Highlighted:
- **Total Discount Given**: $3,962,443
- **Average Selling Price**: $35,077
- **Average Ratings**: 4.33
- **Number of Products with Camera**: 1,693

### Top Insights From the Dashboard:
1. **Apple** leads in sales revenue ($31,728,412), followed by **Samsung** ($17,469,003).
2. Older phone models (e.g., iPhone XS, iPhone 11 Pro) receive the highest discounts, exceeding 200%.
3. Customer ratings remain high across all price ranges, indicating consistent quality perception.
4. Flagship models like the iPhone 13 Pro Max retain their full price, maximizing revenue.

---

## Analysis and Insights

### 1. Models with Highest Discounts
- Older models dominate the highest discount list, with **iPhone XS** at the top (279.1%).
- Discounts likely aim to clear inventory, aligning with expected market behavior for older products.

**Recommendation**: Monitor discount levels to avoid negatively impacting newer model sales.

---

### 2. Brand Sales Contribution
- **Apple** dominates with over $31.7M in revenue, while **Samsung** follows at $17.4M.
- **Realme** and **OPPO** contribute smaller shares but still present growth potential.

**Recommendation**: Focus on targeted promotions for mid-tier brands like **realme** and **OPPO** to diversify revenue streams.

---

### 3. Customer Ratings Across Price Ranges
- Customer ratings show minimal variance, with high scores (4.05–4.39) across all price ranges.
- This reflects consistent satisfaction across low, mid, and high-end models.

**Recommendation**: Leverage positive reviews as a marketing tool, especially for lower-priced models to increase their appeal.

---

### 4. Flagship vs. Discounted Models
- Flagship models like the **iPhone 13 Pro Max** are sold at full price, maximizing revenue potential.
- Older models (e.g., iPhone XR, iPhone 7 Plus) rely on aggressive discounts to drive sales.

**Recommendation**: Protect flagship models' brand value while optimizing clearance strategies for older inventory.

---

## Key Visualizations

1. **Total Sales Contribution by Brand** (Pie Chart)
2. **Discounts by Model** (Bar Chart)
3. **Customer Ratings by Price Range** (Bar Chart)
4. **Highest Revenue-Generating Models and Discounts** (Bar Chart)

---

## Recommendations

1. **Optimize Discounts**: Use dynamic pricing strategies to balance inventory clearance and profitability.
2. **Enhance Mid-Range Offerings**: Focus on $10,000–$15,000 price ranges with competitive features.
3. **Leverage Customer Ratings**: Highlight high satisfaction scores in promotional campaigns.
4. **Boost Underperforming Brands**: Drive growth for **realme** and **OPPO** with targeted marketing efforts.

---

## Tools Used

- **Data Visualization**: Tableau 
- **Data Processing**: Tableau
