What issues will you address by cleaning the data?





Queries:
--creates a new table that resemebles the analytics table (but without duplicating rows)	
create table analytics_clean as
	select distinct * from analytics
 
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
