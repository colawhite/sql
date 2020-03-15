IQ15: 6 SQL Query Interview Questions

** Employee table: ** employee_id, f_name, l_name, gender, position, departmentId, Salary
** Department table: ** departmentId, departmentName

** 1) Return employee record with highest salary **
select * from Employee where Salary = (select max(Salary) from Employee)
** 2) Return second highest salary from employee table **
witht tmp as (
select Salary, rank() over (order by Salary) as rank
from Employee
)
select Salary from tmp
where rank = 2
** 3) Select range of employees based on id **
** 4) Return empolyees with highest Salary and employee's department name **
with tmp as (
select * from Employee where Salary = (select max(Salary) from Employee)
)
select a.employee_id, a.f_name, a.l_name, a.gender, a.position,b.departmentName
from tmp a, Department b
where a.departmentId = b.departmentId
** 5) Return highest salary, employee's name, department name for each department **
witht tmp as (
select *, rank() over (partition by departmentId order by Salary) as rank
from Employee
)
select a.Salary, cocnat(a.f_name, a.l_name) as employee_name, b.departmentName 
from tmp a, Department b
where a.rank = 1 and a.departmentId = b.departmentId
