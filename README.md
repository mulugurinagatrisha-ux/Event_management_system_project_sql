# Event_management_system_project_sql

 use trisha;
CREATE DATABASE event_management_system;

use event_management_system;

CREATE TABLE Customers (
customer_id INT PRIMARY KEY,
name VARCHAR(100) NOT NULL,
email VARCHAR(100) UNIQUE,
phone VARCHAR(15),
registration_date DATE
);


CREATE TABLE Events (
event_id INT PRIMARY KEY,
event_name VARCHAR(100),
event_type VARCHAR(50),
event_date DATE,
location VARCHAR(255),
total_seats INT,
ticket_price DECIMAL(10,2)
);


CREATE TABLE Organizers (
organizer_id INT PRIMARY KEY,
organizer_name VARCHAR(100),
phone VARCHAR(15),
email VARCHAR(100)
);


CREATE TABLE Venues (
venue_id INT PRIMARY KEY,
venue_name VARCHAR(100),
city VARCHAR(100),
capacity INT
);


CREATE TABLE Bookings (
booking_id INT PRIMARY KEY,
customer_id INT,
event_id INT,
booking_date DATE,
tickets INT,
total_amount DECIMAL(10,2),
status VARCHAR(50),
FOREIGN KEY (customer_id) REFERENCES Customers(customer_id),
FOREIGN KEY (event_id) REFERENCES Events(event_id)
);


CREATE TABLE Payments (
payment_id INT PRIMARY KEY,
booking_id INT,
amount DECIMAL(10,2),
payment_date DATE,
payment_method VARCHAR(50),
status VARCHAR(50),
FOREIGN KEY (booking_id) REFERENCES Bookings(booking_id)
);


CREATE TABLE Event_Organizers (
id INT PRIMARY KEY,
event_id INT,
organizer_id INT,
FOREIGN KEY (event_id) REFERENCES Events(event_id),
FOREIGN KEY (organizer_id) REFERENCES Organizers(organizer_id)
);

INSERT INTO Customers VALUES
(1, 'Rahul', 'rahul@gmail.com', '9876549210', '2024-01-10'),
(2, 'Priya', 'priya@gmail.com', '9876543211', '2024-02-12'),
(3, 'Arjun', 'arjun@gmail.com', '9876543212', '2024-03-15'),
(4, 'Sneha', 'sneha@gmail.com', '9876543213', '2024-04-10'),
(5, 'Kiran', 'kiran@gmail.com', '9876543214', '2025-01-01');

INSERT INTO customers VALUES
(6, 'Vijaya', 'vijju@gmail.com', '9876547210', '2025-01-15'),
(7, 'Dravan', 'dravan@gmail.com', '9234567898', '2024-03-24'),
(8, 'Trisha', 'trisha@gmail.com', '9346430722', '2024-08-28'),
(9, 'Vishnu', 'vishnu@gmail.com', '7865439825', '2024-09-29'),
(10, 'Vyshu', 'vyshu@gmail.com', '7895684678', '2024-05-13');


INSERT INTO Events VALUES
(101,'Tech Summit','Technology','2025-08-10','Hyderabad',500,1500),
(102,'Music Fest','Entertainment','2025-09-15','Hydrabad',1000,1200),
(103,'Startup Expo','Business','2025-10-20','Hyderabad',700,1800),
(104,'Food Carnival','Food','2025-07-30','Hydrabad',600,900),
(105,'AI Workshop','Education','2026-02-12','Hyderabad',300,2000),
(106,'ML Workshop','Education','2026-11-22','hydrabad',400,2500),
(107,'Soft Tech Expo','Business','2025-09-25','Hydrabad',500,2400),
(108,'Cricket Tournament','Sports','2026-09-15','Hydrabad',800,2000),
(109,'Art Exhibition','Exbition','2026-10-10','Hydrabad',750,2200),
(110,'Dance Competition','Cultural','2026-11-05','Hydrabad',650,1900);


INSERT INTO Organizers VALUES
(1,'ABC Events','9999999991','abc@gmail.com'),
(2,'Dream Events','9999999992','dream@gmail.com'),
(3,'Event Masters','9999999993','masters@gmail.com'),
(4,'Rishi Events','9867534689','rishi@gmail.com');


INSERT INTO Venues VALUES
(1,'HICC','Hyderabad',5000),
(2,'Vizag Convention','Hydrabad',3000),
(3,'Vijay Convention','Hydrabad',2500),
(4,'Dance Show','Hydrabad',1900);



