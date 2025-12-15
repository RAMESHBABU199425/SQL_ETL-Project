# SQL_EDA-Project
This project performs Exploratory Data Analysis (EDA) using SQL on a
sample `sales_data` table containing 20 rows and 6 columns--

CREATE TABLE sales_data (
    Sale_ID INT,
    Customer_Name VARCHAR(50),
    Product VARCHAR(50),
    Category VARCHAR(50),
    Quantity INT,
    Amount DECIMAL(10,2)
);

INSERT INTO sales_data VALUES
(1,'Rakesh','Laptop','Electronics',1,56000),
(2,'Priya','Headphones','Electronics',2,3200),
(3,'Arjun','T-Shirt','Clothing',3,1500),
(4,'Sneha','Shoes','Footwear',1,2800),
(5,'Varun','Mobile','Electronics',1,18000),
(6,'Kavya','Jeans','Clothing',2,2400),
(7,'Rohit','Blender','Home Appliances',1,3500),
(8,'Neha','Watch','Accessories',1,2200),
(9,'Manish','Sandals','Footwear',2,1700),
(10,'Divya','Mixer','Home Appliances',1,4100),
(11,'Kiran','Laptop Bag','Accessories',1,900),
(12,'Pooja','Saree','Clothing',1,3200),
(13,'Aditya','Mouse','Electronics',3,1500),
(14,'Tanvi','Jacket','Clothing',1,2600),
(15,'Sandeep','Earbuds','Electronics',1,1900),
(16,'Hari','Slippers','Footwear',2,800),
(17,'Asha','Oven','Home Appliances',1,8200),
(18,'Nikhil','Shirt','Clothing',2,2100),
(19,'Swathi','Charger','Electronics',1,700),
(20,'Vivek','Belt','Accessories',1,600);

Basic EDA Tasks
--Count total rows
Select Count(*)from Sales_data
--List category-wise sales
Select Category,Count(Sale_id)sales
From Sales_data
Group by Category
--Most sold product (by Quantity)
Select Top 1 Product,sum(Quantity) Most_sold 
from Sales_data
Group by Product
Order BY Most_sold Desc
--Highest revenue product
Select Top 1 Product,Amount As Total_revenue 
from Sales_data
Order by Total_revenue Desc
Moderate level
--Find total amount credited for each customer.
Select Customer_name,Sum(amount) Credited_amount from cleaned_finance_ETL
Where Trans_type='Credit'
Group by Customer_name
--Find total amount debited from each branch.
Select Branch_code,Sum(Amount) Debited_Amount from cleaned_finance_ETL
Where trans_type='Debit'
Group by Branch_code
--Count how many transactions each customer has made.
Select Customer_name,Count(trans_id) Count_of_Trans from  cleaned_finance_ETL
Group by Customer_name
--Find average transaction amount for CREDIT transactions.
Select Trans_type,Avg(Amount) avg_credit_amt from cleaned_finance_ETL
Where trans_type='Credit'
Group by Trans_type
--Show the highest transaction amount for each Trans_Type.
Select Trans_type,Max(amount) Maximum_trns_amt from cleaned_finance_ETL
Group by Trans_type
--Show customer with the maximum CREDIT amount.
Select Top 1 Customer_name,Max(Amount) Maximum_amunt from cleaned_finance_ETL
where trans_type='Credit'
Group by Customer_name
order by Maximum_amunt Desc
--Show customer with the minimum DEBIT amount.
Select Top 1 Customer_name,Min(Amount) Minimum_amount from cleaned_finance_ETL
where trans_type='Debit'
Group by Customer_name
order by Minimum_amount 
--Find branch with the highest number of transactions.
Select top 1 branch_code,count(trans_id) counted_trans from cleaned_finance_ETL
Group by branch_code
order by counted_trans desc
--Show total CREDIT & DEBIT for each Trans_Date.
select trans_date, sum(amount) total_cr_dr from cleaned_finance_ETL
Group by trans_date
Select Distinct Category
from Sales_data
--Group by branch and show total CREDIT amount per branch.
select Branch_code,sum(amount) Total_amt_cr_branch from cleaned_Finance_ETL
Where trans_type='Credit'
Group by Branch_code
--Find the number of ATM WITHDRAWAL transactions.
Select Count(*) No_of_ATM_WITh from Cleaned_Finance_ETL
Where Remarks='ATM WIthdrawl' or Remarks like 'ATM %'
--Display all transactions where remarks contain "PAYMENT".
Select *from Cleaned_Finance_ETL
Where Remarks like '%Payment%'
/*Show amount range:
Less than 5,000
Between 5,000 and 20,000
Above 20,000*/
select Amount,
case 
when amount<=5000 then 'low'
when amount<20000 then 'medium'
when amount>20000 then 'high'
end as Range
from Cleaned_Finance_ETL
--Find customers who have both CREDIT and DEBIT transactions.
Select Customer_name,Trans_type from Cleaned_Finance_ETL
where trans_type In('Credit','debit')
