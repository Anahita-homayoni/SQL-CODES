SQL Cheat Sheet & Practice Reference

This repository contains a collection of SQL commands organized by topic.
It serves as a quick reference guide for beginners and a review sheet for experienced SQL users.

📚 1. Database Management
List all databases
SHOW DATABASES;

Create a database
CREATE DATABASE database_name;

Delete a database
DROP DATABASE database_name;

Switch to a database
USE database_name;

🏗️ 2. Table Management
Create a table
CREATE TABLE cats (
    name VARCHAR(50),
    age INT
);

Check that a table exists
SHOW TABLES;
SHOW COLUMNS FROM cats;
DESC cats;

Delete a table
DROP TABLE table_name;

📝 3. Insert Data
Insert a single row
INSERT INTO cats (age, name)
VALUES (2, 'Beth');

Insert multiple rows
INSERT INTO sales (name, age)
VALUES 
    ('Meatball', 5),
    ('Turkey', 1),
    ('Potato Face', 15);

Using NOT NULL
CREATE TABLE cats2 (
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL
);

Using DEFAULT values
CREATE TABLE cats3 (
    name VARCHAR(20) DEFAULT 'no name provided',
    age INT DEFAULT 99
);

🔑 4. Primary Keys
CREATE TABLE unique_sale (
    sale_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL
);

🔍 5. Querying Data
Select all
SELECT * FROM cats;

Select specific columns
SELECT age FROM sales;

Filtering using WHERE
SELECT * FROM cats WHERE age = 4;

Column alias
SELECT sales_id AS id, name FROM cats;

✏️ 6. Updating & Deleting
Update rows
UPDATE sales SET breed = 'Shorthair' 
WHERE breed = 'Tabby';

Delete rows
DELETE FROM sales WHERE name = 'Egg';

📌 7. Distinct & String Functions
Remove duplicates
SELECT DISTINCT author_lname FROM books;

Combine two columns
SELECT DISTINCT CONCAT(author_fname, ' ', author_lname)
FROM books;

📃 8. Sorting & Limiting
SELECT * FROM books ORDER BY author_lname DESC;
SELECT title FROM books LIMIT 3;
SELECT title, released_year 
FROM books ORDER BY released_year DESC LIMIT 5;

🔎 9. Pattern Matching (LIKE)
SELECT * FROM books WHERE author_fname LIKE '%da%';
SELECT * FROM books WHERE author_fname LIKE '____';
SELECT * FROM books WHERE title LIKE '%\%%';   -- find %
SELECT * FROM books WHERE title LIKE '%\_%';   -- find _

🔢 10. Aggregate Functions
SELECT COUNT(*) FROM books;
SELECT MAX(pages) FROM books;
SELECT MIN(released_year) FROM books;
SELECT AVG(pages) FROM books;
SELECT SUM(pages) FROM books;

Grouping
SELECT author_lname, COUNT(*) AS books_written
FROM books
GROUP BY author_lname
ORDER BY books_written DESC;

📅 11. Working With Dates
SELECT CURDATE();
SELECT CURTIME();
SELECT NOW();

Date table example
CREATE TABLE people (
    name VARCHAR(100),
    birthdate DATE,
    birthtime TIME,
    birthdt DATETIME
);

Date functions
SELECT birthdate, DAY(birthdate), MONTHNAME(birthdate)
FROM people;

🕒 12. Timestamps
CREATE TABLE captions (
    text VARCHAR(150),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

🔐 13. Constraints
UNIQUE
CREATE TABLE contacts (
    name VARCHAR(100) NOT NULL,
    phone VARCHAR(15) NOT NULL UNIQUE
);

CHECK
CREATE TABLE palindromes (
    word VARCHAR(100) CHECK (REVERSE(word) = word)
);

ALTER
ALTER TABLE companies DROP COLUMN phone;
ALTER TABLE companies MODIFY company_name VARCHAR(100) DEFAULT 'unknown';

🔗 14. Foreign Keys
CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_date DATE,
    amount DECIMAL(8,2),
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);

🔄 15. JOINS
INNER JOIN
SELECT first_name, last_name, amount
FROM customers
JOIN orders ON orders.customer_id = customers.id;

LEFT JOIN
SELECT first_name, last_name, IFNULL(SUM(amount), 0) AS money_spent
FROM customers
LEFT JOIN orders ON customers.id = orders.customer_id
GROUP BY first_name, last_name;

⭐ 16. Views
CREATE OR REPLACE VIEW ordered_series AS
SELECT * FROM series ORDER BY released_year DESC;

📊 17. Window Functions
OVER()
SELECT emp_no, department, salary,
       AVG(salary) OVER(PARTITION BY department) AS dept_avg
FROM employees;

ROW_NUMBER / RANK
SELECT emp_no, salary,
       ROW_NUMBER() OVER(ORDER BY salary DESC) AS rownum
FROM employees;

NTILE
SELECT emp_no, salary,
       NTILE(4) OVER(ORDER BY salary DESC) AS quartile
FROM employees;

LAG
SELECT emp_no, salary,
       salary - LAG(salary) OVER(ORDER BY salary DESC) AS salary_diff
FROM employees;

📸 18. Example Social Media Schema
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE comments (
    id INT PRIMARY KEY AUTO_INCREMENT,
    comment_text VARCHAR(255) NOT NULL,
    photo_id INT NOT NULL,
    user_id INT NOT NULL,
    FOREIGN KEY (photo_id) REFERENCES photos(id),
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE likes (
    user_id INT NOT NULL,
    photo_id INT NOT NULL,
    PRIMARY KEY (user_id, photo_id),
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (photo_id) REFERENCES photos(id)
);
