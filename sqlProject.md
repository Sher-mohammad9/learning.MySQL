# Create database 

```sql
CREATE DATABASE instituteMangement;
```

# USE database

```sql
USE instituteMangement;
```

# Create Students Table

```sql
CREATE TABLE student(
studentId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
studentName VARCHAR(155) NOT NULL,
fatherName VARCHAR(155) NOT NULL,
mobileNumber BIGINT NOT NULL,
email_address VARCHAR(155) NOT NULL,
admissionDate DATE NOT NULL
);
```

# Create Address table

```sql
CREATE TABLE address(
addressId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
plotNo INTEGER NOT NULL,
colony VARCHAR(155) NOT NULL,
pincode INTEGER NOT NULL,
city VARCHAR(155) NOT NULL,
state VARCHAR(155) NOT NULL,
studentId INTEGER UNSIGNED,
FOREIGN KEY (studentId) REFERENCES student(studentId)
);
```

# Create course table 

```sql
CREATE TABLE course(
courseId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
courseName VARCHAR(155) NOT NULL,
courseFee INTEGER NOT NULL,
startDate DATE NOT NULL,
endDate DATE NOT NULL,
classTime TIME NOT NULL
);
```

# Create studentCourse table

```sql
CREATE TABLE studentCourse(
studentId INTEGER UNSIGNED,
courseId INTEGER UNSIGNED,
FOREIGN KEY (studentId) REFERENCES student(studentId),
FOREIGN KEY (courseId) REFERENCES course(courseId)
);
```

# Create fee table 

```sql
CREATE TABLE Fee(
feeId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
amount INTEGER NOT NULL,
feeMonth DATE NOT NULL,
studentId INTEGER UNSIGNED,
FOREIGN KEY (studentId) REFERENCES student(studentId)
);
```

# Create result table

```sql
CREATE TABLE result(
totalMarks INTEGER NOT NULL,
obtainedMarks INTEGER NOT NULL,
resultShow ENUM('Pass', 'Fail'),
testId INTEGER UNSIGNED,
studentId INTEGER UNSIGNED,
FOREIGN KEY (testId) REFERENCES test(testId),
FOREIGN KEY (studentId) REFERENCES student(studentId)
);
```

# create test table 

```sql
CREATE TABLE test(
testId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
subjectName VARCHAR(155) NOT NULL,
totalMarks INTEGER NOT NULL,
passingMarks INTEGER NOT NULL,	
testDate DATE NOT NULL,
studentId INTEGER UNSIGNED,
FOREIGN KEY (studentId) REFERENCES student(studentId)
);
```

# Create employee table

```sql
CREATE TABLE employee(
employeeId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
employeeName VARCHAR(155) NOT NULL,
emp_Designation VARCHAR(155) NOT NULL,
employeeTypeId INTEGER UNSIGNED,
FOREIGN KEY (employeeTypeId) REFERENCES employeeType(employeeTypeId)
);
```

# Create table employeeType table

```sql
CREATE TABLE employeeType(
employeeTypeId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
employeeType VARCHAR(155) NOT NULL
); 
```

# Create salary table 

```sql
CREATE TABLE salary(
salaryId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
amount INTEGER NOT NULL,
salaryMonth DATE NOT NULL,
employeeId INTEGER UNSIGNED,
FOREIGN KEY(employeeId) REFERENCES employee(employeeId)
);
```

# Create expense table

```sql
CREATE TABLE expense(
expenseId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
expenseDetail VARCHAR(155) NOT NULL,
amount INTEGER NOT NULL,
expenseDate DATE NOT NULL
);
```

# Test 1

### 1. Name of all students jinhone abi tak koi fees deposit ni ki
```sql
SELECT * FROM student WHERE studentId NOT IN (SELECT DISTINCT studentId FROM Fee);
```

### 2. Sbse jyada fees kis student ne di hai. naam btao
```sql
SELECT studentId, studentName, SUM(amount) AS total FROM student JOIN Fee ON student.studentId = Fee.studentId GROUP BY studentId, studentName ORDER  BY total DESC LIMIT 1;
```

