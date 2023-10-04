Question 1: Can any assumptions be made about visitor demographic?

SQL Queries:
--QUESTION 
--When is the main demographic of the website
--the following is just for views (not orders)
--3555 for men, 763 for women 
select replace("v2ProductCategory", 'Home/',''), count("v2ProductCategory") from all_sessions
	group by "v2ProductCategory"
	having "v2ProductCategory" ilike '%women%'
	order by count("v2ProductCategory") desc
	
select replace("v2ProductCategory", 'Home/','')	, count("v2ProductCategory") from all_sessions
	group by "v2ProductCategory"
	having "v2ProductCategory" ilike '%women%'
	order by count("v2ProductCategory") desc

Answer: 



Question 2: How do visitors typically access the site?

SQL Queries:
--question (how do people typically find/access the site)
select "channelGrouping", count("channelGrouping") from all_sessions
	group by "channelGrouping"
	order by count("channelGrouping") desc
 
Answer:



Question 3: Are there any product inconsistencies across the datasets?  

SQL Queries:
--rows unique to product table
--638 products missing from 
select * from products p
	left join sales_by_sku sbs on sbs."productSKU" = p."SKU"
	left join sales_report sr using("productSKU")
	where sr."productSKU" is null and sbs."productSKU" is null

--products in sales_by_sku but not the others
--8 total skus missing
select "productSKU", total_ordered from sales_by_sku sbs
	left join sales_report sr using("productSKU")
	left join products p on p."SKU" = sbs."productSKU"
	where sr."productSKU" is null and p."SKU" is null

 --no products in the sales_report that aren't in the other two	
select "productSKU", sr.total_ordered from sales_report sr
	left join sales_by_sku sbs using("productSKU")
	left join products p on p."SKU" = sbs."productSKU"
	where sbs."productSKU" is null and p."SKU" is null

Answer:


