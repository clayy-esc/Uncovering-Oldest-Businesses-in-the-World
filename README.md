<center><img src="image/oldest_businesses_map.png"></center>

# 🌍 Uncovering Oldest Businesses in the World

Some businesses manage to survive for centuries despite wars, political shifts, economic crises, and technological change. This project explores the **oldest continuously operating businesses in the world** using a cleaned dataset compiled by ***BusinessFinancing.co.uk***.

The analysis focuses on **combining multiple datasets using different types of join** to better understand the world's oldest businesses.

---

## 📂 Dataset Overview

`businesses.csv` and `new_businesses.csv`

|Column|Description|
|------|-----------|
|`business`|Name of the business (varchar)|
|`year_founded`|Year the business was founded (int)|
|`category_code`|Code for the business category (varchar)|
|`country_code`|ISO 3166-1 three-letter country code (char)|

`countries.csv`

|Column|Description|
|------|-----------|
|`country_code`|ISO 3166-1 three-letter country code (varchar)|
|`country`|Name of the country (varchar)|
|`continent`|Name of the continent the country exists in (varchar)|

`categories.csv`

|Column|Description|
|------|-----------|
|`category_code`|Code for the business category (varchar)|
|`category`|Description of the business category (varchar)|

---

## 🛠️ Tools Used

- Python  
- Pandas  
- CSV-based relational datasets  

---

## 🔍 Analysis Process

### Data Integration
- **INNER JOIN** `businesses` with `countries` on `country_code` to keep only businesses with valid country data.  
- Combine `businesses` and `new_businesses` using **concatenation** to create a unified dataset.  
- **LEFT JOIN** with `categories` on `category_code` to add category info without losing records.

### Data Validation
- Enforce join integrity using `validate` (`one_to_one`, `many_to_one`).  
- Check for missing values after each merge.  
- **OUTER JOIN** with `countries` to identify missing business data by country.

### Data Analysis
- Sort businesses by `year_founded` to find earliest active businesses.  
- Group by continent and category to find minimum founding years.  
- **RIGHT JOIN** to merge continent-level minimum founding years back into the full dataset.  
- Count missing businesses per continent to highlight data gaps.

---

## 📊 Key Questions & Findings

**1. What is the oldest business on each continent?**

The oldest active business per continent was identified by:
- Performing an **INNER JOIN** between the `businesses` and `countries` datasets on `country_code`
- Sorting businesses by `year_founded`
- Grouping by `continent` and selecting the **minimum founding year**
- Using a **RIGHT JOIN** to merge these minimum founding years back into the full dataset, retrieving complete business records

This produced a dataset listing the **oldest continuously active business in each continent**, including the associated country, business name, and founding year.

**2. How many countries per continent lack data on the oldest businesses?**

To identify countries without recorded oldest active businesses:
- The `businesses` and `new_businesses` datasets were combined using **concatenation**
- An **OUTER JOIN** with the `countries` dataset exposed missing business entries
- Countries with null business values were counted per continent

This highlights **data coverage gaps** across continents where no oldest active business information is available.

**3. What is the oldest business category, and on which continent?**

The oldest business category per continent was determined by:
- Applying an **INNER JOIN** between `businesses` and `countries`
- Enriching business records using a **LEFT JOIN** with the `categories` dataset
- Grouping by `continent` and `category`
- Selecting the **earliest founding year** per category
- Identifying the oldest category within each continent

The results show that **essential service categories** most frequently appear among the oldest active businesses across continents.

---

## 🧠 Conclusion

This project identifies the **oldest active businesses** across continents and categories using different join strategies:

- **INNER JOIN** ensures valid business-country matches  
- **LEFT JOIN** enriches businesses with category data  
- **RIGHT JOIN** reconstructs complete records after aggregation  
- **OUTER JOIN** exposes missing or incomplete data  

By applying the appropriate join type at each stage, the analysis provides a clear view of **which businesses have survived the longest in history**, and where data is missing across the globe.
