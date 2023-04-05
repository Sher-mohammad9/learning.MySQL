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

# Test 2

### 1.Vo students ke name show kro jinke total average marks 60% se kam hai.

~~~
SELECT ResultIdStudent, AVG(Obtainedmarks) AS tm FROM result GROUP BY ResultIdStudent HAVING TM < 60;

SELECT * FROM students WHERE sId IN (?);
~~~

### 2.Topper student kaun hai overall uska naam btao.

~~~
SELECT ResultIdStudent, AVG(Obtainedmarks) AS tm FROM result GROUP BY ResultIdStudent ORDER BY tm DESC LIMIT 1;

SELECT * FROM students WHERE sId IN (?);
~~~

### 3.Particular subject me kaun topper hai us student ka naam btao.

~~~
SELECT ResultIdStudent, AVG(Obtainedmarks) AS tm FROM result WHERE Subject = 'JavaScript' GROUP BY ResultIdStudent ORDER BY TM DESC LIMIT 1;

SELECT * FROM students WHERE sId IN (?);
~~~

### 4.Aise kaunse students hai jinhone 1 b tesr ni dia.

~~~
SELECT DISTINCT ResultIdStudent FROM result WHERE ResultIdStudent;

SELECT * FROM students WHERE sId NOT IN (?);
~~~

### 5.2nd rank pr kaunsa student hai kisi subject me vo btao.

~~~
SELECT ResultIdStudents, AVG(Obtainedmarks) AS tm FROM result WHERE Subject = 'Node.js'
GROUP BY ResultIdStudents ORDER BY tm DESC LIMIT 2;

SELECT * FROM students WHERE sId IN (?);
~~~

### 6.How many students are there in the student table?

~~~
SELECT COUNT(studentsId) FROM student;
~~~

### 7.What is the name of the student with studentid = 5?

~~~
SELECT studentName FROM  studentsId = 5;
~~~

### 8.How many students are there from the city of Mumbai?

~~~
SELECT * FROM student WHERE city = 'Mumbai';
~~~

### 9.What is the email address of the student whose name is 'John Doe'?

~~~
SELECT * FROM student WHERE email LIKE '%John Doe%';
~~~

### 10.What is the total amount of fees paid by the student with studentid = 10?

~~~
SELECT amount FROM fees WHERE studentid = 10;
~~~

### 11.What is the highest amount of fees paid by any student?
~~~
SELECT studentId, SUM(amount) AS tf FROM fees GROUP BY studentId ORDER BY DESC tf LIMIT 1;

SELECT * FROM student WHERE studentId IN (?);
~~~

### 12.What is the average amount of fees paid by all students?

~~~
SELECT AVG(amount) FROM fees studentId;
~~~

### 13.What is the name of the student who paid the highest amount of fees?

~~~
SELECT studentId, SUM(amount) AS tf FROM fees GROUP BY studentId ORDER BY DESC tf LIMIT 1;

SELECT * FROM student WHERE studentId IN (?);
~~~

### 14.What is the total marks obtained by the student with studentid = 7?

~~~
SELECT SUM(obtainedMarks) FROM result WHERE studentid = 7;
~~~~

### 15.What is the highest marks obtained by any student?

~~~
SELECT studentId, SUM(obtainedMarks) AS hm FROM result GROUP BY studentId ORDER BY DESC hm LIMIT 1;

SELECT * FROM student WHERE studentId = ?;
~~~

### 16.What is the average marks obtained by all students?

~~~
SELECT AVG(obtainedMarks) FROM student WHERE studentId = ?;
~~~

### 17.What is the name of the student who obtained the highest marks?

~~~
SELECT studentId, SUM(obtainedMarks) AS hm FROM result GROUP BY studentId ORDER BY DESC hm LIMIT 1;

SELECT * FROM student WHERE studentId = ?;
~~~

### 18. What is the total amount of fees paid by all students from the city of Delhi?

~~~
SELECT studentId FROM student WHERE city = 'Delhi';

SELECT SUM(amount) FROM fees WHERE IN (?);
~~~

### 19.What is the total amount of fees paid for the month of January?

~~~
SELECT SUM(amount) FROM fees WHERE month = 'January';
~~~

### 20.What is the total amount of fees paid by all students for the subject of mathematics?

~~~
SELECT resultId FROM result WHERE Subject = 'JavaScript';

SELECT SUM(amount) FROM fees WHERE IN (?);
~~~

### 21.What is the average marks obtained by the student with studentid = 9 for the subject of science?

~~~
SELECT studentId FROM result WHERE Subject = 'Node.js';

