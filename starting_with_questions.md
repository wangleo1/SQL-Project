Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries: 
---------question1----------------
--USA has the most by far
--sunnyvale and SF (california) have the most as that we know of (most are not available but we know they are in the USA)
--3rd table has insite of breakdown
select country, convert_price(sum("totalTransactionRevenue")) as TR from all_sessions
	group by country
	having sum("totalTransactionRevenue") is not null
	order by tr desc
	
	
select city, convert_price(sum("totalTransactionRevenue")) as TR from all_sessions
	group by city
	having sum("totalTransactionRevenue") is not null
	order by tr desc

--a detailed breakdown of country and city together in the same table
select country,city, convert_price(sum("totalTransactionRevenue")) as TR from all_sessions
	group by country, city
	having sum("totalTransactionRevenue") is not null
	order by tr desc



Answer: An overwhelming majority of total transactional revenue comes from the United States – accounting for approximately 92%.  The remaining 8% of transactional revenue results from business conducted in Israel, Australia, Canada and Switzerland. 

In regards to most profitable cities, the data is slightly ambiguous as the dataset is missing a considerable amount of region data. Nearly half of the transactional revenue generated from the USA is missing an associated city. In terms of the information available, a majority of sales originate from the West Coast – specifically California. Ambiguous data aside, the top revenue generating cities inside the USA include San Francisco, Sunnyvale, Atlanta, Palo Alto, New York and Mountain View – four of which reside in California.





**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
---------question2----------------
--USA has a smaller average because there were more orders, each with varing levels of quantity
--weighted avg makes sense
--whereas Spain only had one large order, resulting in a higher average
select country, avg("productQuantity"), count("productQuantity") from all_sessions
	group by country
	having sum("productQuantity") is not null
	order by avg("productQuantity") desc

--20 total N/As
--12 are from the USA
select city, avg("productQuantity"), count("productQuantity") from all_sessions
	group by city
	having sum("productQuantity") is not null
	order by avg("productQuantity") desc

 --the counts for USA do equal out to 42(same number as the first table) when looking for only USA
select country, city, avg("productQuantity"),count("productQuantity") from all_sessions
	group by country, city
	having sum("productQuantity") is not null
	order by avg("productQuantity") desc




Answer:
The countries with the highest average number of products ordered include both Spain and USA, holding average quantities of 10 and 4.0238 respectively. Additionally, it is important to inspect how these averages are calculated – there exists only one transaction originating from Spain whereas the average for USA is comprised of 42 different orders. Other notable countries include Colombia, France, Canada, Argentina, India, Ireland, Mexico and Finland which all possess average quantities per order of one. 
Corresponding with the previously mentioned countries, Madrid and Salem have the highest average number of products ordered with 10 and 8 respectively. Similar to the previous question, ambiguity exists within this response as 20 of the orders did not have an associated city listed – 12 of which reside within the USA (as seen in the third table).  Further expansion on the topic resides within the QA.md file.






**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
---------question3----------------
--10 different countries just like the previous question
--replace to clean the category name a bit
select country, replace("v2ProductCategory", 'Home/','') as Category, count("v2ProductCategory") from all_sessions
	group by country, "v2ProductCategory"
	--only want results where there have been orders placed (in order to see trends)
	having sum("productQuantity") is not null
	order by count("v2ProductCategory") desc
 
--lots of nest purchases in california (SF, Mountain View, San Jose, LA, Palo Alto)
-- Google Headquarters, Silicone Vally
select city, replace("v2ProductCategory", 'Home/','') as Category , count("v2ProductCategory") from all_sessions
	group by city, "v2ProductCategory"
	having sum("productQuantity") is not null
	order by count("v2ProductCategory") desc

Answer:
The site appears to generate much of its revenue from apparel sale within North America– mainly men’s apparel. There may be a potential correlation between viewer gender and purchasing habits. There also significant sales within the YouTube brand and uncategorized product categories. Sales originating from outside North America do not appear to exhibit any obvious patterns.
Granted the data ambiguity of the city column, an interesting pattern may be seen across the West Coast. Many cities residing within California have shown an affiliation for Nest products – an interactive line of smart home products designed by Google. This trend could potentially share insight on the demographics within California. For instance, Nest sales may experience a spike in sale within these regions due to the types of demographics they attract – California being the home of both the Google headquarters and Silicon Valley may attract more technology progressive people. 





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
--results align with results of previous quesiton (lots of mens appearal)
select country, 
	name_clean("v2ProductName") as Productname,
	count("v2ProductName")
from all_sessions
group by country, "v2ProductName"
having sum("productQuantity") is not null
order by country, count("v2ProductName") desc

-- similar to question 3, Nest products seem very popular across the west coast of USA
select city, 
	name_clean("v2ProductName") as ProductName,
	count("v2ProductName") 
from all_sessions	
group by city, "v2ProductName"
having sum("productQuantity") is not null
order by city, count("v2ProductName") desc

Answer:
The following is a breakdown of the top-selling products by country: 

Argentina	"Alpine Style Backpack"
Canada		"Twill Cap"
Colombia	"Men's Short Sleeve Hero Tee Black"
Finland		"Laptop and Cell Phone Stickers"
France		"Wool Heather Cap Heather/Black"
India		"Men's Vintage Badge Tee Black"
Ireland		"Laptop Backpack"
Mexico		"Men's Vintage Tee"
Spain		"Waze Dress Socks"
United States	"Men's 100% Cotton Short Sleeve Hero Tee White"


The results from the queries align with results from Question 4 – there appears to be high global sales volume in specifically men’s apparel with four out of ten countries having some form of apparel as their top-selling product. 
In regards to cities, men’s t-shirts have found significant popularity amongst buyers. 

In addition, expanding further on the results from Question 4, Nest products are regarded as the top-selling product within the various cities of California. These cities include San Francisco, Sunnyvale, Palo Alto and Mountain View, with their top- selling products consisting of Nest brand outdoor/indoor security cameras, thermostats and smoke detectors respectively. 





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







