# EX-04 Aggregate Function
#### AIM: 
To study and implement aggregate functions, group by and having clause with suitable examples.

#### THEORY:
An aggregate function is a function that performs a calculation on a set of values, and returns a single value.
Aggregate functions are often used with the GROUP BY clause of the SELECT statement. The GROUP BY clause splits the result-set into groups of values and the aggregate function can be used to return a single value for each group.
The most commonly used SQL aggregate functions are:
MIN() - returns the smallest value within the selected column
Syntax: 
SELECT MIN(column_name)
FROM table_name
WHERE condition;
Example: SELECT MIN (Sal) FROM emp;


MAX() - returns the largest value within the selected column
Syntax: 
SELECT MAX(column_name)
FROM table_name
WHERE condition;
Example: SELECT MAX (Sal) FROM emp;


COUNT() - returns the number of rows in a set
Syntax: 
SELECT COUNT(column_name)
FROM table_name
WHERE condition; 
Example: SELECT COUNT (Sal) FROM emp;


SUM() - returns the total sum of a numerical column
Syntax: 
SELECT SUM(column_name)
FROM table_name
WHERE condition;
Example: SELECT SUM (Sal) From emp;


AVG() - returns the average value of a numerical column
	Syntax: 
	SELECT AVG(column_name)
FROM table_name
WHERE condition;
	Example: Select AVG (10, 15, 30) FROM DUAL; 




GROUP BY: This query is used to group all the records in a relation together for each and every value of a specific key(s) and then display them for a selected set of fields in the relation. 
Syntax: 
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);
Example: SQL> SELECT EMPNO, SUM (SALARY) FROM EMP GROUP BY EMPNO; 


GROUP BY-HAVING: The HAVING clause was added to SQL because the WHERE keyword could not be used with aggregate functions. The HAVING clause must follow the GROUP BY clause in a query and must also precede the ORDER BY clause if used. 
Syntax: 
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);

#### 1.How many appointments are scheduled in each hour of the day?
![Screenshot 2024-05-08 120144](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/77501ba9-46ff-4df4-9705-d00ca1977406)
#### Query:
```
SELECT strftime('%H', AppointmentDateTime) AS HourOfDay,COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY HourOfDay
ORDER BY HourOfDay;
```
#### Output:
![Screenshot 2024-05-08 120413](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/dec7fdfd-eff3-4b3e-be82-ec410c97b44c)
#### 2.What is the most common diagnosis among patients?
![Screenshot 2024-05-08 120504](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/aaf75845-0faf-477d-ac9d-f3baace6c063)
#### Query:
```
SELECT Diagnosis, COUNT(*) AS DiagnosisCount
FROM MedicalRecords
GROUP BY Diagnosis
ORDER BY DiagnosisCount DESC
LIMIT 1;
```
#### Output:
![Screenshot 2024-05-08 120610](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/5a492576-a7c4-43f1-9fc6-32fc06a96256)
#### 3.How many prescriptions were written by each doctor?
![Screenshot 2024-05-08 120735](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/5e4429bf-bccb-483d-bd8f-c2a022f01105)
#### Query:
```
SELECT DoctorID, COUNT(*) AS TotalPrescriptions
FROM Prescriptions
GROUP BY DoctorID
ORDER BY DoctorID;
```
#### Output:
![Screenshot 2024-05-08 120835](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/d7780d23-f23d-4b80-901e-68efd814c0d5)

#### 4.Write a SQL query to count the number of customers. Return number of customers.
![Screenshot 2024-05-08 120946](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/f4918e83-7af5-4202-bc2d-684054fd3440)
#### Query:
```
SELECT COUNT(*) AS COUNT
FROM customer;
```
#### Output:
![Screenshot 2024-05-08 121023](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/7b486388-ba14-4872-92f9-30967c135581)
#### 5.Write a SQL query to find how many employees have an income greater than 50K?
![Screenshot 2024-05-08 121133](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/8a095a21-39d6-4446-97fa-4039b0f460a1)
#### Query:
```
SELECT COUNT(*) AS employees_count
FROM employee
WHERE income > 50000;
```
#### Output:
![Screenshot 2024-05-08 121215](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/179c746c-291d-44dd-84d1-6b07d256a936)
#### 6.Write a SQL query to find the shortest email address in the customer table?
![Screenshot 2024-05-08 121324](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/4e6c4a2b-3218-4ebd-b6d0-443441ccd49f)
#### Query:
```
SELECT name, email, LENGTH(email) AS min_email_length
FROM customer
WHERE LENGTH(email) = (
    SELECT MIN(LENGTH(email))
    FROM customer
    WHERE email IS NOT NULL
)
LIMIT 1;
```
#### Output:
![Screenshot 2024-05-08 121411](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/ed67e5b1-d0bf-4f64-88ef-ec7e5df53da4)
#### 7.Write a SQL query to find the total income of employees aged 40 or above.
![Screenshot 2024-05-08 121548](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/72275e2c-5d08-4632-947d-ba82e31914ee)
#### Query:
```
SELECT SUM(income) AS total_income
FROM employee
WHERE age >= 40;
```
#### Output:
![Screenshot 2024-05-08 121650](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/39b7b6af-ad43-44d8-8b9d-a023b4f466b4)

#### 8.Write the SQL query that achieves the grouping of data by occupation, calculates the total work hours for each occupation, and excludes occupations where the total work hour sum is not greater than 20.
![Screenshot 2024-05-08 121802](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/80afb7f6-9015-4397-8753-f8371fe763e1)
#### Query:
```
SELECT occupation, SUM(workhour)
FROM employee1
GROUP BY occupation
HAVING SUM(workhour) > 20;
```
#### Output:
![Screenshot 2024-05-08 121843](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/93a08282-9dce-422a-9ab0-59e58a2a85f2)
#### 9.Write the SQL query that achieves the grouping of data by city, calculates the average income for each city, and includes only those cities where the average income is greater than 500,000.
![Screenshot 2024-05-08 121925](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/301b9e1c-ddab-47ef-a383-89478ee31371)
#### Query:
```
SELECT city, AVG(income)
FROM employee
GROUP BY city
HAVING AVG(income) > 500000;
```
#### Output:
![Screenshot 2024-05-08 122022](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/7dd47d2f-14b5-4dc6-b05d-63db24884c73)
#### 10.Write the SQL query that accomplishes the grouping of data by age intervals using the expression (age/5)5, calculates the minimum age for each group, and excludes groups where the minimum age is not less than 25.
![Screenshot 2024-05-08 122136](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/f4a49980-bddc-40e2-9b30-99c0c5a9b018)
#### Query
```
SELECT (age / 5) * 5 AS age_group, MIN(age)
FROM customer1
GROUP BY (age / 5) * 5
HAVING MIN(age) < 25;
```
#### Output:
![Screenshot 2024-05-08 122258](https://github.com/syedmokthiyar/DBMS--EX-04/assets/118787294/435fc5d8-a27c-4859-bc64-dc561a088b28)
### Result:
Therefore these are some example to implement Aggregate Functions, Group by and Having Clause.

