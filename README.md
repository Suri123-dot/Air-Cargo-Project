# Air-Cargo-Analysis-problem-statement
Air Cargo is an aviation company that provides air transportation services for passengers and freight. Air Cargo uses its aircraft to provide different services with the help of partnerships or alliances with other airlines. The company wants to prepare reports on regular passengers, busiest routes, ticket sales details, and other scenarios to improve the ease of travel and booking for customers.

## Project Objective
As a DBA expert, need to focus on identifying the regular customers to provide offers, analyze the busiest route which helps to increase the number of aircraft required and prepare an analysis to determine the ticket sales details. This will ensure that the company improves its operability and becomes more customer-centric and a favorable choice for air travel.

## My Tasks
1. Write a SQL query to display all the passengers (customers) who have travelled in routes 1 to 25.

2. Write a SQL query to identify the number of passengers and total revenue in bussiness class from the ticket_details table. 

3. Write a SQL query to display the full name of the customer by extracting the first name and last name from the customer table. 

4. Write a SQL query to extract the customers who have registered and booked a ticket. Use data from the customer and ticket_details tables. 

5. Write a SQL query to identify the customer’s first name and last name based on their customer ID and brand (Emirates) from the ticket_details table. 

6. Write a SQL query to identify the customers who have travelled by Economy Plus class using Group By and Having clause on the passengers_on_flights table. 

7. Write a SQL query to identify whether the revenue has crossed 450 using the IF clause on the ticket_details table. 

8. Write a SQL query to find the maximum ticket price for each class using window functions on the ticket_details table. 

9. For the route ID 4, write a SQL query to view the execution plan of the passengers_on_flights table. 

10.4 Write a SQL query to calculate the total price of all tickets booked by a customer across different aircraft IDs using rollup function.

11 Write a SQL query to create a view with only business class customers along with the brand of airlines.

12 Write a SQL query to create a stored procedure that extracts all the details from the routes table where the travelled distance is more than 2000 miles. 

13 Write a SQL query to create a stored procedure that groups the distance travelled by each flight into three categories. The categories are, short distance travel (SDT) for >=0 AND <= 2000 miles, intermediate distance travel (IDT) for >2000 AND <=6500, and long-distance travel (LDT) for >6500. 

14. Write a SQL query to extract ticket purchase date, customer ID, class ID and specify if the complimentary services are provided for the specific class using a stored function in stored procedure on the ticket_details table. Condition: If the class is Business and Economy Plus, then complimentary services are given as Yes, else it is No.

## Sample SQL Queries
1. Write a SQL query to display all the passengers (customers) who have travelled in routes 1 to 25.

select customer.*, passengers_on_flights.route_id, passengers_on_flights.travel_date from customer
join passengers_on_flights on customer.customer_id = passengers_on_flights.customer_id
where passengers_on_flights.route_id between 01 and 25
order by customer.customer_id;

2. Write a SQL query to identify the number of passengers and total revenue in business class from the ticket_details table. 

select count(distinct customer_id) as no_of_passengers, 
sum(no_of_tickets*price_per_ticket) as total_revenue
from ticket_details 
where class_id = "Bussiness";

3.  Write a SQL query to identify whether the revenue has crossed 450 using the IF clause on the ticket_details table.

select no_of_tickets, Price_per_ticket,
if(sum(no_of_tickets * price_per_ticket) > 450, "Crossed 450", " Not crossed 450") as revenue_check 
from ticket_details
group by no_of_tickets, Price_per_ticket;

4. Write a SQL query to find the maximum ticket price for each class using window functions on the ticket_details table.

SELECT distinct class_id, 
MAX(price_per_ticket) OVER (PARTITION BY class_id) AS max_price
FROM ticket_details
order by max_price;

5. Write a SQL query to create a stored procedure that groups the distance travelled by each flight into three categories. The categories are, short distance travel (SDT) for >=0 AND <= 2000 miles, intermediate distance travel (IDT) for >2000 AND <=6500, and long-distance travel (LDT) for >6500. 

USE `air_cargo`;
DROP procedure IF EXISTS `distance_miles_category1`;

DELIMITER $$
USE `air_cargo`$$
CREATE PROCEDURE `distance_miles_category1` ()
BEGIN
select flight_num, distance_miles,
case
when distance_miles between 0 and 2000 then "SDT"
when distance_miles between 2000 and 6500 then "IDT"
else "LDT"
end as distance_category
from routes;
END$$

DELIMITER ;

call distance_miles_category1;

## Tech Stack
SQL (MySQL)
Git & GitHub
DB Visualization (Power BI)
