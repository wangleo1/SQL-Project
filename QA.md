What are your risk areas? Identify and describe them.
Risk factors include:
- Redundancy in the form of repeating rows
- Inconsistencies such as varying/contrasting information amongst datasets
- Incomplete/missing data causing misleading results
  

QA Process:

--creates a new table that resemebles the analytics table (but without duplicating rows)	
create table analytics_clean as
	select distinct * from analytics
--check that the new table has no duplicates	
select distinct count(*) from analytics_clean

--QA 
--analytics data spans 92 days while the all_sessions database spans one year (365 days)
-- check the interval of each time series dataset
select convert_date(max(date)) - convert_date(min(date)) as interval_days from analytics_clean
select convert_date(max(date)) - convert_date(min(date)) as interval_days from all_sessions

 --a majority of entries dont have a city
select city, count(city) from all_sessions
	group by city 
	order by count(city) desc
 
--majority of orders with missing cities are from the USA (Q2)
--12 are from the USA
select country, count(city) from all_sessions
	where city = 'not available in demo dataset' and "productQuantity" is not null
	group by country
	order by country
 
 --checking number of orders for spain 
--used to check why average is so high (only one transaction)
select "productQuantity" from all_sessions
	where country = 'Spain' and "productQuantity" is not null

 --more short ids than long ones
select count(distinct "fullvisitorId") as fullid, count(distinct "visitId") shortid from analytics_clean


The quality assurance process consisted of various steps, the first being the validation of data – consisting of inconsistency checks and the confirmation of unique values. Prior to query formation, a check had been run on each of the five table to check for duplicate rows, any table with redundancy would be copied into a new table without the duplicated values; a new table was generated to avoid tampering with direct/raw data itself. A test would then be conducted to check for distinct rows within the newly created table.
As two of the tables consisted of time-series data, it was crucial to inspect the time intervals for the respective datasets. The analysis table spanned a time interval of 92 days whereas the all_sessions data spanned a total of 365 day. Knowing this information, a majority of the calculations/code developed made strict use of only one database, all_sessions – utilizing different datasets for different questions would have resulted in conflicting information. For the sake of consistency, only the all_sessions table was used as it covered a larger time distance of data.
Many individual queries had been created to double check the results for previous queries such as ones to check how many values any particular column was missing. Additionally, queries had been constructed to analyze any suspicious results; for instance, Spain had a high average order quantity so a query was developed to isolate the individual case for inspection – turn out the country only had one order but with a high product quantity, resulting in a high average. Furthermore, suspicious results had been validated through either manual calculations or the usage of outside softwares such as Excel.
