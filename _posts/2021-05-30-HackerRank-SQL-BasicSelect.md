---
title: HackerRank-BasicSelect-Revising the Select Query II

tags: 
  - sql
categories: 
  - sql
date: '2021-05-30'

---

# Revising the Select Query II 
Query the  **NAME**  field for all American cities in the  **CITY**  table with populations larger than  `120000`. The  _CountryCode_  for America is  `USA`.

The  **CITY**  table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

```sql
SELECT NAME
FROM CITY
WHERE COUNTRYCODE = 'USA' AND POPULATION >= 120000;
```

![](https://i.imgur.com/AN9t0mM.png)

