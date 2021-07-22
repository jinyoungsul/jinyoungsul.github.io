# Symmetric Pairs

You are given a table,  _Functions_, containing two columns:  _X_ and  _Y_.

![](https://s3.amazonaws.com/hr-challenge-images/12892/1443818798-51909e977d-1.png)

Two pairs  _(X1, Y1)_  and  _(X2, Y2)_  are said to be  _symmetric_  _pairs_  if _X1  = Y2_  and  _X2  = Y1_.

Write a query to output all such  _symmetric_  _pairs_  in ascending order by the value of  _X_. List the rows such that  _X1  ≤ Y1_.

**Sample Input**

![](https://s3.amazonaws.com/hr-challenge-images/12892/1443818693-b384c24e35-2.png)

**Sample Output**

```
20 20
20 21
22 23
```

**Most vote solution**

```sql
SELECT f1.X,f1.Y
FROM Functions f1, Functions f2
WHERE f1.X=f2.Y AND f1.Y=f2.X
GROUP BY f1.X,f1.Y
HAVING COUNT(f1.X)>1 OR f1.X<f1.Y
ORDER BY f1.X;
```
