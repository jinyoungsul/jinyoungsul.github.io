---
title : HackerRank-BasicSelect-Weather Observation Station 6

tags:
    - sql
categories:
    - sql 
date: '2021-06-06'

---

# Weather Observation Station 6


Query the list of  _CITY_  names starting with vowels (i.e.,  `a`,  `e`,  `i`,  `o`, or  `u`) from  **STATION**. Your result  _cannot_  contain duplicates.

The  **STATION**  table is described as follows:
![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

**방법1**  정규표현식 이용
```sql
SELECT DISTINCT(CITY)
FROM STATION
WHERE REGEXP_LIKE(CITY, '^[A,E,I,O,U]');
```
**방법2**  LIKE 이용
```sql
SELECT DISTINCT(CITY)
FROM STATION
WHERE (CITY like 'A%' or CITY like 'E%' or CITY like 'I%' or CITY like 'O%' or CITY like 'U%');
```

![](https://i.imgur.com/8emEN2O.png)