### 3. Sbse jyada fees me 2nd number pr jo student hai uska naam btao 
```sql
SELECT studentId, studentName, SUM(amount) AS total FROM student JOIN Fee ON student.studentId = Fee.studentId GROUP BY studentId, studentName ORDER  BY total DESC LIMIT 1,1;
```

### 4. Coaching me total kitne employees hain unka naam and designation/role show krvao
```sql
SELECT employeeId, employeeName, emp_Designation FROM employee GROUP BY employeeId, employeeName, emp_Designation;
```

### 5. Kis employee ne kitni salary uthayi hai ab tak vo btao ya month wise
```sql
SELECT employeeId, employeeName, SUM(amount) FROM employee JOIN salary ON employee.employeeId = salary.employeeId GROUP BY employeeId, employeeName;
```

### 6. Vo sare students jo abi tak 1 b test me fail hue hai unka naam, subject, totalmarks, passingmarks, obtainedmarks btao
```sql
SELECT student.studentId, student.studentName, test.subjectName, result.totalMarks, test.passingmarks, result.obtainedmarks, result.resultShow FROM student JOIN result ON student.studentId = result.studentId  JOIN test ON student.studentId = test.studentId  AND test.passingmarks > result.obtainedmarks GROUP BY student.studentId, student.studentName, test.subjectName, result.totalMarks, test.passingmarks, result.obtainedmarks, result.resultShow;
```

### 7. Particular month ka kharcha btao. Kharche me tume salary and expenses dono add krne hai 
```sql
SELECT (SELECT SUM(amount) FROM salary WHERE MONTH(month) = 2) + (SELECT SUM(amount) FROM expense WHERE MONTH(expenseDate) = 2) as Total_amount; 
```

### 8. Particular month me total income btao 
```sql
SELECT SUM(amount) FROM Fee WHERE MONTH(month) = 2
```

### 9. Total income aaj tak 
```sql
SELECT SUM(amount) FROM Fee;
```

### 10. Total kharche aaj tak 
```sql
SELECT (SELECT SUM(amount) FROM salary) + (SELECT SUM(amount) FROM expense) as Total_amount; 
```

### 11. Kis course me kitne students hai vo btane hai coursename startdate time totalstudents
```sql
SELECT course.courseId, course.courseName, course.startDate, course.classTime, COUNT(course.courseId) 
FROM student JOIN studentCourse ON student.studentId = studentCourse.studentId 
JOIN course ON studentCourse.courseId = course.courseId 
GROUP BY course.courseId, course.courseName, course.startDate, course.classTime; 
```

### 12. Vo course btana hai jisme sbse jyada income hui hai 
```sql
SELECT course.courseId, course.courseName, SUM(amount) AS total_amount FROM studentCourse 
JOIN Fee ON Fee.studentId = studentCourse.studentId 
JOIN course ON course.courseId = studentCourse.courseId 
GROUP BY course.courseId, course.courseName ORDER BY total_amount DESC LIMIT 1;
```

### 13. Vo course btana hai jisme sbse kam income hui hai 
```sql
SELECT course.courseId, course.courseName, SUM(amount) AS total_amount FROM studentCourse 
JOIN Fee ON Fee.studentId = studentCourse.studentId 
JOIN course ON course.courseId = studentCourse.courseId 
GROUP BY course.courseId, course.courseName ORDER BY total_amount LIMIT 1;
```

### 14. Kaunsa course hai jisme sbse jyada students hai 
```sql
SELECT course.courseId, course.courseName, COUNT(student.studentId) AS total_student FROM student 
JOIN studentCourse ON student.studentId = studentCourse.studentId 
JOIN course ON course.courseId = studentCourse.courseId GROUP BY course.courseId, course.courseName ORDER BY total_student DESC LIMIT 1;
```

### 15. Kaunsa course hai jisme sbse kam students hain
```sql
SELECT course.courseId, course.courseName, COUNT(student.studentId) AS total_student FROM student 
JOIN studentCourse ON student.studentId = studentCourse.studentId 
JOIN course ON course.courseId = studentCourse.courseId GROUP BY course.courseId, course.courseName ORDER BY total_student LIMIT 1;
```

