# Phone-Brand-Sales-Analysis-Data-Cleaning
The goal of this project was to analyze phone sales data, clean and prepare it for analysis using SQL, and create actionable visualizations in Tableau to identify trends, optimize discounts, and improve customer satisfaction.

# Phone Brand Sales Analysis - Data Cleaning and Visualization

---

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

