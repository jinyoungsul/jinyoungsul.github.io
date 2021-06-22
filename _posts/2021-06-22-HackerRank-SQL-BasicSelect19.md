---
title : HackerRank-BasicSelect-Employee Names - order by

tags:
    - sql
categories:
    - sql 
date: '2021-06-22'

---

# Employee Names - order by

Write a query that prints a list of employee names (i.e.: the  _name_  attribute) from the  **Employee**  table in alphabetical order.

**Input Format**

The  **Employee**  table containing employee data for a company is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)

where  _employee_id_  is an employee's ID number,  _name_  is their name,  _months_  is the total number of months they've been working for the company, and  _salary_  is their monthly salary.

**Sample Input**


![](https://s3.amazonaws.com/hr-challenge-images/19629/1458558202-9a8721e44b-ScreenShot2016-03-21at4.32.59PM.png)

**Sample Output**

```
Angela
Bonnie
Frank
Joe
Kimberly
Lisa
Michael
Patrick
Rose
Todd
```

```sql
SELECT NAME
FROM EMPLOYEE
ORDER BY NAME ASC;
```

![](https://i.imgur.com/Mm32cpa.png)


