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

  Here's the result set.

    Name                          MinSalary             MaxSalary             AvgSalary             EmployeesPerDept
    ----------------------------- --------------------- --------------------- --------------------- ----------------
    Document Control              10.25                 17.7885               14.3884               5
    Engineering                   32.6923               63.4615               40.1442               6
    Executive                     39.06                 125.50                68.3034               4
    Facilities and Maintenance    9.25                  24.0385               13.0316               7
    Finance                       13.4615               43.2692               23.935                10
    Human Resources               13.9423               27.1394               18.0248               6
    Information Services          27.4038               50.4808               34.1586               10
    Marketing                     13.4615               37.50                 18.4318               11
    Production                    6.50                  84.1346               13.5537               195
    Production Control            8.62                  24.5192               16.7746               8
    Purchasing                    9.86                  30.00                 18.0202               14
    Quality Assurance             10.5769               28.8462               15.4647               6
    Research and Development      40.8654               50.4808               43.6731               4
    Sales                         23.0769               72.1154               29.9719               18
    Shipping and Receiving        9.00                  19.2308               10.8718               6
    Tool Design                   8.62                  29.8462               23.5054               6
  
    (16 row(s) affected)
