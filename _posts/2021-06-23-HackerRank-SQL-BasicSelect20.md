---
title : HackerRank-BasicSelect-Employee Salaries

tags:
    - sql
categories:
    - sql 
date: '2021-06-23'

---

# Employee Salaries


Write a query that prints a list of employee names (i.e.: the  _name_  attribute) for employees in  **Employee**  having a salary greater than  2000 per month who have been employees for less than  10 months. Sort your result by ascending  _employee_id_.

**Input Format**

The  **Employee**  table containing employee data for a company is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)

where  _employee_id_  is an employee's ID number,  _name_  is their name,  _months_  is the total number of months they've been working for the company, and  _salary_  is the their monthly salary.

**Sample Input**


![](https://s3.amazonaws.com/hr-challenge-images/19629/1458558202-9a8721e44b-ScreenShot2016-03-21at4.32.59PM.png)

**Sample Output**

```
Angela
Michael
Todd
Joe
```

```sql
SELECT NAME
FROM EMPLOYEE
WHERE SALARY > 2000 AND MONTHs < 10
ORDER BY EMPLOYEE_ID;
```

![](https://i.imgur.com/KKTzPiH.png)


