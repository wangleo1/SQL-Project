Question 1: Can any assumptions be made about visitor demographic?

SQL Queries:
--QUESTION 
--When is the main demographic of the website
--the following is just for views (not orders)
--3086 for men, 763 for women 
select replace("v2ProductCategory", 'Home/',''), count("v2ProductCategory") from all_sessions
	group by "v2ProductCategory"
	having "v2ProductCategory" ilike '%/men%' or "v2ProductCategory" ilike '%man%'
	order by count("v2ProductCategory") desc
	
select replace("v2ProductCategory", 'Home/','')	, count("v2ProductCategory") from all_sessions
	group by "v2ProductCategory"
	having "v2ProductCategory" ilike '%women%' or "v2ProductCategory" ilike '%woman%'
	order by count("v2ProductCategory") desc

Answer: 
When cleaning the different category names, questions concerning demographic began to arose – what types of people are visiting the site? Granted the limit information within the datasets, few correlations may be gathered; variables such as age, ethnicity and income are completely nonexistent. However, connections/assumptions for gender may be construct using the website’s traffic data. For instance, the number of views a page containing gender specific products may be used as a proxy for viewer gender. By analyzing the total number of views pages including the keywords “Men” or “Woman” collected, assumptions may be made about overall viewer gender traffic. The firm may wish to focus their marketing towards males as it appears to be where a majority of their attention/revenue comes from.
Overall, product pages containing the keyword “men” gathered nearly four times as much traffic as pages containing the keyword “women” – 3086 views and 763 respectively. Utilizing these results, one may assume the website is predominately viewed by male consumers.
This form of analysis does come with potential drawbacks. For instance, false positives may arise when a consumer browses for potential gifts for their significant other of the opposite sex. Furthermore, the results may only conclude on correlation, not causation. The results do not directly explain why there appears to be predominantly male viewer traffic. Is the site specifically geared towards men and this is the end result? No finite conclusions may be drawn due to lack of data.   



Question 2: How do visitors typically access the site?

SQL Queries:
--question (how do people typically find/access the site)
select "channelGrouping", count("channelGrouping") from all_sessions
	group by "channelGrouping"
	order by count("channelGrouping") desc
 
Answer:
When inspecting the various columns within the datasets, columns such as bounce and page directory became variables of interest. Curiosity concerning the topic began to arose in the form of one question – how do viewers typically find/access the site? 
Analysis showed a majority of viewers accessed the website through an organic search, utilizing search engines such as Google or Bing – 8653 total. However, a substantial number of visitors accessed the sight directly by typing out the website’s URL, as well as referral links from other websites – 2997 and 2580 respectively. These results may be useful for the company’s marketing department in their marketing efforts. For instance, the company may decide against working with paid searches as to save the company some money, especially since a majority of their traffic results from organic searches.  




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