# Test 2

### 1. Kaunsa course hai jisme koi admission ni hua hai

```sql
SELECT courseName FROM course WHERE courseId NOT IN(SELECT DISTINCT courseId FROM studentCourse);
```

### 2. Sbse jyada expense from expense table kis chiz ke liye hua hai 
```sql
SELECT expenseDetail, SUM(amount) AS maximum_ExpD FROM expense GROUP BY expenseDetail ORDER BY maximum_ED DESC LIMIT 1;
```


### 3. Employee list print krvani hai unki total paid salary ke descending order me
- Sajid Teacher 100000
- Shahrukh Teacher 80000
- Rehna Peon 20000
```sql
SELECT employee.employeeId, employee.employeeName, employee.emp_Designation, SUM(amount) AS total_salary 
FROM employee LEFT JOIN salary ON salary.employeeId = employee.employeeId 
LEFT JOIN employeeType ON employee.employeeId = employeeType.employeeTypeId 
GROUP BY employee.employeeId, employee.employeeName, employee.emp_Designation ORDER BY total_salary DESC;
```

### 4. Course table ko alter krna hai aur usme ek teacherid column add krna hai jo ki foreign key hogi 
```sql
ALTER TABLE course ADD COLUMN teacherId INTEGER UNSIGNED;
ALTER TABLE course ADD FOREIGN KEY(teacherId) REFERENCES employee(employeeId);
```

### 5. Kaunse course me kaunsa teacher pdhata hai uski detail print krvani hai CourseName CourseTime TeacherName
```sql
SELECT * FROM course;

UPDATE course SET teacherId = 1 WHERE courseId = 1;
UPDATE course SET teacherId = 1 WHERE courseId = 2;
UPDATE course SET teacherId = 2 WHERE courseId = 3;
UPDATE course SET teacherId = 1 WHERE courseId = 4;
UPDATE course SET teacherId = 2 WHERE courseId = 5;

SELECT courseName, classTime, employeeName FROM course 	JOIN employee ON course.teacherId = employee.employeeId;
```

### 6. Student list print krvani hai unki total paid fees ke descending order me
- Sajid Nodejs 100000
- Shahrukh JavaScript 80000
- Rehna HTML 20000
```sql
SELECT student.studentId, student.studentName, course.courseName, SUM(amount) AS total_fee FROM student 
JOIN studentCourse ON  student.studentId = studentCourse.studentId 
JOIN Fee ON student.studentId = Fee.studentId 
JOIN course ON course.courseId = studentCourse.courseId 
GROUP BY student.studentId, student.studentName, course.courseName ORDER BY total_fee DESC;
```
### 7. Kisi b year ka total profit/loss btana hai Total fees - (total salary + total expenses)
```sql
SELECT (SELECT SUM(amount) FROM Fee WHERE YEAR(feeMonth) = 2023) - ((SELECT SUM(amount) FROM salary WHERE YEAR(salaryMonth) = 2023) + (SELECT SUM(amount) FROM expense WHERE YEAR(expenseDate) = 2023)) AS total_amount;
```

### 8. Student count list print krvani hai unki total batch count ke descending order me
- Nodejs 10:00PM 10/01/2023  10/07/2023 30
- JS 9:00PM 10/01/2023  10/07/2023 20
- HTML 10:00AM 10/01/2023  10/07/2023 40
```sql
SELECT course.courseId, course.courseName, course.classTime, course.startDate, course.endDate, COUNT(student.studentId) AS total_student FROM course 
JOIN studentCourse ON studentCourse.courseId = course.courseId 
JOIN student ON student.studentId = studentCourse.studentId
GROUP BY course.courseId, course.courseName, course.classTime, course.startDate, course.endDate ORDER BY total_student DESC;
```

### 9. Student list print krvani hai unki total student in pincode ke descending order me
- 302012 Jhotwara 20
- 303012 Merta 15
- 304013 Sikar 12
```sql
SELECT address.pincode, address.colony, COUNT(address.pincode) AS total_student FROM address 
JOIN student ON student.studentId = address.studentId 
GROUP BY address.pincode, address.colony ORDER BY total_student DESC;
```