INSERT INTO Bookings VALUES
(1001,1,101,'2025-07-01',2,3000,'Confirmed'),
(1002,2,102,'2025-07-02',1,1200,'Confirmed'),
(1003,3,101,'2025-07-05',3,4500,'Confirmed'),
(1004,4,104,'2025-07-06',2,1800,'Cancelled'),
(1005,5,105,'2025-07-08',1,2000,'Cancelled');


INSERT INTO Payments VALUES
(1,1001,3000,'2025-07-01','UPI','Paid'),
(2,1002,1200,'2025-07-02','Card','Paid'),
(3,1003,4500,'2025-07-05','Cash','Paid'),
(4,1004,1800,'2025-07-06','UPI','Refunded'),
(5,1005,2000,'2025-07-08','Card','Paid');




INSERT INTO Event_Organizers VALUES
(1,101,1),
(2,102,2),
(3,103,3),
(4,104,2),
(5,105,1);

SELECT * FROM customers;
SELECT * FROM events;
SELECT * FROM organizers;
SELECT * FROM venues;
SELECT * FROM bookings;
SELECT * FROM payments;
SELECT * FROM event_organizers;

SELECT * FROM Events WHERE ticket_price>1000;

SELECT * FROM Events WHERE location='Hyderabad';

SELECT * FROM Events WHERE event_date>'2024-12-31';

SELECT * FROM Customers
ORDER BY registration_date DESC;

SELECT c.name,b.booking_id,b.total_amount
FROM Customers c
JOIN Bookings b
ON c.customer_id=b.customer_id;


SELECT e.event_name,o.organizer_name
FROM Events e
JOIN Event_Organizers eo
ON e.event_id=eo.event_id
JOIN Organizers o
ON eo.organizer_id=o.organizer_id;


SELECT b.booking_id,p.amount,p.payment_method
FROM Bookings b
JOIN Payments p
ON b.booking_id=p.booking_id;


SELECT c.customer_id,
c.name,
e.event_name,
e.event_date,
e.location
FROM Customers c
JOIN Bookings b
ON c.customer_id = b.customer_id
JOIN Events e
ON b.event_id = e.event_id;

desc venues;
desc events;

SELECT COUNT(*) FROM Events;

SELECT AVG(total_amount) FROM Bookings;

SELECT SUM(amount) FROM Payments;

SELECT COUNT(*) FROM Bookings;

SELECT event_id,COUNT(*)
FROM Bookings
GROUP BY event_id
ORDER BY COUNT(*) DESC
LIMIT 1;


SELECT *
FROM Customers
WHERE customer_id NOT IN
(SELECT customer_id FROM Bookings);


SELECT *
FROM Events
WHERE event_id NOT IN
(SELECT event_id FROM Bookings);


SELECT *
FROM Bookings
WHERE total_amount>
(SELECT AVG(total_amount)
FROM Bookings);



SELECT customer_id,
SUM(total_amount) AS total_spent
FROM Bookings
GROUP BY customer_id
HAVING SUM(total_amount) > (
SELECT AVG(total_spent)
FROM (
SELECT SUM(total_amount) AS total_spent
FROM Bookings
GROUP BY customer_id)
AS avg_spending
);



SELECT event_id,
COUNT(*) AS total_bookings
FROM Bookings
GROUP BY event_id
HAVING COUNT(*) > (
SELECT AVG(booking_count)
FROM (
SELECT COUNT(*) AS booking_count
FROM Bookings
GROUP BY event_id) 
AS avg_bookings
);




CREATE VIEW Event_Bookings AS
SELECT e.event_id,
e.event_name,
c.customer_id,
c.name AS customer_name,
b.booking_id,
b.booking_date,
b.tickets,
b.total_amount,
b.status
FROM Events e
JOIN Bookings b
ON e.event_id = b.event_id
JOIN Customers c
ON b.customer_id = c.customer_id;




UPDATE Events
SET location = 'Bangalore',
ticket_price = 1800
WHERE event_id = 101;

select * from events;






CREATE VIEW Payment_History AS
SELECT p.payment_id,
b.booking_id,
c.name AS customer_name,
p.amount,
p.payment_date,
p.payment_method,
p.status
FROM Payments p
JOIN Bookings b
ON p.booking_id = b.booking_id
JOIN Customers c
ON b.customer_id = c.customer_id;


UPDATE Customers
SET email = 'priya_new@gmail.com'
WHERE customer_id = 2;


UPDATE Bookings
SET status = 'Completed'
WHERE booking_id = 1001;

