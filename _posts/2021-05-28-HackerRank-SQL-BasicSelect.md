---
title: HackerRank-BasicSelect-Revising the Select Query I
tags: 
  - sql
categories: 
  - sql
date: '2021-05-28'

---

# Revising the Select Query I 
Query all columns for all American cities in CITY with populations larger than 100000 . The CountryCode for America is USA . Input Format The CITY table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

```sql
SELECT *
FROM CITY
WHERE COUNTRYCODE='USA' AND POPULATION >= 100000
```

![](https://i.imgur.com/kForS2R.png)

