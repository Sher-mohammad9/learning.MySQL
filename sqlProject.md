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
CREATE TABLE students(
studentId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
studentName VARCHAR(155) NOT NULL,
fatherName VARCHAR(155) NOT NULL,
mobileNumber BIGINT NOT NULL,
email_address VARCHAR(155) NOT NULL,
age INTEGER NOT NULL,
gender VARCHAR(15) NOT NULL,
admissionDate DATE NOT NULL
);
```

# Create Address table

```sql
CREATE TABLE address(
addressId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
plotNo INTEGER NOT NULL,
colony VARCHAR(155) NOT NULL,
pincode BIGINT NOT NULL,
city VARCHAR(155) NOT NULL,
state VARCHAR(155) NOT NULL,
sId INTEGER, 
FOREIGN KEY (sID) REFERENCES students(studentId)
);
```

# Create course table 

```sql
CREATE TABLE course(
courseId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
subjectName VARCHAR(155) NOT NULL,
subjectFee VARCHAR(155) NOT NULL,
startDate DATE NOT NULL,
endDate DATE NOT NULL,
durationTime TIME,
sId INTEGER,
FOREIGN KEY (sID) REFERENCES students(studentId)
);
```

# Create studentCourse table

```sql
CREATE TABLE studentCourse(
sCourseId INTEGER UNSIGNED AUTO_INCREMENT,
sId INTEGER,
cId INTEGER,
PRIMARY KEY(sCourseId, sId, cId)
);
```

# Create fee table 

```sql
CREATE TABLE fees(
feeId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
amount BIGINT NOT NULL,
months VARCHAR(155) NOT NULL,
sId INTEGER,
FOREIGN KEY (sID) REFERENCES students(studentId)
);
```

# Create result table

```sql
CREATE TABLE result(
resultId INTEGER UNSIGNED AUTO_INCREMENT,
totalMarks INTEGER NOT NULL,
obtainedMarks INTEGER NOT NULL,
resultShow VARCHAR(15) NOT NULL,
testId INTEGER,
sId INTEGER,
PRIMARY KEY(resultId, testId,sId)
);
```

# create test table 

```sql
CREATE TABLE test(
testId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
testName VARCHAR(155) NOT NULL,
totalMarks INTEGER NOT NULL,
passingMarks INTEGER NOT NULL,	
testDate DATE,
sId INTEGER,
FOREIGN KEY (sID) REFERENCES students(studentId)
);
```

# Create employee table

```sql
CREATE TABLE employee(
employeeId INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
employeeName VARCHAR(155) NOT NULL,
employeeWork VARCHAR(155) NOT NULL,
employeeTypeId INTEGER,
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
amount BIGINT NOT NULL,
months VARCHAR(155) NOT NULL,
employeeId INTEGER,
FOREIGN KEY (employeeId) REFERENCES employee(employeeId)
);
```

# Create expense table

```sql
CREATE TABLE expense(
expenseId INTEGER UNSIGNED NOT NULL PRIMARY KEY AUTO_INCREMENT,
expenseDetail VARCHAR(155) NOT NULL,
amount BIGINT NOT NULL,
expenseDate DATE
);
```


