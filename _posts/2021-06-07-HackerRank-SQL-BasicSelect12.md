# Weather Observation Station 7

Query the list of  _CITY_  names ending with vowels (a, e, i, o, u) from  **STATION**. Your result  _cannot_  contain duplicates.

The  **STATION**  table is described as follows:
![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

**방법1**  정규표현식 이용
```sql
SELECT DISTINCT(CITY)
FROM STATION
WHERE REGEXP_LIKE(CITY, '[a-zA-Z]*[a|e|i|o|u]$');
```
**방법2**  LIKE 이용
```sql
SELECT DISTINCT(CITY)
FROM STATION
WHERE CITY LIKE '% %a' or CITY LIKE '% %e' or CITY LIKE '% %e' or CITY LIKE '% %i' or CITY LIKE '% %u' or CITY LIKE '%a' or CITY LIKE '%e' or CITY LIKE '%i' or CITY LIKE '%o' or CITY LIKE '%u';
```

![](https://i.imgur.com/EGr2JnJ.png)

