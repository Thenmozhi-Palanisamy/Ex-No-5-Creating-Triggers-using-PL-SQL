# Ex. No: 5 Creating Triggers using PL/SQL

## DATE:1.9.23

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
```
CREATE TABLE employed(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE sal_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employed values(1,'Shakthi','IT',1000000);
insert into employed values(2,'Suju','SALES',500000)

````
## Create employee table

![5-1](https://github.com/Thenmozhi-Palanisamy/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/95198708/16e5f06f-4e40-4f06-92b6-91fc026cbbb4)

## Create salary_log table

![5-2](https://github.com/Thenmozhi-Palanisamy/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/95198708/c69b0e29-4491-46b1-b961-64481f88db73)


## PLSQL Trigger code
```
-- Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employed
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employed values(1,'Shakthi','IT',1000000);
insert into employed values(2,'Suju','SALES',500000);

-- Update the salary of an employee
UPDATE employed
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employed;

-- Display the salary_log table
SELECT * FROM sal_log;

```
## output:

![5-3](https://github.com/Thenmozhi-Palanisamy/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/95198708/1cef5005-f658-4c36-b243-eaa47eb9257d)


![5-4](https://github.com/Thenmozhi-Palanisamy/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/95198708/605f733d-edfe-4cb9-b8a8-05d025b19159)


## Result:
Thus the program implemented successfully.
