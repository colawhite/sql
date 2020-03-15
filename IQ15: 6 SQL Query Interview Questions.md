IQ15: 6 SQL Query Interview Questions <br>
https://www.youtube.com/watch?v=uAWWhEA57bE <br>
**Employee table:** employee_id, f_name, l_name, gender, position, departmentId, Salary <br>
**Department table:** departmentId, departmentName <br>

**1) Return employee record with highest salary** <br>
select * from Employee where Salary = (select max(Salary) from Employee) <br>
**2) Return second highest salary from employee table** <br>
witht tmp as ( <br>
select Salary, rank() over (order by Salary) as rank <br>
from Employee <br>
) <br>
select Salary from tmp <br>
where rank = 2 <br>

**Another solution** <br>
select max(Salary) from Employee where Salary not in (select max(Salary) from Employee) <br>

**3) Select range of employees based on id** <br>
select * from Employee where employee_id between 3 and 15 <br>
**4) Return empolyees with highest Salary and employee's department name** <br>
with tmp as ( <br>
select * from Employee where Salary = (select max(Salary) from Employee) <br>
) <br>
select a.employee_id, a.f_name, a.l_name, a.gender, a.position,b.departmentName <br>
from tmp a, Department b <br>
where a.departmentId = b.departmentId <br>
**5) Return highest salary, employee's name, department name for each department** <br>
witht tmp as ( <br>
select *, rank() over (partition by departmentId order by Salary) as rank <br>
from Employee <br>
) <br>
select a.Salary, cocnat(a.f_name, a.l_name) as employee_name, b.departmentName  <br>
from tmp a, Department b <br>
where a.rank = 1 and a.departmentId = b.departmentId <br>
