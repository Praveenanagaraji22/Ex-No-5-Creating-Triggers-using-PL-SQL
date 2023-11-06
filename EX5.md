# Ex. No: 5 Creating Triggers using PL/SQL
## Date: 31/8/23
### AIM: To create a Trigger using PL/SQL.
### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:
### Create employee table
#### Query:
```
CREATE TABLE employee (empid INT PRIMARY KEY,empname VARCHAR(10),dept VARCHAR(10),salary DECIMAL(10, 2));

insert into employee values (1,'Abi','HR',35000);
insert into employee values (2,'Divya','TL',25000);

select * from employee;
```
#### Table:
![1](https://github.com/Divya110205/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119404855/1726120b-81df-43d4-bc8b-92d5a57c061e)

### Create salary_log table
#### Query:
```
CREATE TABLE salary_log (log_id INT AUTO_INCREMENT PRIMARY KEY,empid INT,empname VARCHAR(10),old_salary DECIMAL(10, 2),
new_salary DECIMAL(10, 2),update_date DATE);

desc salary_log;
```
#### Table:
![2](https://github.com/Divya110205/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119404855/2a275571-344f-4599-a127-828351b4355b)

### PLSQL Trigger code
```
DELIMITER //
CREATE TRIGGER log_salary_update AFTER UPDATE ON employee FOR EACH ROW
BEGIN
  INSERT INTO salary_log (empid, empname, old_salary, new_salary, update_date) VALUES (OLD.empid, OLD.empname,
OLD.salary, NEW.salary, NOW());
END;
//
DELIMITER ;
```
### Output:
![3](https://github.com/Divya110205/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119404855/5e3783f4-dddd-48c9-a11c-68bec8bcf679)

### Updated Tables:
#### Query:
```
UPDATE employee SET salary = 50000 WHERE empid = 1;
UPDATE employee SET salary = 40000 WHERE empid = 2;

SELECT * FROM employee;
SELECT * FROM salary_log;
```
#### Output:
![4](https://github.com/Divya110205/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119404855/32f94782-398c-4597-9a85-79d8a66c89f9)

### Result:
The program has been implemented successfully.
