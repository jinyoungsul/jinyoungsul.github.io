---
title : HackerRank-AdvancedJoin-Placements

tags:
    - sql
categories:
    - sql 
date: '2021-07-22'

---

# Placements


You are given three tables: _Students_, _Friends_ and _Packages._  _Students_ contains two columns: _ID_ and _Name_. _Friends_ contains two columns: _ID_ and _Friend_ID_ (_ID_ of the ONLY best friend). _Packages_ contains two columns: _ID_ and _Salary_ (offered salary in $ thousands per month).

![](https://s3.amazonaws.com/hr-challenge-images/12895/1443820186-2a9b4939a8-1.png) 

Write a query to output the names of those students whose best friends got offered a higher salary than them. Names must be ordered by the salary amount offered to the best friends. It is guaranteed that no two students got same salary offer.

**Sample Input**

![](https://s3.amazonaws.com/hr-challenge-images/12895/1443820079-9bd1e231b1-2_1.png)
  
![](https://s3.amazonaws.com/hr-challenge-images/12895/1443820100-adb691b2f5-2_2.png)

**Sample Output**

```
Samantha
Julia
Scarlet
```

**Explanation**
See the following table:

![](https://s3.amazonaws.com/hr-challenge-images/12895/1443819966-c37c146d27-3.png)

Now,

-   _Samantha's_  best friend got offered a higher salary than her at 11.55
-   _Julia's_  best friend got offered a higher salary than her at 12.12
-   _Scarlet's_  best friend got offered a higher salary than her at 15.2
-   _Ashley's_  best friend did NOT get offered a higher salary than her

The name output, when ordered by the salary offered to their friends, will be:

-   _Samantha_
-   _Julia_
-   _Scarlet_

**My solution**

```sql
SELECT my_name
FROM 
(
    SELECT f.id as friend_id,p.salary as f_salary
    FROM STUDENTS s, FRIENDS f, packages p
    WHERE s.id=f.id and f.friend_id = p.id
) f,
(
    SELECT s.id,s.name as my_name, p.salary as my_salary
    FROM STUDENTS s, packages p
    WHERE s.id=p.id
) my
WHERE my.id=f.friend_id and my_salary < f_salary
ORDER BY f_salary ASC;
```

**Most vote solution**

```sql
select s.name
from students s, friends f, packages p, packages p2
where s.id = f.id and f.friend_id = p2.id and s.id = p.id and p.salary < p2.salary
order by p2.salary;
```

