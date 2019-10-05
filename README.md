# Viome-Coding-Challenge-


Java Programming Test

PREPARATION:
You will be given a sample database of a small DVD rental business. In your Postgres server on your laptop, please create a database named dvdrentals. Then, populate the database using the assigned sql file. For your convenience, the DB’s table diagrams have been provided on the next page. Please create an Eclipse Java project and name it using your last name, all lowercase, with no spaces.


QUESTION 1:
In your source directory, create the following packages: com.viome.interview.models com.viome.interview.business com.viome.interview.dao
Using these packages and a DAO programming pattern, write a Java program that when given a customer’s first name as a command line argument outputs either “true” or “false” depending on whether the customer is in the database. Your main class must be located in com.viome.interview.business
With the name: CheckCustomer.


QUESTION 2:

In another class, write a function that changes customers located in Vancouver to New York.
Please note that your main class must be located in
com.viome.interview.business
With the name: UpdateCustomers.

SUBMISSION:
Please upload your project to Google Drive and share it to pedro@viome.com.
* Please use hibernate to communicate with the DB.
 

Database Concepts Test

QUESTION 1:

Write a query to run on the dvdrentals database that:
Lists all customers’ cities whose monthly payments exceed $5 in the last year.

select city from city
where city_id in (select city_id from address 
		       where address_id  in (select address_id from customer
where customer_id in (SELECT gg.customer_id
From (SELECT customer_id, EXTRACT(MONTH FROM payment_date) as mon 
		From payment
		Group By EXTRACT(MONTH FROM payment_date), customer_id
		Having sum(amount) > 5) as gg 
group by gg.customer_id
having count(*)= (select count(distinct EXTRACT(MONTH FROM payment_date))
				 from payment)
)))


  




Note: Here I have taken the fact that in every month if customer’s payment exceeds 5 then only the city which customer’s live in will be there in the result.


QUESTION 2:

Write a query to run on the dvdrentals database that:
Deletes all staﬀ who have fewer than 5 rentals in the last month.

Delete from staff
Where staff_id in(select staff_id
		      From rental
Where DATEPART(m, rental_date) = DATEPART(m, DATEPART(m, -1, getdate())
AND
DATEPART(yyyy, rental_date) = DATEPART(m, DATEPART(m , -1, getdate())
Group by staff_id
Having count(*) < 5
