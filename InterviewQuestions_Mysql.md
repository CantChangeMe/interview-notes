## Mysql interview questions

  #### EmployeeInfo table:

  |EmpID|EmpFname|EmpLname|Department|Project|Address|DOB|Gender|
|-----|--------|--------|----------|-------|-------|---|------|
|1|Sanjay|Mehra|HR|P1|Hyderabad(HYD)|01/12/1976|M|
|2|Ananya|Mishra|Admin|P2|Delhi(DEL)|02/05/1968|F|
|3|Rohan|Diwan|Account|P3|Mumbai(BOM)|01/01/1980|M|
|4|Sonia|Kulkarni|HR|P1|Hyderabad(HYD)|02/05/1992|F|
|5|Ankit|Kapoor|Admin|P2|Delhi(DEL)|03/07/1994|M|


#### EmployeePosition Table:

|EmpID|EmpPosition|DateOfJoining|Salary|
|-----|-----------|-------------|------|
|1|Manager|01/05/2019|500000|
|2|Executive|02/05/2019|75000|
|3|Manager|01/05/2019|90000|
|2|Lead|02/05/2019|85000|
|1|Executive|01/05/2019|300000|

##### 1.Write a query to fetch top N records.
  1.By using the TOP command in SQL Server:
    SELECT TOP N * FROM EmployeePosition ORDER BY Salary DESC;
  2.By using the LIMIT command in MySQL:
    SELECT * FROM EmpPosition ORDER BY Salary DESC LIMIT N;

##### 2.Write a query find number of employees whose DOB is between 02/05/1970 to 31/12/1975 and are grouped according to gender
  
  SELECT COUNT(*), Gender FROM EmployeeInfo WHERE DOB BETWEEN '02/05/1970 ' AND '31/12/1975' GROUP BY Gender;
  
##### 3.Write a query to fetch all the records from the EmployeeInfo table ordered by EmpLname in descending order and Department in the ascending order.
  SELECT * FROM EmployeeInfo ORDER BY EmpFname desc, Department asc;
  
##### 4.Write a query to fetch all employees who also hold the managerial position.
  SELECT E.EmpFname, E.EmpLname, P.EmpPosition 
  FROM EmployeeInfo E INNER JOIN EmployeePosition P ON
  E.EmpID = P.EmpID;-- AND P.EmpPosition IN ('Manager');


##### 5.Write a query to find the Nth highest salary from the table without using TOP/limit keyword.
      SELECT Salary 
    FROM EmployeePosition E1 
    WHERE N-1 = ( 
          SELECT COUNT( DISTINCT ( E2.Salary ) ) 
          FROM EmployeePosition E2 
          WHERE E2.Salary >  E1.Salary );
      
  
##### 6. Write a query to retrieve the last 3 records from the EmployeeInfo table.
    SELECT * FROM EmployeeInfo WHERE
    EmpID <=3 UNION SELECT * FROM
    (SELECT * FROM EmployeeInfo E ORDER BY E.EmpID DESC) 
    AS E1 WHERE E1.EmpID <=3;
    
    
##### 7.Write a query to find the third-highest salary from the EmpPosition table.
      SELECT  salary
    FROM(
    SELECT  salary
    FROM EmployeePosition
    ORDER BY salary DESC limit 3) AS emp
    ORDER BY salary ASC limit 1;
    
##### 8.Write a query to display the first and the last record from the EmployeeInfo table.
    SELECT * FROM EmployeeInfo WHERE EmpID = (SELECT MIN(EmpID) FROM EmployeeInfo);
    
##### 9.Write a query to retrieve Departments who have less than 2 employees working in it.
    select department from EmployeeInfo
    group by(department) having count(department)<2;
