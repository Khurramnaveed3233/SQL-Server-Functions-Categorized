# SQL-Server-Functions-Categorized

#  Aggregate Functions:

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

 - **STDEV() function in SQL Server**

   STDEV() ek SQL function hai jo kisi column ki standard deviation calculate karta hai. Yeh batata hai ke values average se kitni door hain. Yeh sirf numeric data ke liye kaam karta 
   hai.

   Example:
   Maam lo ek bookstore ki sales ka data hai:

       OrderID	   Amount
       1	        20
       2 	        25
       3	        30
       4	        35
       5	        40

Agar hum STDEV(Amount) use karein, toh yeh humein batayega ke sales ki amounts ka variation ( farq ) kitna hai.

    SELECT STDEV(Amount) AS Sales_Deviation
    FROM Orders;

    Result is 7.91

Agar result 7.91 aaye, iska matlab hai ke sales ki values, average ke 7.91 upar ya neeche move karti hain. Agar standard deviation zyada ho, iska matlab hai ke values ek jagah par nahi, balki bohot spread hain. Agar kam ho, toh values ek doosray ke qareeb hain.

Real-life Use:
Agar ek bookstore ki kisi genre ki book sales ka STDEV zyada hai, iska matlab hai ke kabhi sales bohot high hoti hai aur kabhi bohot low. Isko samajhne ke liye business ko analysis karna chahiye.

Variation ka matlab hai farq ya changes kisi bhi cheez ki values mein.

Agar kisi bookstore ki daily sales dekhein:

    Monday:       20 books
    Tuesday:      50 books
    Wednesday:    10 books
    Thursday:     40 books
    Friday:       30 books

Toh yeh sales ek jaisi nahi hain, kabhi zyada, kabhi kam hoti hain. Yeh variation hai.

Agar sales roz barabar hoti (jaise har din 30 books bikti) toh variation kam hota.
Agar sales bohot upar neeche hoti (kabhi 10, kabhi 100 books) toh variation zyada hota.

STDEV() function yahi batata hai ke kisi data ka variation kitna hai. 

 - **VAR() function in SQL Server**

VAR() ek SQL function hai jo variance calculate karta hai. Variance ka matlab hai kisi data ki values average se kitni door hain. Yeh humein batata hai ke data kitna stable ya spread hai.

Asaan Lafzon Mein Samajhna:
Socho ek bookstore ki daily sales hain:

    Monday:    10 books
    Tuesday:   20 books
    Wednesday: 30 books
    Thursday:  40 books
    Friday:    50 books

Yahan sales thodi thodi barhti ja rahi hai, iska matlab kam variation hai, toh variance bhi kam hoga.

Lekin agar sales aise hoti:

    Monday:     5 books
    Tuesday:    50 books
    Wednesday:  8 books
    Thursday:   60 books
    Friday:     2 books

Toh yeh bohot zyada upar neeche ho rahi hain, iska matlab zyada variation hai, toh variance bhi zyada hoga.

Agar hum Orders table mein se book sales ka variance dekhna chahein:

    SELECT VAR(Amount) AS Sales_Variance  
    FROM Orders;

    14108 

Agar variance zyada hai, iska matlab sales bohot unstable hain.
Agar variance kam hai, iska matlab sales ek jaisi chal rahi hain.

Variance ka istemal business analysis mein hota hai, taake yeh samajh sakein ke sales consistent hain ya unpredictable.

 - **Dono functions data ka variation batate hain, lekin tareeqa thoda different hota hai.**

1️⃣ VAR() (Variance):

Yeh batata hai data ki values average se kitni door hain, lekin square form mein hoti hain.
Iska result thoda bara number hota hai.

2️⃣ STDEV() (Standard Deviation):

Yeh bhi data ka variation batata hai, lekin square root le leta hai, taake number asani se samajhne laayak ho jaye.
Iska result chhota aur readable hota hai.

Asaan Example:

Socho ek bookstore ki sales hain: 10, 20, 30, 40, 50
Agar hum VAR() lagayen, toh result aayega: 250
Agar hum STDEV() lagayen, toh result aayega: 15.8

📌 Summary:

  - VAR() ka result bara hota hai (kyunki square hota hai).
  - STDEV() ka result chhota hota hai (kyunki square root leta hai).
  - Dono ka kaam same hai, sirf representation ka farq hai.
  - Zyada STDEV ya VAR ka matlab hai zyada variation (data inconsistent hai).

# String Functions:

-  **LTRIM() – Leading Spaces Hataana**

  LTRIM() kisi string ke start (baayen taraf) se spaces hata deta hai.

     Example: SELECT LTRIM('   Hello World') AS Result;

     Output: 'Hello World' (Shuru ke spaces remove ho gaye)

- **RTRIM() – Trailing Spaces Hataana**

RTRIM() kisi string ke end (dayen taraf) se spaces hata deta hai.

    Example: SELECT RTRIM('Hello World   ') AS Result;
    
    Output: 'Hello World' (Akhri ke spaces remove ho gaye)

 - **REPLACE() – Text Replace Karna**

REPLACE() kisi string ke andar ek word ya character ko doosre se replace karta hai.

    Example: SELECT REPLACE('Hello World', 'World', 'SQL') AS Result;

    Output: 'Hello SQL' (World ko SQL se replace kar diya)

 - **PATINDEX() – Pattern Ki Position Dhoondhna**

PATINDEX() – Pattern Ki Position Dhoondhna

PATINDEX() kisi string mein ek specific pattern ya word ka starting position batata hai.

    Example: SELECT PATINDEX('%SQL%', 'Hello SQL World') AS Result;

    Output: 7 (SQL ka pehla letter 7th position par hai)

Note: % wildcards use hoti hain, taake partial match bhi search ho sake.

# Date and Time Functions:

- GETDATE() – Aaj Ki Tareekh Aur Waqt
  
   Yeh function current date aur time return karta hai.
  
      Example: SELECT GETDATE() AS CurrentDateTime;
      Output: 2025-01-31 14:30:00

- **GETUTCDATE() – Aaj Ki UTC Tareekh Aur Waqt**
  
   Yeh function current date aur time UTC (Universal Time Coordinated) format mein deta hai.
   Example:
  
      SELECT GETUTCDATE() AS CurrentUTC;
      Output: 2025-01-31 09:30:00 (Jo local time se alag ho sakta hai)

- **DATEADD() – Kisi Date Mein Waqt Ya Din Add Karna**

  Yeh function tareekh ya waqt mein din, mahine, saal ya seconds add karne ke liye use hota hai.
  Example:

      SELECT DATEADD(DAY, 5, '2025-01-31') AS NewDate;
      Output: 2025-02-05 (5 din add kar diye)
  
- **DATEDIFF() – Do Dates Ka Difference Nikalna**

  Yeh function do dates ke darmiyan farq (difference) batata hai.
  Example:

      SELECT DATEDIFF(DAY, '2025-01-01', '2025-01-31') AS DaysDifference;
      Output: 30 (Dono dates ke darmiyan 30 din ka farq hai)

- **DATEPART() – Kisi Date Ka Part Extract Karna**

Yeh function kisi date ka specific part nikalta hai, jaise saal, mahina, ya din.
Example:

      SELECT DATEPART(YEAR, '2025-01-31') AS YearPart;
      Output: 2025 (Saal extract kar liya)

- **EOMONTH() – Mahine Ka Akhri Din Nikalna**

   Yeh function kisi bhi date ka last day return karta hai.
   Example:

      SELECT EOMONTH('2025-01-15') AS LastDayOfMonth;
      Output: 2025-01-31







