# SQL-Server-Functions-Categorized

1. Aggregate Functions: 

- **Usage of COUNT and DISTINCT**

This example returns the number of titles an Adventure Works Cycles employee can hold.

    SELECT COUNT(DISTINCT Title)
    FROM HumanResources.Employee;
    
- **Use Of Count With OVER clause**

This example uses the MIN, MAX, AVG and COUNT functions with the OVER clause, to return aggregated values for each department in the AdventureWorks2022 database HumanResources.Department table.

    SELECT DISTINCT Name
      , MIN(Rate) OVER (PARTITION BY edh.DepartmentID) AS MinSalary
      , MAX(Rate) OVER (PARTITION BY edh.DepartmentID) AS MaxSalary
      , AVG(Rate) OVER (PARTITION BY edh.DepartmentID) AS AvgSalary
      , COUNT(edh.BusinessEntityID) OVER (PARTITION BY edh.DepartmentID) AS EmployeesPerDept
    
    FROM HumanResources.EmployeePayHistory AS eph
    JOIN HumanResources.EmployeeDepartmentHistory AS edh  ON eph.BusinessEntityID = edh.BusinessEntityID
    JOIN HumanResources.Department AS d ON d.DepartmentID = edh.DepartmentID
    WHERE edh.EndDate IS NULL
    ORDER BY Name;

  
