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
months DATE NOT NULL,
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
employeeWork VARCHAR(155) NOT NULL,
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
month DATE NOT NULL,
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

# MySQL Queries

### 1. Name of all students jinhone abi tak koi fees deposit ni ki
```sql
SELECT * FROM student WHERE studentId NOT IN (SELECT studentId FROM Fee);
```

### 2. Sbse jyada fees kis student ne di hai. naam btao
```sql
SELECT studentName, SUM(amount) AS total FROM student JOIN Fee ON student.studentId = Fee.studentId GROUP BY studentName ORDER  BY total DESC LIMIT 1;
```

### 3. Sbse jyada fees me 2nd number pr jo student hai uska naam btao 
```sql
SELECT studentName, SUM(amount) AS total FROM student JOIN Fee ON student.studentId = Fee.studentId GROUP BY studentName ORDER  BY total DESC LIMIT 2;
```

### 4. Coaching me total kitne employees hain unka naam and designation/role show krvao
```sql
SELECT COUNT(*), employeeName, employeeWork FROM employee GROUP BY employeeName, employeeWork;
```

### 5. Kis employee ne kitni salary uthayi hai ab tak vo btao ya month wise
```sql
SELECT employeeName, SUM(amount) FROM employee JOIN salary ON employee.employeeId = salary.employeeId GROUP BY employeeName;
```

### 6. Vo sare students jo abi tak 1 b test me fail hue hai unka naam, subject, totalmarks, passingmarks, obtainedmarks btao
```sql
SELECT student.studentName, test.subjectName, result.totalMarks, test.passingmarks, result.obtainedmarks, result.resultShow FROM student JOIN result ON student.studentId = result.studentId  JOIN test ON student.studentId = test.studentId  AND test.passingmarks > result.obtainedmarks;
```

### 7. Particular month ka kharcha btao. Kharche me tume salary and expenses dono add krne hai 
```sql
SELECT sum(salary.amount) as salray, sum(expense.amount) as expense, sum(salary.amount) + sum(expense.amount) AS   
Total FROM salary LEFT JOIN expense ON salaryId = expenseId;
```
```sql
SELECT (SELECT SUM(amount) FROM salary) + (SELECT SUM(amount) FROM expense) as Total_amount; 
```

### 8. Particular month me total income btao 
```sql
SELECT SUM(amount) FROM Fee WHERE months = '2023-01-31'
```

### 9. Total income aaj tak 
```sql
SELECT SUM(amount) FROM Fee;
```

### 10. Total kharche aaj tak 
```sql
SELECT SUM(amount) FROM expense;
```

### 11. Kis course me kitne students hai vo btane hai coursename startdate time totalstudents
```sql
SELECT course.courseName, course.startDate, course.classTime, COUNT(course.courseName) 
FROM student JOIN studentCourse ON student.studentId = studentCourse.studentId 
JOIN course ON studentCourse.courseId = course.courseId 
GROUP BY course.courseName, course.startDate, course.classTime; 
```

### 12. Vo course btana hai jisme sbse jyada income hui hai 
```sql
SELECT course.courseName, SUM(amount) AS total_amount FROM studentCourse 
JOIN Fee ON Fee.studentId = studentCourse.studentId 
JOIN course ON course.courseId = studentCourse.courseId 
GROUP BY course.courseName ORDER BY total_amount DESC LIMIT 1;
```

### 13. Vo course btana hai jisme sbse kam income hui hai 
```sql
SELECT course.courseName, SUM(amount) AS total_amount FROM studentCourse 
JOIN Fee ON Fee.studentId = studentCourse.studentId 
JOIN course ON course.courseId = studentCourse.courseId 
GROUP BY course.courseName ORDER BY total_amount LIMIT 1;
```

### 14. Kaunsa course hai jisme sbse jyada students hai 
```sql
SELECT course.courseName, COUNT(student.studentId) AS total_student FROM student 
JOIN studentCourse ON student.studentId = studentCourse.studentId 
JOIN course ON course.courseId = studentCourse.courseId GROUP BY course.courseName ORDER BY total_student DESC LIMIT 1;
```

### 15. Kaunsa course hai jisme sbse kam students hain
```sql
SELECT course.courseName, COUNT(student.studentId) AS total_student FROM student 
JOIN studentCourse ON student.studentId = studentCourse.studentId 
JOIN course ON course.courseId = studentCourse.courseId GROUP BY course.courseName ORDER BY total_student LIMIT 1;
```

