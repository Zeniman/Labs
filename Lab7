---------------------------------------------------------------------
-- LAB 07
--
-- Exercise 1
---------------------------------------------------------------------
---------------------------------------------------------------------
-- Task 1
-- 
-- 
-- Open the project file F:\10774A_Labs\10774A_07_PRJ\10774A_07_PRJ.ssmssln and the T-SQL script 51 - Lab Exercise 1.sql. To set your database context to that of the TSQL2012 database, highlight the statement USE TSQL2012; and execute the highlighted code. After executing this statement, the TSQL2012 database should be selected in the Available Databases box. In subsequent exercises, you will simply be instructed to ensure that you are connected to the TSQL2012 database.
--
-- Write a SELECT statement to return columns that contain:
--  The current date and time. Use the alias currentdatetime.
--  Just the current date. Use the alias currentdate.
--  Just the current time. Use the alias currenttime.
--  Just the current year. Use the alias currentyear.
--  Just the current month number. Use the alias currentmonth.
--  Just the current day of month number. Use the alias currentday.
--  Just the current week number in the year. Use the alias currentweeknumber.
--  The name of the current month based on the currentdatetime column. Use the alias currentmonthname.
-- 
-- Execute the written statement and compare the results that you got with the desired results shown in the file 52 - Lab Exercise 1 - Task 1 Result.txt. Your results will be different because of the current date and time value.
--
-- Can you use the alias currentdatetime as the source in the second column calculation (currentdate)? Please explain.
---------------------------------------------------------------------
select
getdate() as currentdatetime
,convert(date,getdate()) as currentdate
,convert(time,getdate()) as currenttime
,YEAR(getdate()) as currentyear
,MONTH(getdate()) as currentmonth
,DAY(getdate()) as currentday
,DATEPART(week,getdate()) as currentweeknumber
,DATEPART(month,getdate()) as currentmonthname
,DATEPART(WEEKDAY,getdate()-1) as currentweekday;


---------------------------------------------------------------------
-- Task 2
--  
-- Write December 11, 2011, as a column with a data type of date. Use the different possibilities inside the T-SQL language (cast, convert, specific function, etc.) and use the alias somedate.
---------------------------------------------------------------------
--SELECT DATEFROMPARTS(2015, 12, 11) AS somedate;

--SELECT CAST('20151211' AS date) AS somedate;

SELECT CONVERT(date, '12/11/2015', 101) AS somedate;

---------------------------------------------------------------------
-- Task 3
-- 
-- Write a SELECT statement to return columns that contain:
--  Three months from the current date and time. Use the alias threemonths.
--  Number of days between the current date and the first column (threemonths). Use the alias diffdays.
--  Number of weeks between April 4, 1992, and September 16, 2011. Use the alias diffweeks.
--  First day in the current month based on the current date and time. Use the alias firstday.
--
select DATEADD(MONTH,3,GETDATE()) as threemonths,
 DATEDIFF(DAY,GETDATE(),DATEADD(MONTH,3,GETDATE())) as diffdays,
 DATEDIFF(WEEK,'19920404','20110916') as diffweeks,
 DATEADD(MONTH,DATEDIFF(MONTH,'',GETDATE()),'') as firstday;

---------------------------------------------------------------------
-- Task 4
-- 
-- The IT department has written a T-SQL statement that creates and populates a table named Sales.Somedates. 
--
-- Execute the provided T-SQL statement.
-- 
-- Write a SELECT statement against the Sales.Somedates table and retrieve the isitdate column. Add a new column named converteddate with a new date data type value based on the column isitdate. If the column isitdate cannot be converted to a date data type for a specific row, then return a NULL. 
--
-- Execute the written statement and compare the results that you got with the desired results shown in the file 54 - Lab Exercise 1 - Task 4 Result.txt. 
-- 
-- What is the difference between the SYSDATETIME and CURRENT_TIMESTAMP functions?
--
-- What is a language-neutral format for the DATE type?
---------------------------------------------------------------------

SET NOCOUNT ON;

IF OBJECT_ID('Sales.Somedates') IS NOT NULL 
	DROP TABLE Sales.Somedates;

CREATE TABLE Sales.Somedates (
	isitdate varchar(9)
);