### 10. Ek view bnana hai. 
- StudentName Mobie Email CourserName CourseStartDate CourseEndDate 
- Time TotalFees AvgMarks Address(plotno, colony, city, state, pincode)
```sql
CREATE VIEW studentRecord AS
SELECT s.studentName, s.mobileNumber, s.email_Address, c.courseName, c.startDate, c.endDate, c.classTime, 
SUM(f.amount) AS totalFee, AVG(r.obtainedMarks) AS AvgMarks, CONCAT(a.plotNo, ' ', a.colony, ' ', a.city,' ', a.state, ' ', a.pincode) AS address 
FROM student s LEFT JOIN studentCourse sc ON s.studentId = sc.studentId 
LEFT JOIN course c ON c.courseId = sc.courseId 
LEFT JOIN address a ON a.studentId = s.studentId
LEFT JOIN Fee f ON f.studentId = s.studentId
LEFT JOIN result r ON r.studentId = s.studentId 	
GROUP BY  s.studentName, s.mobileNumber, s.email_Address, c.courseName, c.startDate, c.endDate, c.classTime, 
f.amount, address;
```

### 11. Ek view result pr bnana hai 
- StudentName Mobile TotalMakrs TotalOBtainedMarks Avg Rank
- Sajid 945655445 500 400 80 1
```sql
CREATE VIEW studentResult AS 
SELECT s.studentId, s.studentName, s.mobileNumber, r.totalMarks, AVG(r.obtainedMarks) AS AvgMarks
FROM student s 
LEFT JOIN result r ON s.studentId = r.studentId 
GROUP BY s.studentId, s.studentName, s.mobileNumber, r.totalMarks ORDER BY AvgMarks DESC;

SELECT *, ROW_NUMBER() OVER(ORDR BY AvgMarks) AS rank FROM studentResult;
```

### 12. Vo student jinhone koi b fees jama ni krayi hai unko delete kr dena hai student table se  Aur iske child records Address, Result tables me hai vo vha se b delete krna hai
```sql
SET SQL_SAFE_UPDATES = 0;

SET FOREIGN_KEY_CHECKS = 0; -- to disable them

DELETE FROM student WHERE studentId NOT IN(SELECT studentId FROM Fee);

SET FOREIGN_KEY_CHECKS = 1; -- to re-enable them
```

### 13. Expenses table se monthly expenses descending order me btane hai 
- Year Month TotalExpenses
- 2023 Feb 25000
- 2022 Dec 12000
```sql
SELECT YEAR(expense.expenseDate) AS Year, MONTH(expense.expenseDate) AS month, SUM(amount) AS total_expense from expense GROUP BY Year,Month ORDER BY total_expense DESC;
```

### 14. Kaunse teacher ke batch ke students ki performance sbse best hai 
```sql
SELECT e.employeeId, e.employeeName, s.studentName, c.courseName, AVG(r.obtainedMarks) AS marks 
FROM course c JOIN employee e ON c.teacherId = e.employeeId 
JOIN studentCourse sc ON sc.courseId = c.courseId
JOIN student s ON s.studentId = sc.studentId
JOIN result r ON r.studentId = s.studentId
GROUP BY e.employeeId, e.employeeName, s.studentName, c.courseName ORDER BY marks DESC LIMIT 1; 
```

### 15. ek view bnana hai 
- TeacherName BatchName BatchStartDate BatchEndDate Designation TotalFeesDepositByThisBatch  TotalSalar
```sql
CREATE VIEW teacherRecord AS
SELECT e.employeeName, c.courseName, c.startDate, c.endDate, e.emp_Designation, 
SUM(f.amount) AS This_Batch, SUM(sa.amount) AS total_salary 
FROM employee e JOIN course c ON c.teacherId = e.employeeId
JOIN studentCourse sc ON sc.courseId = c.courseId
JOIN student s ON s.studentId = sc.studentId  
JOIN Fee f on f.studentId = s.studentId
JOIN salary sa ON sa.employeeId = e.employeeId
GROUP BY e.employeeName, c.courseName, c.startDate, c.endDate, e.emp_Designation;
```

# Test 3

