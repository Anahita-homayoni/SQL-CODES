# SQL-CODES
To list available databases: show databases;
The general command for creating a database:CREATE DATABASE <database_name>;
drop a database: DROP DATABASE <database-name>;
To use a database:USE <database-name>;
Creating Tables:CREATE TABLE cats (name VARCHAR(50),age INT);
How Do We Know It Worked? SHOW tables; SHOW COLUMNS FROM cats; DESC cats;
To drop a table: DROP TABLE <table-name>;
To view all rows in our table:SELECT * FROM cats;
Single insert (switching order of name and age):INSERT INTO cats (age, name)VALUES   (2, 'Beth');
Multiple Insert: INSERT INTO sales (name, age) VALUES   ('Meatball', 5),   ('Turkey', 1),   ('Potato Face', 15);
Using NOT NULL:CREATE TABLE cats2 (name VARCHAR(100) NOT NULL,age INT NOT NULL);
Define a table with a DEFAULT name specified:CREATE TABLE sales3( name VARCHAR(20) DEFAULT 'no name provided', age INT DEFAULT 99);
Define a table with a DEFAULT name specified:CREATE TABLE cats3  (name VARCHAR(20) DEFAULT 'no name provided',age INT DEFAULT 99);
specifying a PRIMARY KEY: CREATE TABLE unique_sale (sale_id INT PRIMARY KEY,name VARCHAR(100) NOT NULL,age INT NOT NULL);
To only get the age column:SELECT age FROM sales;
Use where to specify a condition: SELECT * FROM cats WHERE age = 4;
Use 'AS' to alias a column in your results (it doesn't actually change the name of the column in the table):SELECT sales_id AS id, name FROM cats;

       
