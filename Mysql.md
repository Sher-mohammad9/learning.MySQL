# Mysql

### How to create the student table in MySQL?
~~~
CREATE TABLE student (
COLUMN_NAME DATATYPE CONSTRAINT,
)
~~~

### How to create the fees table in MySQL?
~~~
CREATE TABLE fees (
COLUMN_NAME DATATYPE CONSTRAINT,
)
~~~

### How to insert a new fee record into the fees table for a particular student?

~~~
INSERT INTO fees (COLUMN_NAME, COLUMN_NAME)
VALUES (VALUE1, VALUE2);
~~~

### How to update a student record in the student table?

~~~
UPDATE student SET COLUMN_NAME = 'UPDATE_VALUE' WHERE condition;
~~~

### How to update a fee record in the fees table?
~~~
UPDATE fees SET COLUMN_NAME = 'UPDATE_VALUE' WHERE condition;
~~~

### How to select all the records from the fees table?
~~~
SELECT * FROM fees;
~~~

### How to select a particular student record from the student table?
~~~
SELECT * FROM student WHERE condition;
~~~

### How to select all the fee records for a particular student from the fees table?
~~~
SELECT * FROM fees WHERE condition;
~~~

### How to get the total number of students in the student table?

~~~
SELECT COUNT(*) FROM student;
~~~

### How to get the sum of all the fees paid by a particular student?

~~~
SELECT SUM(fee) FROM fees WHERE condition;
~~~

### How to get the average fee paid by all the students?
~~~
SELECT AVG(fee) FROM fees;
~~~

### How to get the student record with the highest mobile number in the student table?
~~~
SELECT MAX(mobileNumber) FROM student;
~~~

### How to get the fee record with the highest fee amount in the fees table?
~~~
SELECT MAX(fee) FROM fees;
~~~

### How to get the list of all students who live in a city?
~~~
SELECT COUNT(*),City FROM student GROUP BY City;
~~~

### How to get the list of all students who have paid fees for the month of 'February'?
~~~
SELECT * FROM fees WHERE condition;
~~~

### How to get the list of all cities along with the count of students living in each city?
~~~
SELECT COUNT(*),City FROM student GROUP BY City;
~~~

### How to get the list of all cities along with the count of students living in each city, where the count is greater than 1?
~~~
SELECT COUNT(*),city FROM student GROUP BY city HAVING COUNT(city) > 1;
~~~

### How to get the list of all students sorted by their names in ascending order?
~~~
SELECT * FROM students ORDER BY studentsName;
SELECT * FROM students ORDER BY studentsName ASC;
~~~

### How to get the list of all students sorted by their mobile numbers in descending order? 
~~~
SELECT * FROM students ORDER BY mobileNumber DESC;
~~~

### How to get the list of all fees records sorted by the fee amount in descending order?
~~~
SELECT * FROM fees ORDER BY fee DESC;
~~~

### How to get the list of all fees records sorted by the fee amount in descending order, for a particular student?
~~~
SELECT * FROM fees ORDER BY fee DESC WHERE condition;
~~~

### Find khan

~~~
SELECT * FORM students WHERE sName LIKE '%khan%';
~~~

### where studentid between 5 and 10

~~~
SELECT * FROM students WHERE sId BETWEEN 5 AND 8;
~~~

### Rename fathername column to mothername;

~~~
ALTER TABLE students RENAME COLUMN fName To mName;
~~~

### kaunse month me sbse jyada fees aayi hai;

~~~
SELECT mobths, SUM(amount) AS total FROM fees GROUP BY months ORDER BY total DESC LIMIT 1;
~~~

### kaunse month me sbse kam fees aayi hai

~~~
SELECT months, SUM(amount) AS total FROM fees GROUP BY mounts ORDER BY total ASC LIMIT 1;
~~~

### sbse jyada fees kis student ne di hai

~~~
SELECT sId, SUM(amount)	 AS total FROM fees GROUP BY sId ORDER BY total DESC LIMIT 1;

SELECT * FROM students WHERE sId = ?
~~~

### sbse kam fees kis student ne di hai

~~~
SELECT sId, SUM(amount) AS total FROM fees GROUP BY sId ORDER BY total ASC LIMIT 1;]

SELECT * FROM students WHERE sId = ?
~~~

### aise kaunse student hai jinhone ek b bar fee ni di hai

~~~
SELECT DISTINCT * FROM fees WHERE sId;

SELECT * FROM students WHERE sId NOT IN (1,2,3,4,5,6,7,8,9,10);
~~~

### aise kaunse students hai jinka mobile and fathername ni hai db me

~~~
SELECT * FROM students WHERE fNAME IS NULL AND mNumber IS NULL;

SELECT DISTINCT * FROM students WHERE sId;
~~~

### vo sare students ka record delete krdo jinhone koi fees ni di hai

~~~
SELECT DISTINCT * FROM fees WHERE sId;

DELETE FROM students WHERE sId NOT IN (1,2,3,4,5,6,7,8,9,10);
~~~













