# Weather Observation Station 18


Consider **P1(a,b)** and **P2(c,d)** to be two points on a  _2D_  plane.

-   **a** happens to equal the minimum value in  _Northern Latitude_  (_LAT_N_  in  **STATION**).
-   **b** happens to equal the minimum value in  _Western Longitude_  (_LONG_W_  in  **STATION**).
-   **c** happens to equal the maximum value in  _Northern Latitude_  (_LAT_N_  in  **STATION**).
-   **d** happens to equal the maximum value in  _Western Longitude_  (_LONG_W_  in  **STATION**).

Query the  [Manhattan Distance](https://xlinux.nist.gov/dads/HTML/manhattanDistance.html)  between points **P1** and **P2** and round it to a scale of  decimal places.

**Input Format**

The  **STATION**  table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

**My solution **
```sql
SELECT ROUND(ABS(MAX(LAT_N) - MIN(LAT_N)) + ABS(MAX(LONG_W) - MIN(LONG_W)),4)
FROM STATION;
```




