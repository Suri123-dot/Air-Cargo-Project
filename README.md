# Air-Cargo-Analysis-problem-statement
Air Cargo is an aviation company that provides air transportation services for passengers and freight. Air Cargo uses its aircraft to provide different services with the help of partnerships or alliances with other airlines. The company wants to prepare reports on regular passengers, busiest routes, ticket sales details, and other scenarios to improve the ease of travel and booking for customers.

## Project Objective
As a DBA expert, need to focus on identifying the regular customers to provide offers, analyze the busiest route which helps to increase the number of aircraft required and prepare an analysis to determine the ticket sales details. This will ensure that the company improves its operability and becomes more customer-centric and a favorable choice for air travel.

## My Tasks

As a hypothetical applicant for this role, I was tasked with:

Writing and executing SQL queries to answer these requests.
Creating a presentation to showcase these insights, targeting top-level management.

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

## My Approach
Data Extraction with SQL:

-Used MySQL to write queries and fetch the needed data.

Data Visualization:

-Used Power BI to create visuals that made the insights easy to understand and engaging.

Presentation Design:

-Created a clear and professional presentation in Microsoft PowerPoint to share the insights.

Actionable Insights:

-Provided actionable insights and recommendations to assist the management team in making informed decisions.

## Outcome
This project showed my ability to work with complex data queries and share findings in a clear and engaging way. It helped me improve both my technical skills and my ability to explain insights effectively.

## Tech Stack
SQL (Joins, Group By, Window Functions, Subqueries, CASE, Stored Procedures)

Power BI (Visualizations, Report Design)

Git & GitHub (Version Control)

## Folder Structure
Air Cargo Requests: Document containing the 14 Air Cargo business requests.
SQL Queries: Folder containing SQL scripts used to extract data.
Power BI Visualizations: Folder containing Power BI files with data visualizations.
Presentation: PowerPoint file showcasing insights and recommendations.

  ## Key Insights
Identified top 5 customers contributing 70% of business-class revenue.

Determined that Route ID 8 is the busiest, requiring increased aircraft capacity.

Found that 60% of long-distance routes lack complimentary services for Economy Plus customers.

## How to Use
SQL Queries:

Navigate to the SQL Queries folder.

Run the SQL scripts in your MySQL Workbench to extract the necessary data.

Power BI Visualizations:

Open the Power BI files in Power BI Desktop to view the visualizations.

Presentation:

Open the PowerPoint file to view the presentation designed for top-level management.

