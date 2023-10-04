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

In regards to most profitable cities, the data is slightly ambiguous as the dataset is missing a considerable amount of region data. Nearly half of the transactional revenue generated from the USA is missing an associated city. In terms of the information available, a majority of sales originate from the West Coast – specifically California. Ambiguous data aside, the top revenue generating cities inside the USA include San Francisco, Sunnyvale, Atlanta, Palo Alto,  New York and Mountain View – four of which reside in California.





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





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







