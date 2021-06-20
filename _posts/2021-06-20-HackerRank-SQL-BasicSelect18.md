---
title : HackerRank-BasicSelect-Higher Than 75 Marks - substr, length

tags:
    - sql
categories:
    - sql 
date: '2021-06-20'

---

# Higher Than 75 Marks - substr, length

Query the _Name_ of any student in **STUDENTS** who scored higher than _Marks_. Order your output by the _last three characters_ of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending _ID_.

**Input Format**

![](https://s3.amazonaws.com/hr-challenge-images/12896/1443815243-94b941f556-1.png)

The **STUDENTS** table is described as follows: The _Name_ column only contains uppercase (`A`-`Z`) and lowercase (`a`-`z`) letters.

**Sample Input**

![](https://s3.amazonaws.com/hr-challenge-images/12896/1443815209-cf4b260993-2.png)

**Sample Output**

```
Ashley
Julia
Belvet
```

**Explanation**

Only Ashley, Julia, and Belvet have  _Marks_  >  . If you look at the last three characters of each of their names, there are no duplicates and 'ley' < 'lia' < 'vet'.

```sql
SELECT NAME
FROM STUDENTS
WHERE MARKS > 75
ORDER BY SUBSTR(NAME, LENGTH(NAME)-2, 3) ASC, ID ASC;
```

![](https://i.imgur.com/ZFdTLF3.png)


