# Event_management_system_project_sql

 create table customers(
-> customer_id int primary key,
-> name varchar(100) not null,
-> email varchar(100) unique,
-> phone varchar(15),
-> registration_date date
-> );
Query OK, 0 rows affected (0.0593 sec)
 MySQL  localhost:33060+ ssl  trisha  SQL > desc customers;
+-------------------+--------------+------+-----+---------+-------+
| Field             | Type         | Null | Key | Default | Extra |
+-------------------+--------------+------+-----+---------+-------+
| customer_id       | int          | NO   | PRI | NULL    |       |
| name              | varchar(100) | NO   |     | NULL    |       |
| email             | varchar(100) | YES  | UNI | NULL    |       |
| phone             | varchar(15)  | YES  |     | NULL    |       |
| registration_date | date         | YES  |     | NULL    |       |
+-------------------+--------------+------+-----+---------+-------+
create database events;
Query OK, 1 row affected (0.0197 sec)
create table events( event_id int primary key, event_name varchar(100), event_type varchar(50), event_date date, location varchar(255), total_seats int );
Query OK, 0 rows affected (0.0421 sec)
create database organizers;
Query OK, 1 row affected (0.0194 sec)
 MySQL  localhost:33060+ ssl  trisha  SQL > create table organizers(
                                         -> organizer_id int primary key,
                                         -> organizer_name varchar(100),
                                         -> phone varchar(15),
                                         -> email varchar(100)
                                         -> );
Query OK, 0 rows affected (0.0356 sec)

 MySQL  localhost:33060+ ssl  trisha  SQL > create database venus;
Query OK, 1 row affected (0.0085 sec)
 MySQL  localhost:33060+ ssl  trisha  SQL > create table venus(
                                         -> venu_id int primary key,
                                         -> venu_name varchar(100),
                                         -> city varchar(100),
                                         -> capacity int
                                         -> );
Query OK, 0 rows affected (0.0416 sec)

 MySQL  localhost:33060+ ssl  trisha  SQL > create database bookings;
Query OK, 1 row affected (0.0122 sec)
 MySQL  localhost:33060+ ssl  trisha  SQL > CREATE TABLE Bookings (
                                         -> booking_id INT PRIMARY KEY,
                                         -> customer_id INT,
                                         -> event_id INT,
                                         -> booking_date DATE,
                                         -> tickets INT,
                                         -> total_amount DECIMAL(10,2),
                                         -> status VARCHAR(50),
                                         -> FOREIGN KEY (customer_id) REFERENCES Customers(customer_id),
                                         -> FOREIGN KEY (event_id) REFERENCES Events(event_id)
                                         -> );
Query OK, 0 rows affected (0.0415 sec)

 MySQL  localhost:33060+ ssl  trisha  SQL > create database payments;
Query OK, 1 row affected (0.0198 sec)
 MySQL  localhost:33060+ ssl  trisha  SQL > CREATE TABLE Payments (
                                         -> payment_id INT PRIMARY KEY,
                                         -> booking_id INT,
                                         -> amount DECIMAL(10,2),
                                         -> payment_date DATE,
                                         -> payment_method VARCHAR(50),
                                         -> status VARCHAR(50),
                                         -> FOREIGN KEY (booking_id) REFERENCES Bookings(booking_id)
                                         -> );
Query OK, 0 rows affected (0.0274 sec)

 MySQL  localhost:33060+ ssl  trisha  SQL > create database event_organizers;
Query OK, 1 row affected (0.0212 sec)
 MySQL  localhost:33060+ ssl  trisha  SQL > CREATE TABLE Event_Organizers (
                                         -> id INT PRIMARY KEY,
                                         -> event_id INT,
                                         -> organizer_id INT,
                                         -> FOREIGN KEY (event_id) REFERENCES Events(event_id),
                                         -> FOREIGN KEY (organizer_id) REFERENCES Organizers(organizer_id)
                                         -> );
Query OK, 0 rows affected (0.0361 sec)

 MySQL  localhost:33060+ ssl  trisha  SQL > insert into customers values (111,'ravi','ravi23@gmail.com',3456788990,'2024-1-14'),
                                         -> (112,'lakshman','lucky@gmailcom',9343456789,'2024-06-12'),
                                         -> (113,'ganesh','gani@gmail.com',9876345602,'2024-02-20'),
                                         -> (114,'rohith','roki@gmail.com',9550346169,'2024-03-24'),
                                         -> (115,'manasa','manasa123@gmail.com',3456788909,'2024-04-17'),
                                         -> (117,'lakshmi','lucky75@gmail.com',6302236043,'2024-10-11'),
                                         -> (118,'srikanth','srikanth90@gmail.com',9087890986,'2024-11-29'),
                                         -> (119,'ramesh','ramesh456@gmail.com',4756446376,'2024-08-27'),
                                         -> (120,'priya','priya24@gmail.com',1235689968,'2024-07-07');
Query OK, 10 rows affected (0.0890 sec)
 MySQL  localhost:33060+ ssl  trisha  SQL > select * from customers;
+-------------+----------+----------------------+------------+-------------------+
| customer_id | name     | email                | phone      | registration_date |
+-------------+----------+----------------------+------------+-------------------+
|         111 | ravi     | ravi23@gmail.com     | 3456788990 | 2024-01-14        |
|         112 | lakshman | lucky@gmailcom       | 9343456789 | 2024-06-12        |
|         113 | ganesh   | gani@gmail.com       | 9876345602 | 2024-02-20        |
|         114 | rohith   | roki@gmail.com       | 9550346169 | 2024-03-24        |
|         115 | manasa   | manasa123@gmail.com  | 3456788909 | 2024-04-17        |
|         116 | trisha   | trisha@gmail.com     | 9346430722 | 2024-09-27        |
|         117 | lakshmi  | lucky75@gmail.com    | 6302236043 | 2024-10-11        |
|         118 | srikanth | srikanth90@gmail.com | 9087890986 | 2024-11-29        |
|         119 | ramesh   | ramesh456@gmail.com  | 4756446376 | 2024-08-27        |
|         120 | priya    | priya24@gmail.com    | 1235689968 | 2024-07-07        |
+-------------+----------+----------------------+------------+-------------------+


                                         
