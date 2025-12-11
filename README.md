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
--Distinct categories
Select Distinct Category
from Sales_data