SELECT AVG(obtainedMarks) FROM result WHERE studentid = 9;
~~~

### 22.What is the name of the student who paid the highest amount of fees for the month of February?

~~~
SELECT studentId,SUM(amount) FROM fees WHERE month = 'February' GROUP BY studentId ORDER BY hf DESC LIMIT 1;

SELECT * FROM student WHERE studentId IN (?);
~~~

### 23.What is the name of the student who obtained the highest marks in the subject of English?

~~~
SELECT studentId, SUM(obtainedMarks) AS hm FROM result WHERE Subject = 'JavaScript' GROUP BY studentId ORDER BY DESC hm LIMIT 1;

SELECT * FROM student WHERE studentId = ?;
~~~

### 24.What is the name of the student who paid the highest amount of fees for the subject of computer science?

~~~
SELECT studentId, SUM(amount) AS hf FROM fees WHERE Subject = 'JavaScript' GROUP BY studentId ORDER BY hf DESC LIMIT 1;

SELECT * FROM student WHERE IN (?);
~~~

### 25.What is the name of the student who obtained the highest marks in the subject of mathematics for the test date of '2022-02-15'?

~~~
SELECT studentId, obtainedMarks  AS hf FROM fees WHERE Subject = 'JavaScript' AND date = '2022-02-15' GROUP BY studentId ORDER BY hf DESC LIMIT 1;

SELECT * FROM student WHERE IN (?);
~~~

### 26.What is the total amount of fees paid by all students whose fathers' names start with the letter 'S'?

~~~
SELECT studentId FROM student WFERE fName LIKE 'S%'

SELECT SUM(amount) FROM fees WHERE IN (?);
~~~

### 27.What is the average marks obtained by all students for the subject of science?

~~~
SELECT studentId FROM result WHERE Subject = 'Node.js';

SELECT AVG(obtainedMarks) FROM result WHERE IN (?);
~~~

### 28.What is the name of the student who paid the highest amount of fees for the year 2022?

~~~
SELECT amount AS hf FROM fees WHERE year = '2022' GROUP BY amount ORDER BY hf DESC LIMIT 1;
~~~

### 29.What is the name of the student who obtained the highest marks in the subject of English for the test date of '2022-03-15'?

~~~
SELECT studentId,obtainedMarks AS hm FROM fees WHERE date = '2022-03-15' GROUP BY amount ORDER BY hm DESC LIMIT 1;

SELECT * FROM student WHERE studentId = ?;
~~~

### 30.What is the name of the student who paid the second highest amount of fees for the subject of computer science?

~~~
SELECT studentId, SUM(amount) AS shf FROM fees WHERE subject = 'JavaScript' GROUP BY studentId ORDER BY shf DESC LIMIT 2;

SELECT * FROM student WHERE studentId = ?;
~~~

### 31.What is the name of the student who obtained the highest marks in the subject of mathematics and science combined?

~~~
SELECT studentId,SUM(obtainedMarks) AS hm FROM result WHERE subject = 'JavaSript' AND 
subject = 'Node.js' GROUP BY studentId ORDER BY hm DESC LIMIT 1;

SELECT * FROM student WHERE studentId = ?;
~~~

### 32.What is the name of the student who paid the highest amount of fees for the month of March and the subject of English combined?

~~~
SELECT studentId,SUM(amount) AS hf FROM fees WHERE subject = 'JavaSript' AND 
month = 'March' GROUP BY studentId ORDER BY hm DESC LIMIT 1;

SELECT * FROM student WHERE studentId = ?;
~~~

### 33.What is the name of the student who obtained the highest marks for the test date of '2022-04-15' in any subject?

~~~
SELECT studentId, obtainedMarks AS hm FROM result WHERE date = '2022-04-15' GROUP BY studentId ORDER BY hm DESC LIMIT 1;

SELECT * FROM student WHERE studentId = ?;
~~~

# Test 3

#### Q1What is the query to get all the details of a student along with the fees and result data for the student?
~~~
SELECT * FROM students JOIN cochingFee ON students.sId = cochingFee.sId JOIN result ON result.ResultIdStudent = cochingFee.sId;
~~~

#### Q2 How can we retrieve the data of a student who has paid fees for the month of January?
~~~
SELECT * FROM students JOIN cochingFee ON students.sId = cochingFee.sId AND cochingFee.months = 'February';
~~~

#### Q3 What is the query to get the list of all students who have not yet paid their fees?
~~~
SELECT * FROM students LEFT JOIN cochingFee ON students.sId IN(cochingFee.sId);

SELECT * FROM students WHERE SID NOT IN (SELECT sId FROM cochingFee);
~~~

