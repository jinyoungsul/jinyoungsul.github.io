---
title : HackerRank-BasicSelect-Weather Observation Station 12

tags:
    - sql
categories:
    - sql 
date: '2021-06-17'

---

# Weather Observation Station 12


Query the list of  _CITY_  names from  **STATION**  that  _do not start_  with vowels and  _do not end_  with vowels. Your result cannot contain duplicates.

**Input Format**

The  **STATION**  table is described as follows:
![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)


```sql
SELECT DISTINCT CITY
FROM STATION
WHERE REGEXP_LIKE(CITY, '^[^AEIOU]+[a-zA-Z ]*[^aeiou]$');
```

![](https://i.imgur.com/eVt0cB9.png)

