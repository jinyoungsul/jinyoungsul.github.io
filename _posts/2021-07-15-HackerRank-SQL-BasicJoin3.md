---
title : HackerRank-BasicJoin-Average Population of Each Continent

tags:
    - sql
categories:
    - sql 
date: '2021-07-15'

---

# Average Population of Each Continent

Given the  **CITY**  and  **COUNTRY**  tables, query the names of all the continents (_COUNTRY.Continent_) and their respective average city populations (_CITY.Population_) rounded  _down_  to the nearest integer.

**Note:**  _CITY.CountryCode_  and  _COUNTRY.Code_  are matching key columns.

**Input Format**

The  **CITY**  and  **COUNTRY**  tables are described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

![](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg)

**My solution **
```sql
SELECT MAX(CONTINENT), FLOOR(AVG(CITY.POPULATION))
FROM CITY, COUNTRY
WHERE CITY.COUNTRYCODE = COUNTRY.CODE
GROUP BY COUNTRY.CONTINENT;
```




