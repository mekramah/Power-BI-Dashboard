# Power-BI-Dashboard
Sales Insights for products sold in different region
Our case study is based on a computer hardware business which is facing challenges in dynamically changing market. Sales director decides to invest in data analysis 
project and he would like to build power BI dashboard that can give him real time sales insights.
We started by using AIMs Grid, so that we can get a clear cut idea about the Purpose, Customers/Stakeholders, Result, Success Rate.
Important Queries:
1. Show transactions for Chennai market (market code for chennai is Mark001)
	 SELECT * FROM transactions where market_code='Mark001';

2.Show distrinct product codes that were sold in chennai
	SELECT distinct product_code FROM transactions where market_code='Mark001';

3.Show transactions in 2020 join by date table
	SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;

4.Show total revenue in year 2020,
	SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";

5.Show total revenue in year 2020, January Month,
	SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");

6.Show total revenue in year 2020 in Chennai
	SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.market_code="Mark001";

We used Power BI for data cleanup(ETL Process).
Few queries in Power BI (Power Query):

1. To add column to a table
   = Table.AddColumn(#"Filtered Rows", "Custom", each if [currency] = "USD" then 1 else null)
   
2. To change USD to INR
   = Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount])