select * from payment_history;



CREATE VIEW Event_Organizer_Details AS
SELECT e.event_id,
e.event_name,
e.event_type,
e.event_date,
o.organizer_name,
o.phone,
o.email
FROM Events e
JOIN Event_Organizers eo
ON e.event_id = eo.event_id
JOIN Organizers o
ON eo.organizer_id = o.organizer_id;


SELECT * FROM Event_Organizer_Details;



CREATE VIEW Customer_Booking_History AS
SELECT c.customer_id,
       c.name,
       e.event_name,
       b.booking_date,
       b.tickets,
       b.total_amount,
       b.status
FROM Customers c
JOIN Bookings b
ON c.customer_id = b.customer_id
JOIN Events e
ON b.event_id = e.event_id;


SELECT * FROM Customer_Booking_History;



CREATE VIEW Event_Revenue AS
SELECT e.event_id,
e.event_name,
SUM(p.amount) AS total_revenue
FROM Events e
JOIN Bookings b
ON e.event_id = b.event_id
JOIN Payments p
ON b.booking_id = p.booking_id
GROUP BY e.event_id, e.event_name;


SELECT * FROM Event_Revenue;



DELIMITER $$

CREATE PROCEDURE InsertCustomer(
    IN p_customer_id INT,
    IN p_name VARCHAR(100),
    IN p_email VARCHAR(100),
    IN p_phone VARCHAR(15),
    IN p_registration_date DATE
)
BEGIN
    INSERT INTO Customers
    VALUES(p_customer_id, p_name, p_email, p_phone, p_registration_date);
END$$

DELIMITER ;


DELIMITER $$

CREATE PROCEDURE CreateBooking(
    IN p_booking_id INT,
    IN p_customer_id INT,
    IN p_event_id INT,
    IN p_booking_date DATE,
    IN p_tickets INT,
    IN p_total_amount DECIMAL(10,2),
    IN p_status VARCHAR(50)
)
BEGIN
    INSERT INTO Bookings
    VALUES(p_booking_id,p_customer_id,p_event_id,
           p_booking_date,p_tickets,p_total_amount,p_status);
END$$

DELIMITER ;


DELIMITER $$

CREATE PROCEDURE GetEventBookings(
    IN p_event_id INT
)
BEGIN
    SELECT *
    FROM Bookings
    WHERE event_id = p_event_id;
END$$

DELIMITER ;


DELIMITER $$

CREATE PROCEDURE TotalRevenue()
BEGIN
    SELECT SUM(amount) AS Total_Revenue
    FROM Payments;
END$$

DELIMITER ;




DELIMITER $$

CREATE PROCEDURE EventsByDate(
    IN p_start_date DATE,
    IN p_end_date DATE
)
BEGIN
    SELECT *
    FROM Events
    WHERE event_date
    BETWEEN p_start_date AND p_end_date;
END$$

DELIMITER ;


SELECT e.event_name,
COUNT(b.booking_id) AS Total_Bookings
FROM Events e
JOIN Bookings b
ON e.event_id = b.event_id
GROUP BY e.event_id,e.event_name
ORDER BY Total_Bookings DESC
LIMIT 5;






SELECT c.customer_id,
c.name,
COUNT(b.booking_id) AS Total_Bookings
FROM Customers c
JOIN Bookings b
ON c.customer_id = b.customer_id
GROUP BY c.customer_id,c.name
ORDER BY Total_Bookings DESC;





SELECT MONTH(payment_date) AS Month,
YEAR(payment_date) AS Year,
SUM(amount) AS Revenue
FROM Payments
GROUP BY YEAR(payment_date),MONTH(payment_date)
ORDER BY Year,Month;



SELECT e.event_name,
COUNT(b.booking_id) AS Booking_Count
FROM Events e
LEFT JOIN Bookings b
ON e.event_id = b.event_id
GROUP BY e.event_id,e.event_name;





ALTER TABLE Events
ADD venue_id INT;

ALTER TABLE Events
ADD CONSTRAINT fk_venue
FOREIGN KEY (venue_id)
REFERENCES Venues(venue_id);





SELECT v.venue_name,
v.capacity,
SUM(b.tickets) AS Total_Tickets_Booked,
ROUND((SUM(b.tickets) / v.capacity) * 100, 2) AS Utilization_Percentage
FROM Venues v
JOIN Events e
ON v.venue_id = e.venue_id
JOIN Bookings b
ON e.event_id = b.event_id
GROUP BY v.venue_id, v.venue_name, v.capacity;





