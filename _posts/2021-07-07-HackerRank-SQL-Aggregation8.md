---
title : HackerRank-Aggregation-Top Earners

tags:
    - sql
categories:
    - sql 
date: '2021-07-07'

---

# Top Earners

We define an employee's _total earnings_ to be their monthly **salary x months** worked, and the _maximum total earnings_ to be the maximum total earnings for any employee in the **Employee** table. Write a query to find the _maximum total earnings_ for all employees as well as the total number of employees who have maximum total earnings. Then print these values as 2 space-separated integers.

**Input Format**
The **Employee** table containing employee data for a company is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)

where _employee_id_ is an employee's ID number, _name_ is their name, _months_ is the total number of months they've been working for the company, and _salary_ is the their monthly salary.

**Sample Input**
![](https://s3.amazonaws.com/hr-challenge-images/19631/1458559098-23bf583125-ScreenShot2016-03-21at4.32.59PM.png)

**Sample Output**
```
69952 1
```

**Explanation**

The table and earnings data is depicted in the following diagram:

![](https://s3.amazonaws.com/hr-challenge-images/19631/1458559218-9f37585c7a-ScreenShot2016-03-21at4.49.23PM.png)

The maximum _earnings_ value is 69952. The only employee with _earnings_  69952 is _Kimberly_, so we print the maximum _earnings_ value (69952) and a count of the number of employees who have earned 69952(which is 1) as two space-separated values.

**My solution 1**
```sql
SELECT max(earnings), count(earnings)
FROM
(
    SELECT salary*months as earnings, RANK() OVER(order by salary*months DESC) as rank
    FROM Employee
)
GROUP BY rank
HAVING rank=1;
```

**My solution 2**
```sql
SELECT *
FROM
(
SELECT salary*months as earnings, count(*)
FROM employee
GROUP BY salary*months
ORDER BY salary*months DESC
)
WHERE ROWNUM = 1;
```

![](https://i.imgur.com/enNIW5G.png)


