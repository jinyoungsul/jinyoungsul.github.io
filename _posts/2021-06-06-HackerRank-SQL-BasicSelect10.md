---
title : HackerRank-BasicSelect-Weather Observation Station 5

tags:
    - sql
categories:
    - sql 
date: '2021-06-06'

---

# Weather Observation Station 5


Query the two cities in **STATION** with the shortest and longest _CITY_ names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.  
The **STATION** table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

When ordered alphabetically, the  **CITY**  names are listed as  **ABC, DEF, PQRS,**  and  **WXY**, with lengths 3, 3, 4 and 3. The longest name is  **PQRS**, but there are 3 options for shortest named city. Choose  **ABC**, because it comes first alphabetically.

**Note**  
You can write two separate queries to get the desired output. It need not be a single query.


```sql
SELECT CITY, LENGTH(CITY)
FROM (SELECT CITY, LENGTH(CITY)
      FROM STATION
      ORDER BY LENGTH(CITY) asc, CITY)
WHERE ROWNUM = 1;

SELECT CITY, LENGTH(CITY)
FROM (SELECT CITY, LENGTH(CITY)
      FROM STATION
      ORDER BY LENGTH(CITY) DESC, CITY ASC) 
WHERE ROWNUM = 1;


```

![](https://i.imgur.com/TmujbNk.png)

