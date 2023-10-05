# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
To create and extract information with SQL code from raw data files concerning a website’s visitor history. The project seeks to produce a cleaned database free of errors and redundancy to answer a set of preassigned questions; in addition to creating/answering user questions formed from said data.

## Process
 # Extract data from Compass
 ## Visually inspect individual .csv files using Excel to identify useful columns and their respective data types
 Create tables and import data in SQL
 Clean, normalize and transform datasets
 Inspect again to ensure the newly cleaned data is viable and correct
 Create queries
 Run queries 
 Repeat various steps as neccessary
 Quality Assurance to ensure data is free of redundancy and inconsistencies
 Draw conclusions


## Results
 A majority of sales originate from the United States
 Within USA, a majority of high revenue generating cities reside within the West Coast (specifically California)
 Lots of missing city data exists within the database (too much to exclude, replace or drop the column entirely)
 Top selling products consist of Men's Apperal (mainly t-shirts) and NEST branded products
 Predominantly Male Clientele 
 Majoirty of visitor traffic comes from organic searches
 Many inconsistencies within the product, sales_by_sku and sales_report databases


## Challenges 
 The presence of cross-sectional data in the product, sales_by_sku and sales_report tables resulted in a varying number of product SKUs (some tables had SKUs which were not in the other ones)
 The time series data provided corresponded to different intervals/periods (all_sessions spans 365 days whereas analytics spans 92 days)
 Redundancy/duplicate rows within tables
 Raw data is inconsistent and poorly formatted

 Future Goals
 Further investigate products to hopefully explain the discrepancy between tables (When was the data gathered? Are there new or discontinued products?)
 Investigate trends such as seasonal purchasing habits (Does the site sell more t-shirt during the summer?)
 Create more connections/generalizations to potentially create some financial models (may be outside the scope of the project)
