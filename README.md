# SQL-Server-Functions-Categorized

1. Aggregate Functions: 

- **A. Use COUNT and DISTINCT**

This example returns the number of titles an Adventure Works Cycles employee can hold.

    SELECT COUNT(DISTINCT Title)
    FROM HumanResources.Employee;

