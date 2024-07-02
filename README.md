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
Updating Data Change long hair to shorthair:UPDATE sales SET breed='Shorthair' WHERE breed='Tabby';
Delete all sales with name of 'Egg':DELETE FROM sales WHERE name='Egg';    
avoide duplicate: SELECT DISTINCT author_lname FROM books;
Combine two columns:SELECT DISTINCT CONCAT(author_fname,' ', author_lname) FROM books;
SELECT * FROM books ORDER BY author_lname DESC;
SELECT * FROM books ORDER BY released_year;
SELECT book_id, author_fname, author_lname, pages FROM books ORDER BY author_lname, author_fname;
SELECT book_id, author_fname, author_lname, pages FROM books ORDER BY 2 desc;
SELECT title FROM books LIMIT 3;
SELECT * FROM books LIMIT 1;
SELECT title, released_year FROM books ORDER BY released_year DESC LIMIT 5;
SELECT title, released_year FROM books ORDER BY released_year DESC LIMIT 1,3;
SELECT title, author_fname, author_lname, pages FROM booksWHERE author_fname LIKE '%da%';
SELECT * FROM books WHERE author_fname LIKE '____';
SELECT * FROM books WHERE author_fname LIKE '_a_';
To select books with '%' in their title:
SELECT * FROM books WHERE title LIKE '%\%%';
To select books with an underscore '_' in title:SELECT * FROM books WHERE title LIKE '%\_%';
SELECT COUNT(*) FROM books; 
SELECT COUNT(author_lname) FROM books; 
SELECT COUNT(DISTINCT author_lname) FROM books;
SELECT author_lname, COUNT(*) AS books_written FROM  books GROUP BY author_lname ORDER BY books_written DESC;
SELECT MAX(pages) FROM books; 
SELECT MIN(author_lname) FROM books;
SELECT title, pages FROM books WHERE pages = (SELECT MAX(pages) FROM books);
SELECT MIN(released_year) FROM books;
SELECT title, released_year FROM books 
WHERE released_year = (SELECT MIN(released_year) FROM books);
SELECT author_fname, author_lname, COUNT(*) FROM books GROUP BY author_lname, author_fname;
SELECT CONCAT(author_fname, ' ', author_lname) AS author,  COUNT(*)FROM books GROUP BY author;
SELECT author_lname, MIN(released_year) FROM books GROUP BY author_lname;
SELECT author_lname, MAX(released_year), MIN(released_year) FROM books GROUP BY author_lname;
SELECT 	author_lname, 	COUNT(*) as books_written, 	MAX(released_year) AS latest_release,	MIN(released_year)  AS earliest_release,MAX(pages) AS longest_page_count FROM books GROUP BY author_lname;
SELECT 	author_lname, author_fname,	COUNT(*) as books_written,MAX(released_year) AS latest_release,	MIN(released_year)  AS earliest_release FROM books GROUP BY author_lname, author_fname;
SELECT SUM(pages) FROM books; 
SELECT author_lname, COUNT(*), SUM(pages)FROM books GROUP BY author_lname;
SELECT AVG(pages) FROM books; 
SELECT AVG(released_year) FROM books; 
SELECT released_year, AVG(stock_quantity),COUNT(*) FROM books GROUP BY released_year;
CREATE TABLE people (name VARCHAR(100),birthdate DATE,birthtime TIME,birthdt DATETIME);
SELECT CURTIME(); 
SELECT CURDATE(); 
SELECT NOW(); 
INSERT INTO people (name, birthdate, birthtime, birthdt)VALUES ('Hazel', CURDATE(), CURTIME(), NOW());
SELECT birthdate,DAY(birthdate),DAYOFWEEK(birthdate),DAYOFYEAR(birthdate)FROM people;
SELECT birthdate,MONTHNAME(birthdate),YEAR(birthdate)FROM people;
SELECT birthtime,HOUR(birthtime),MINUTE(birthtime)FROM people;
SELECT birthdate, DATE_FORMAT(birthdate, '%a %b %D') FROM people; 
SELECT birthdt, DATE_FORMAT(birthdt, '%H:%i') FROM people; 
SELECT birthdt, DATE_FORMAT(birthdt, 'BORN ON: %r') FROM people;
CREATE TABLE captions (text VARCHAR(150),created_at TIMESTAMP default CURRENT_TIMESTAMP); 
CREATE TABLE captions2 (text VARCHAR(150),  created_at TIMESTAMP default CURRENT_TIMESTAMP,updated_at TIMESTAMP ON UPDATE CURRENT_TIMESTAMP);
SELECT * FROM books WHERE released_year != 2017;
SELECT * FROM books WHERE title NOT LIKE '%e%';
SELECT * FROM books WHERE released_year > 2005;
SELECT * FROM books WHERE pages > 500;
SELECT * FROM books WHERE released_year < 2000;
SELECT * FROM books WHERE released_year <= 1985;
SELECT title, author_lname, released_year FROM books
WHERE released_year > 2010 AND author_lname = 'Eggers';
SELECT title, author_lname, released_year FROM books WHERE author_lname='Eggers' OR released_year > 2010;
SELECT title, released_year FROM books WHERE released_year <= 2015 AND released_year >= 2004;
SELECT * FROM people WHERE birthtime BETWEEN CAST('12:00:00' AS TIME)AND CAST('16:00:00' AS TIME);
CREATE TABLE contacts (	name VARCHAR(100) NOT NULL,phone VARCHAR(15) NOT NULL UNIQUE);
CREATE TABLE palindromes (word VARCHAR(100) CHECK(REVERSE(word) = word));
ALTER TABLE companies DROP COLUMN phone;
CREATE TABLE users2 ( username VARCHAR(20) NOT NULL, age INT, CONSTRAINT age_not_negative CHECK (age >= 0));
CREATE TABLE houses ( purchase_price INT NOT NULL, sale_price INT NOT NULL, CONSTRAINT sprice_gt_pprice CHECK(sale_price >= purchase_price));
ALTER TABLE companies ADD COLUMN employee_count INT NOT NULL DEFAULT 1;
RENAME TABLE companies to suppliers;
ALTER TABLE suppliers RENAME TO companies;
ALTER TABLE companies MODIFY company_name VARCHAR(100) DEFAULT 'unknown';
ALTER TABLE suppliers CHANGE business biz_name VARCHAR(50);
ALTER TABLE houses ADD CONSTRAINT positive_pprice CHECK (purchase_price >= 0);
ALTER TABLE houses DROP CONSTRAINT positive_pprice;
CREATE TABLE customers (id INT PRIMARY KEY AUTO_INCREMENT,first_name VARCHAR(50),last_name VARCHAR(50),email VARCHAR(50));
Foreighn key:CREATE TABLE orders (id INT PRIMARY KEY AUTO_INCREMENT,order_date DATE,amount DECIMAL(8,2),customer_id INT,FOREIGN KEY (customer_id) REFERENCES customers(id));
inner join:SELECT * FROM customers JOIN orders ON orders.customer_id = customers.id;
SELECT first_name, last_name, order_date, amount FROM customers JOIN orders ON orders.customer_id = customers.id;
INNER JOINS:SELECT first_name, last_name, SUM(amount) AS total FROM customers JOIN orders ON orders.customer_id = customers.id GROUP BY first_name , last_name ORDER BY total;
SELECT first_name, last_name, order_date, amount FROM customers LEFT JOIN orders ON orders.customer_id = customers.id;
SELECT order_date, amount, first_name, last_name FROM orders LEFT JOIN customers ON orders.customer_id = customers.id;
