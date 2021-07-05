# Revising Aggregations - Averages


Query the average population of all cities in **CITY** where _District_ is **California**.

**Input Format**
The **CITY** table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

**My solution**
```sql
SELECT AVG(population)
FROM CITY
WHERE DISTRICT = 'California';
```

![](https://i.imgur.com/m3VkDp7.png)