INSERT INTO Sales.Somedates (isitdate) VALUES 
	('20110101'),
	('20110102'),
	('20110103X'),
	('20110104'),
	('20110105'),
	('20110106'),
	('20110107Y'),
	('20110108');

SET NOCOUNT OFF;

SELECT 
 isitdate,
 CASE WHEN ISDATE(isitdate) = 1 THEN CONVERT(DATE, isitdate) ELSE NULL END AS converteddate
FROM Sales.Somedates;
---------------------------------------------------------------------
-- Task 5
-- 
-- copy-paste text about lab from doc file
---------------------------------------------------------------------
-- drop the table 

DROP TABLE Sales.Somedates;
-- LAB 07
--
-- Exercise 2
---------------------------------------------------------------------
---------------------------------------------------------------------
-- Task 1
-- 
-- Open the project file F:\10774A_Labs\10774A_07_PRJ\10774A_07_PRJ.ssmssln and the T-SQL script 61 - Lab Exercise 2.sql. Ensure that you are connected to the TSQL2012 database.
--
-- Write a SELECT statement to retrieve distinct values for the custid column from the Sales.Orders table. Filter the results to include only orders placed in February 2008.
--
-- Execute the written statement and compare the results that you got with the desired results shown in the file 62 - Lab Exercise 2 - Task 1 Result.txt.
---------------------------------------------------------------------
SELECT DISTINCT
 custid
FROM Sales.Orders
WHERE
 orderdate >= '20080201'
 AND orderdate < '20080301';
---------------------------------------------------------------------
-- Task 2
-- 
-- Write a SELECT statement with these columns:
--  Current date and time
--  First date of the current month
--  Last date of the current month
--
-- Execute the written statement and compare the results that you got with the recommended result shown in the file 63 - Lab Exercise 2 - Task 2 Result.txt.
---------------------------------------------------------------------
select GETDATE() as Currentdate
,DATEADD(MONTH,DATEDIFF(MONTH,'',GETDATE()),'') as Firstday_CurrentMonth
,DATEADD(DAY,-1,DATEADD(MONTH,DATEDIFF(MONTH,'',GETDATE())+1,'')) as Lastday_CurrentMonth
---------------------------------------------------------------------
-- Task 3
-- 
-- Write a SELECT statement against the Sales.Orders table and retrieve the orderid, custid, and orderdate columns. Filter the results to include only orders placed in the last five days of the order month.
--
-- Execute the written statement and compare the results that you got with the recommended result shown in the file 64 - Lab Exercise 2 - Task 3 Result.txt.
---------------------------------------------------------------------
select orderid, custid, orderdate
from Sales.Orders
where orderdate between DATEADD(DAY,-4,EOMONTH(orderdate)) and EOMONTH(orderdate)
order by orderdate ASC;
---------------------------------------------------------------------
-- Task 4
-- 
-- Write a SELECT statement against the Sales.Orders and Sales.OrderDetails tables and retrieve all the distinct values for the productid column. Filter the results to include only orders placed in the first 10 weeks of the year 2007.
--
-- Execute the written statement and compare the results that you got with the recommended result shown in the file 65 - Lab Exercise 2 - Task 4 Result.txt.
---------------------------------------------------------------------
select distinct(od.productid)
from Sales.Orders o
inner join Sales.OrderDetails od
on o.orderid = od.orderid
where o.orderdate between '2007-01-02' and DATEADD(WEEK,10,'2007-01-02') order by productid;
-- LAB 07
--
-- Exercise 3
---------------------------------------------------------------------

---------------------------------------------------------------------
-- Task 1
-- 
-- Open the project file F:\10774A_Labs\10774A_07_PRJ\10774A_07_PRJ.ssmssln and the T-SQL script 71 - Lab Exercise 3.sql. Ensure that you are connected to the TSQL2012 database.
--
-- Write a SELECT statement against the Sales.Customers table and retrieve the contactname and city columns. Concatenate both columns so that the new column looks like this:
--   Allen, Michael (city: Berlin)
--
-- Execute the written statement and compare the results that you got with the recommended result shown in the file 72 - Lab Exercise 3 - Task 1 Result.txt. 
---------------------------------------------------------------------
select contactname + space(2) + '(city: ' + city + ')'
from Sales.Customers