#### Q4 How can we fetch the list of students who scored more than 80 marks in any subject in the result table?
~~~
SELECT * FROM students JOIN result ON students.sId = result.ResultIdStudent AND result.Obtainedmarks > 80; 
~~~

#### Q5 What is the query to get the details of students along with the total amount of fees they have paid so far?
~~~ 
SELECT *, SUM(amount) AS total FROM students JOIN cochingFee ON students.sId = cochingFee.sId;
~~~

#### Q6 How can we fetch the list of all students along with their fees data and result data, even if they do not have any data in the fees or result table?
~~~
SELECT * FROM students LEFT JOIN cochingFee ON students.sId IN(cochingFee.sId) LEFT JOIN result ON cochingFee.sId IN(result.ResultIdStudent);
~~~

#### Q7 What is the query to get the name, email address, and mobile number of all the students who belong to the city of "Delhi"?
~~~
SELECT sName,fName,mNumber FROM students WHERE city = 'Merta';
~~~

#### Q8 How can we retrieve the details of students who belong to the city of "Mumbai" and have paid their fees for the month of February?
~~~
SELECT * FROM students JOIN cochingFee ON students.sId IN (cochingFee.sId) AND cochingFee.months = 'February' AND students.city = 'Merta';
~~~

#### Q9 What is the query to get the name, email address, and total amount of fees paid by all the students who have paid their fees?
~~~
SELECT sName,fNAME, SUM(amount) AS total FROM students JOIN cochingFee ON students.sId IN (cochingFee.sId) GROUP BY sName,fNAME;
~~~

#### Q10 How can we fetch the details of all students who have taken any test before a specific date?
~~~
SELECT * FROM students JOIN result ON students.sId IN(result.ResultIdStudent) AND result.Testdate < '2023-03-30';
~~~

#### Q11 What is the query to get the name, email address, and subject name of all the students who have scored more than 90 marks in any subject?
~~~
SELECT SNAME,FNAME, Subject FROM students JOIN result ON students.sId IN(result.ResultIdStudent) AND result.Obtainedmarks > 90;
~~~

#### Q12 How can we retrieve the details of students who belong to the city of "Bangalore" and have scored less than 50 marks in any subject?
~~~
SELECT * FROM students JOIN result ON students.sId IN(result.ResultIdStudent) AND result.Obtainedmarks < 50 AND students.city = 'Merta';
~~~

#### Q13 What is the query to get the details of all students along with their fees and result data, sorted by their name in ascending order?
~~~
SELECT * FROM students JOIN cochingFee ON students.sId = cochingFee.sId JOIN result ON result.ResultIdStudent = cochingFee.sId ORDER BY sName;
~~~

#### Q14 How can we fetch the name, email address, and total amount of fees paid by all the students who have not paid their fees yet?
~~~
SELECT sName,fNAME,SUM(amount)FROM students LEFT JOIN cochingFee ON students.sId IN(cochingFee.sId) GROUP BY sName,fNAME;
~~~

#### Q15 What is the query to get the details of all students who have paid their fees for the month of March and have scored more than 70 marks in any subject?
~~~
SELECT * FROM students JOIN cochingFee ON students.sId IN(cochingFee.sId) AND cochingFee.months = 'March' JOIN result ON result.ResultIdStudent IN(cochingFee.sId) AND result.Obtainedmarks > 70;
~~~

#### Q16 How can we retrieve the details of students who have not taken any test yet?
~~~
SELECT * FROM students LEFT JOIN result ON students.sId IN (result.ResultIdStudent);
~~~

#### Q17 What is the query to get the name, email address, and subject name of all the students who have scored less than 40 marks in any subject?
~~~
SELECT sName,fNAME,Subject FROM students JOIN result ON students.sId IN (result.ResultIdStudent) and result.Obtainedmarks < 40;
~~~

#### Q18 How can we fetch the details of students who belong to the city of "Pune" and have paid their fees for the month of January?
~~~
SELECT * FROM students JOIN cochingFee ON students.sId IN(cochingFee.sId) AND students.city = 'Peeh' AND cochingFee.months = 'January';
~~~

#### Q19 What is the query to get the name, email address, and mobile number of all the students who have not taken any test yet?
~~~
SELECT sName,fNAME,mNumber FROM students LEFT JOIN result ON students.sId IN (result.ResultIdStudent);
~~~

#### Q20 How can we retrieve the details of students who have scored more than 60 marks in all the subjects they have taken tests for?
~~~
SELECT * FROM students JOIN result ON students.sId IN (result.ResultIdStudent) AND result.Obtainedmarks > 60;
~~~














