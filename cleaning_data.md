What issues will you address by cleaning the data?

In regards to the datasets provided; a significant amount of workload must be allocated towards normalizing the data in order to reduce/eliminate redundancy. For instance, the analytics dataset contains a substantial amount of redundancy in the form of duplicate rows. The data cleaning process seeks to generate usable/normalized data without directly altering the databases themselves – for said reason, a cleaned duplicate table for analytics was created which did not contain duplicate rows. The analytics_clean table was then used in place of the original analytics table.
Furthermore, the unit prices needed to be converted into usable data. A user-defined function (UDF) was created which would divide any given price by 1,000,000 in order to convert prices into USD; the unit prices within the data set had to be converted to real, as opposed to integers originally, to get decimal places.
Dates, which had been initially stored as strings due to their inconsistent format, needed to be converted into the date datatype. The UDF convert_date seeks to convert the provided dates, which appear in a YYYYMMDD format, into a useable date format – YYYY/MM/DD.
The final piece of data cleaning within the project involved product names. The product names had been initially been provided in a directory format, making the interpolation of results rather difficult. The convert_name UDF seeks to drop the “YouTube”, “Google” and “Android” prefixes proceeding the product names. Additionally, “Home/” had been dropped from the product categories for similar reasons as the product names; this had been directly altered within the queries as opposed to a UDF for simplicity.



Queries:
--creates a new table that resemebles the analytics table (but without duplicating rows)	
create table analytics_clean as
	select distinct * from analytics

 --check that the new table has no duplicates	
select distinct count(*) from analytics_clean
 
--UDF to clean price/ convert to used
create or replace function convert_price (price real)
returns real
as
$$
	begin 
		return price/1000000 as Price_in_USD;
	end
$$
LANGUAGE PLPGSQL; 

--UDF to convert a date from a string to a date
create or replace function convert_date (date varchar)
returns date
as
$$
	begin 
		return cast(date as date);
	end
$$
LANGUAGE PLPGSQL; 

--UDF to clean the product names
--removes the random names proceeding the product names
CREATE OR REPLACE FUNCTION name_clean("v2ProductName" VARCHAR)
RETURNS VARCHAR
AS $$
DECLARE
    name VARCHAR;
BEGIN
    CASE 
        WHEN "v2ProductName" LIKE 'Google%' THEN
            name := REPLACE("v2ProductName", 'Google ', '');
        WHEN "v2ProductName" LIKE 'YouTube%' THEN
            name := REPLACE("v2ProductName", 'YouTube ', '');
        WHEN "v2ProductName" LIKE 'Android%' THEN
            name := REPLACE("v2ProductName", 'Android ', '');
        ELSE
            name := "v2ProductName";
    END CASE;
    RETURN name;
END;
$$ LANGUAGE PLPGSQL;

--drops the 'prefix' of the category names
replace("v2ProductCategory", 'Home/','') as Category


Note: All transformational processes had been stored in the form of UDFs so they could be later applied to any of the datasets.
Only data used within the analysis/calculations had been cleaned. Data which had not been used had not been cleaned.