### 1. Student ka count print krvana hai desc order me unke city ke according. for example totalstudents cityname
- 25 Jaipur 
- 20 Nagaur
```sql
SELECT COUNT(s.studentId), a.City FROM student s 
JOIN address a ON s.studentId = a.studentId AND city = 'Merta city';
```

### 2. Kisi student ki sare months me kitni fees aayi hai vo btani hai sare months ki ab tak 
StudentName MonthName Fees 
- Sajid Feb, 2022 2000
- Sajid March, 2022 1000
- Sajid April 0
- Sajid May 1000
Agar kisi month me koi fees ni aayi hai to 0 dhikana hai  
```sql
SELECT s.studentId, s.studentName, IFNULL(SUM(f.amount), 0) AS total_fee FROM  student s
LEFT JOIN Fee f ON s.studentId = f.studentId 
GROUP BY s.studentId, s.studentName ORDER BY total_fee DESC;
```
### 3. Kisi particular test me total kitne students pass fail hue hai vo btana hai 
TestId TestName TotalPass TotalFail
- 1 Nodejs 10 5
- 2 JS 20 10
```sql
SELECT t.subjectName,r.resultShow, COUNT(r.resultShow) AS total_stu
FROM result r JOIN test t ON t.testId = r.testId GROUP BY t.subjectName, r.resultShow;
```

### 4. Kisi particular month me total kitne test hue hai vo btane hai 
MonthName TotalTests
- May 20
- June 10
```sql
SELECT MONTH(testDate) AS monthName, COUNT(MONTH(testDate)) AS totalTest FROM test GROUP BY monthName;
```

### 5. Kisi particular designation pr kitne employees hai vo btana hai 
Designation Count
Teacher    10
Peon 2
Receptionist 1
```sql 
SELECT employeeWork, COUNT(employeeWork) AS totalEmp FROM employee GROUP BY employeeWork;
```

### 6. Kisi particular designation ke employees ki total salary particular month me kitni hai vo btana hai 
Designation Month TotalSalary
Teacher June 25000
Peon June 10000
Receptionist June 5000
```sql
SELECT e.employeeId, et.employeeType, Month(s.month), s.amount AS totalSalary FROM employee e
JOIN salary s ON e.employeeId = s.salaryId 
JOIN employeeType et ON et.employeeTypeId = e.employeeTypeId
GROUP BY e.employeeId, et.employeeType;
```

### 7. Employees ki totalsalary ko desc order me btao with name 
EmployeeName totalsalary
- Sajid  200000
- Shahrukh 120000
- Raja 80000
```sql
SELECT e.employeeId, e.employeeName, SUM(s.amount) AS totalSalary FROM employee e
JOIN salary s ON s.employeeId = e.employeeId GROUP BY e.employeeId, e.employeeName 
ORDER BY totalSalary DESC;
```

### 8. Ek new table bnani hai jisme ye columns honge 
- TableName : TeacherSalaryRecord
- columnName : SalaryRecordId, TeacherId(foreignkey),   TotalSalary 

```sql
CREATE TABLE TeacherSalaryRecord (
SalaryRecordId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
TeacherId INTEGER UNSIGNED,
TotalSalary INTEGER UNSIGNED NOT NULL,
FOREIGN KEY (TeacherId) REFERENCES employee(employeeId)
);
```

### 9. Ek trigger bnana hai. Aur jab b salary table me kisi b employee ke liye entry hogi
to TeacherSalaryRecord table me uski totalsalary update hogi 
- Salary  : Sajid 10000
- TeacherSalaryRecord : Sajid 10000

- Salary Sajid 20000
- TeacherSalaryRecord : Sajid 30000

```sql
DELIMITER //
CREATE TRIGGER salary_Aupt
AFTER INSERT ON salary 
FOR EACH ROW
BEGIN
   UPDATE TeacherSalaryRecord SET TotalSalary = TotalSalary + NEW.amount WHERE TeacherId = NEW.employeeId;
END;//
```

### 10. Student table me studnetname, fathername pr index bnani hai

```sql
CREATE INDEX Stu_Fat_Ind ON student (studnetName, fatherName);
```
