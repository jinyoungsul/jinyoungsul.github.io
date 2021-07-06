﻿# Japan Population


Query the sum of the populations for all Japanese cities in **CITY**. The _COUNTRYCODE_ for Japan is **JPN**.

**Input Format**
The **CITY** table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

**My solution**
```sql
SELECT SUM(POPULATION)
FROM CITY
WHERE COUNTRYCODE = 'JPN';
```

![](https://i.imgur.com/cGpqQcQ.png)