---------------------------------------------------------------------
-- Task 2
-- 
-- Copy the T-SQL statement in task 1 and modify it to extend the calculated column with new information from the region column. Treat a NULL in the region column as an empty string for concatenation purposes. When the region is NULL, the modified column should look like this:
--  Allen, Michael (city: Berlin, region: )
--
-- When the region is not NULL, the modified column should look like this
--  Richardson, Shawn (city: Sao Paulo, region: SP)
--
-- Execute the written statement and compare the results that you got with the recommended result shown in the file 73 - Lab Exercise 3 - Task 2 Result.txt.
---------------------------------------------------------------------
select contactname + space(2) + '(city: ' + city + ', region: ' + ISNULL(region,' ') + ')'
from Sales.Customers


---------------------------------------------------------------------
-- Task 3
-- 
-- Write a SELECT statement to retrieve the contactname and contacttitle columns from the Sales.Customers table. Return only rows where the first character in the contact name is ‘A’ through ‘G’.
--
-- Execute the written statement and compare the results that you got with the recommended result shown in the file 74 - Lab Exercise 3 - Task 3 Result.txt. Notice the number of rows returned.
---------------------------------------------------------------------
select contactname,contacttitle
from Sales.Customers
where SUBSTRING(contactname,1,1) in ('A','B','C','D','E','F','G')
order by contactname asc

-- LAB 07
--
-- Exercise 4
---------------------------------------------------------------------

---------------------------------------------------------------------
-- Task 1
-- 
-- Open the project file F:\10774A_Labs\10774A_07_PRJ\10774A_07_PRJ.ssmssln and the T-SQL script 81 - Lab Exercise 4.sql. Ensure that you are connected to the TSQL2012 database.
--
-- Write a SELECT statement to retrieve the contactname column from the Sales.Customers table. Based on this column, add a calculated column named lastname, which should consist of all the characters before the comma.
--
-- Execute the written statement and compare the results that you got with the recommended result shown in the file 82 - Lab Exercise 4 - Task 1 Result.txt. 
---------------------------------------------------------------------

select contactname , SUBSTRING(contactname,0,CHARINDEX(',',contactname)) as lastname
from Sales.Customers


---------------------------------------------------------------------
-- Task 2
-- 
-- Write a SELECT statement to retrieve the contactname column from the Sales.Customers table and replace the comma in the contact name with an empty string. Based on this column, add a calculated column named firstname, which should consist of all the characters after the comma.
--
-- Execute the written statement and compare the results that you got with the recommended result shown in the file 83 - Lab Exercise 4 - Task 2 Result.txt. 
---------------------------------------------------------------------
select REPLACE(contactname,',','') as contactname, SUBSTRING(contactname,CHARINDEX(',',contactname)+2,LEN(contactname)) as firstname
from Sales.Customers

---------------------------------------------------------------------
-- Task 3
-- 
-- Write a SELECT statement to retrieve the custid column from the Sales.Customers table. Add a new calculated column to create a string representation of the custid as a fixed-width (6 characters) customer code prefixed with the letter C and leading zeros. For example, the custid value 1 should look like C00001.
--
-- Execute the written statement and compare the results that you got with the recommended result shown in the file 84 - Lab Exercise 4 - Task 3 Result.txt. 
---------------------------------------------------------------------
SELECT
 custid,
 FORMAT(custid, N'\C00000') AS custnewid
FROM Sales.Customers;


---------------------------------------------------------------------
-- Task 4
--
-- Write a SELECT statement to retrieve the contactname column from the Sales.Customers table. Add a calculated column, which should count the number of occurrences of the character ‘a’ inside the contact name. (Hint: Use the string functions REPLACE and LEN.) Order the result from rows with the highest occurrences to lowest.
--
-- Execute the written statement and compare the results that you got with the recommended result shown in the file 85 - Lab Exercise 4 - Task 4 Result.txt. 
---------------------------------------------------------------------
select contactname,LEN(contactname) - LEN(REPLACE(contactname,'a','')) as a_occurrences
from Sales.Customers
order by a_occurrences desc
