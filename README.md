# CIT28

--Alexander Phosykeo
--CIT 28
--Assignment #5 - Chapter 8
--Using SQLQFMM2

--Sales Orders Database: #1, #3, #5

--#1
select Orders.CustomerID,Customers.CustLastName, CustFirstName,OrderDate
from Orders
inner join Customers
on Orders.CustomerID=Customers.CustomerID
order by OrderDate asc


--#3
select Orders.OrderNumber, Products.ProductName, Products.RetailPrice
from Orders
inner join Order_Details
on Orders.OrderNumber=Order_Details.OrderNumber
inner join Products
on Order_Details.ProductNumber = Products.ProductNumber
order by Orders.OrderNumber asc

--#5
select Customers.CustLastName, Customers.CustFirstName, Employees.EmpLastName, Employees.EmpFirstName
from Customers
inner join Employees
on Customers.CustLastName = Employees.EmpLastName

--Entertainment Agency Database: #1 and #3

--#1
select Agents.AgentID, Agents.AgtLastName, Agents.AgtFirstName, Engagements.StartDate, Engagements.EndDate
from Agents
inner join Engagements
on Agents.AgentID = Engagements.AgentID
order by Engagements.StartDate asc

--#3
select *
from Agents
inner join Entertainers
on agents.AgtZipCode = Entertainers.EntZipCode


--School Scheduling Database: #1 and #3

--#1
select Buildings.BuildingName, Class_Rooms.ClassRoomID
from Buildings
inner join Class_Rooms
on Buildings.BuildingCode = Class_Rooms.BuildingCode














-----------------------------
--Sales Orders Database: #1, #3
--#1
select CustLastName, CustFirstName
from Customers
left outer join
(select distinct orders.CustomerID, Orders.OrderDate, Products.ProductName, Products.ProductNumber
from Orders
inner join Order_Details
on Orders.OrderNumber = Order_Details.OrderNumber
inner join Products
on  Order_Details.ProductNumber = Products.ProductNumber
where ProductName like '%helmet%') 
as R
on Customers.CustomerID = R.CustomerID
where R.ProductName is null
