# # # Type of Triangle - case when


Write a query identifying the  _type_  of each record in the  **TRIANGLES**  table using its three side lengths. Output one of the following statements for each record in the table:

-   **Equilateral**: It's a triangle with  3sides of equal length.
-   **Isosceles**: It's a triangle with  2sides of equal length.
-   **Scalene**: It's a triangle with  3sides of differing lengths.
-   **Not A Triangle**: The given values of  _A_,  _B_, and  _C_  don't form a triangle.

**Input Format**

The  **TRIANGLES**  table is described as follows:

![](https://s3.amazonaws.com/hr-challenge-images/12887/1443815629-ac2a843fb7-1.png)


Each row in the table denotes the lengths of each of a triangle's three sides.

**Sample Input**

![](https://s3.amazonaws.com/hr-challenge-images/12887/1443815827-cbfc1ca12b-2.png)

**Sample Output**

```
Isosceles
Equilateral
Scalene
Not A Triangle
```

```sql
SELECT CASE WHEN A+B <= C OR B+C <= A OR A+C <= B THEN 'Not A Triangle'
            WHEN A=B AND B=C THEN 'Equilateral'
            WHEN (A=B AND A!=C) OR (B=C AND B!=A) OR (A=C AND A!=B)THEN 'Isosceles'
            WHEN A!=B AND B!=C AND A!=C THEN 'Scalene'
            END
FROM TRIANGLES;
```

![](https://i.imgur.com/EgPE5LS.png)


