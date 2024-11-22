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
- **Data Type Errors:** Numeric columns like `Selling Price` were stored as text.

---

### 3. Cleaning Steps in SQL

#### Step 1: Load Data
The CSV file was imported into the database using SQL’s `LOAD DATA` function.

#### Step 2: Handling Missing Values
- **Ratings**: Replaced missing ratings with the average rating of the respective brand.

-- **Discount Percentages**: Recalculated missing discounts using the formula:            

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

### 4. Export for Visualization
The cleaned dataset was exported to a new CSV file for use in Tableau:

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
