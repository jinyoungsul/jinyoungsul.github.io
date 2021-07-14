---
title : HackerRank-BasicJoin-African Cities

tags:
    - sql
categories:
    - sql 
date: '2021-07-14'

---

# African Cities


Given the  **CITY**  and  **COUNTRY**  tables, query the names of all cities where the  _CONTINENT_  is  _'Africa'_.

**Note:**  _CITY.CountryCode_  and  _COUNTRY.Code_  are matching key columns.

**Input Format**
The **CITY** and **COUNTRY** tables are described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

![](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg)

**My solution **
```sql
SELECT NAME
FROM CITY
WHERE COUNTRYCODE IN (SELECT CODE
                     FROM COUNTRY
                     WHERE CONTINENT='Africa');
```




