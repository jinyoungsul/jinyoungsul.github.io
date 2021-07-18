# Ollivander's Inventory



Harry Potter and his friends are at Ollivander's with Ron, finally replacing Charlie's old broken wand.

Hermione decides the best way to choose is by determining the minimum number of gold galleons needed to buy each  _non-evil_  wand of high power and age. Write a query to print the  _id_,  _age_,  _coins_needed_, and  _power_  of the wands that Ron's interested in, sorted in order of descending  _power_. If more than one wand has same power, sort the result in order of descending  _age_.

**Input Format**

The following tables contain data on the wands in Ollivander's inventory:

-   _Wands:_  The  _id_  is the id of the wand,  _code_  is the code of the wand,  _coins_needed_  is the total number of gold galleons needed to buy the wand, and  _power_  denotes the quality of the wand (the higher the power, the better the wand is).  
![](https://s3.amazonaws.com/hr-challenge-images/19502/1458538092-b2a8163a74-ScreenShot2016-03-08at12.13.39AM.png)
    
-   _Wands_Property:_  The  _code_  is the code of the wand,  _age_  is the age of the wand, and  _is_evil_  denotes whether the wand is good for the dark arts. If the value of  _is_evil_  is  _0_, it means that the wand is not evil. 
![](https://s3.amazonaws.com/hr-challenge-images/19502/1458538221-18c4092b7d-ScreenShot2016-03-08at12.13.53AM.png)


**Sample Input**

_Wands_  Table:  
![](https://s3.amazonaws.com/hr-challenge-images/19502/1458538559-51bf29644e-ScreenShot2016-03-21at10.34.41AM.png)  

_Wands_Property_  Table:  
![](https://s3.amazonaws.com/hr-challenge-images/19502/1458538583-fd514566f9-ScreenShot2016-03-21at10.34.28AM.png)

**Sample Output**

```
9 45 1647 10
12 17 9897 10
1 20 3688 8
15 40 6018 7
19 20 7651 6
11 40 7587 5
10 20 504 5
18 40 3312 3
20 17 5689 3
5 45 6020 2
14 40 5408 1
```

**Explanation**
The data for wands of  _age 45_  (code 1):  
-   The minimum number of galleons needed for wand(age = 45, power = 2) = 6020
-   The minimum number of galleons needed for
wand(age = 45, power = 10) = 1647
![](https://s3.amazonaws.com/hr-challenge-images/19502/1458539700-2f319702ab-ScreenShot2016-03-21at11.23.06AM.png)


The data for wands of  _age 40_  (code 2):  
-   The minimum number of galleons needed for
wand(age = 40, power = 1) = 5408
-   The minimum number of galleons needed for
wand(age = 40, power = 3) = 3312
-   The minimum number of galleons needed for
wand(age = 40, power = 5) = 7587
-   The minimum number of galleons needed for
wand(age = 40, power = 7) = 6018
![](https://s3.amazonaws.com/hr-challenge-images/19502/1458539909-ab79f7ff95-ScreenShot2016-03-21at11.23.14AM.png)



The data for wands of  _age 20_  (code 4):  
-   The minimum number of galleons needed for
wand(age = 20, power = 5) = 504
-   The minimum number of galleons needed for
wand(age = 20, power = 6) = 7651
-   The minimum number of galleons needed for
wand(age = 20, power = 8) = 3688
![](https://s3.amazonaws.com/hr-challenge-images/19502/1458540035-d950b9c900-ScreenShot2016-03-21at11.23.25AM.png)



The data for wands of  _age 17_  (code 5): 
-   The minimum number of galleons needed for
wand(age = 17, power = 3) = 5689
-   The minimum number of galleons needed for
wand(age = 17, power = 10) = 9897
![](https://s3.amazonaws.com/hr-challenge-images/19502/1458540132-79fd7b916b-ScreenShot2016-03-21at11.23.34AM.png)



**My solution**

```sql
SELECT id, age, coins_needed, power
FROM
(
SELECT ROW_NUMBER() OVER(PARTITION BY Wands_property.age, Wands.power ORDER BY Wands.coins_needed) AS rownumber, Wands.id, Wands_property.age, Wands.coins_needed, Wands.power
FROM Wands, Wands_property
WHERE Wands.code = Wands_property.code AND Wands_property.is_evil=0
)
WHERE rownumber=1
ORDER BY power DESC, age DESC;
```


