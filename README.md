# SQL-Server-Functions-Categorized

1. Aggregate Functions: 

- **Usage of COUNT and DISTINCT**

This example returns the number of titles an Adventure Works Cycles employee can hold.

    SELECT COUNT(DISTINCT Title)
    FROM HumanResources.Employee;

