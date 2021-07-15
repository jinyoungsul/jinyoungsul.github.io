---
title : HackerRank-BasicJoin-Average Population of Each Continent

tags:
    - sql
categories:
    - sql 
date: '2021-07-15'

---

# The Report

You are given two tables: _Students_ and _Grades_. _Students_ contains three columns _ID_, _Name_ and _Marks_.

![](https://s3.amazonaws.com/hr-challenge-images/12891/1443818166-a5c852caa0-1.png)

_Grades_ contains the following data:

![](https://s3.amazonaws.com/hr-challenge-images/12891/1443818137-69b76d805c-2.png)

_Ketty_  gives  _Eve_  a task to generate a report containing three columns:  _Name_,  _Grade_  and  _Mark_.  _Ketty_  doesn't want the NAMES of those students who received a grade lower than  _8_. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

Write a query to help Eve.

**Sample Input**

![](https://s3.amazonaws.com/hr-challenge-images/12891/1443818093-b79f376ec1-3.png)

**Sample Output**
```
Maria 10 99
Jane 9 81
Julia 9 88 
Scarlet 8 78
NULL 7 63
NULL 7 68
```

**Note**

Print "NULL" as the name if the grade is less than 8.

**Explanation**

Consider the following table with the grades assigned to the students:

![](https://s3.amazonaws.com/hr-challenge-images/12891/1443818026-0b3af8db30-4.png)

So, the following students got  _8_,  _9_  or  _10_  grades:

-   _Maria (grade 10)_
-   _Jane (grade 9)_
-   _Julia (grade 9)_
-   _Scarlet (grade 8)_

**My solution**

```sql
SELECT CASE WHEN Grade < 8 THEN 'NULL'
            ELSE Name
            END
        ,Grade
        ,Marks
FROM
(
SELECT Name
       ,CASE WHEN Marks>=1 AND Marks<10 THEN 1
            WHEN Marks>=10 AND Marks<20 THEN 2
            WHEN Marks>=20 AND Marks<30 THEN 3
            WHEN Marks>=30 AND Marks<40 THEN 4
            WHEN Marks>=40 AND Marks<50 THEN 5
            WHEN Marks>=50 AND Marks<60 THEN 6
            WHEN Marks>=60 AND Marks<70 THEN 7
            WHEN Marks>=70 AND Marks<80 THEN 8
            WHEN Marks>=80 AND Marks<90 THEN 9
            WHEN Marks>=90 AND Marks<=100 THEN 10
            END AS Grade
        ,Marks
FROM STUDENTS
ORDER BY Grade DESC, Name ASC, Marks ASC
);
```

**Most vote solution**

```sql
SELECT CASE WHEN g.Grade < 8 THEN 'NULL'
            ELSE Name
            END
        ,g.Grade
        ,s.Marks
FROM Students s, Grades g
WHERE s.Marks BETWEEN G.Min_Mark AND G.Max_Mark
ORDER BY g.Grade DESC, s.Name ASC, s.Marks ASC;
```




