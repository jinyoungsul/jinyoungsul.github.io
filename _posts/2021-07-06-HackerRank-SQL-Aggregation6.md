# Population Density Difference


Query the difference between the maximum and minimum populations in **CITY**.

**Input Format**
The **CITY** table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

**My solution**
```sql
SELECT MAX(population) - MIN(population)
FROM CITY;
```

![](https://i.imgur.com/uH1vWYP.png)


