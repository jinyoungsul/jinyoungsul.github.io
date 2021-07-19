# Challenges

Julia asked her students to create some coding challenges. Write a query to print the  _hacker_id_,  _name_, and the total number of challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one student created the same number of challenges, then sort the result by  _hacker_id_. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.

**Input Format**

The following tables contain challenge data:

-   _Hackers:_  The  _hacker_id_  is the id of the hacker, and  _name_  is the name of the hacker. 
![](https://s3.amazonaws.com/hr-challenge-images/19506/1458521004-cb4c077dd3-ScreenShot2016-03-21at6.06.54AM.png)
    
-   _Challenges:_  The  _challenge_id_  is the id of the challenge, and  _hacker_id_  is the id of the student who created the challenge.  ![](https://s3.amazonaws.com/hr-challenge-images/19506/1458521079-549341d9ec-ScreenShot2016-03-21at6.07.03AM.png)
    
----------

**Sample Input 0**

_Hackers_  Table: 
 
![](https://s3.amazonaws.com/hr-challenge-images/19506/1458521384-34c6866dae-ScreenShot2016-03-21at6.07.15AM.png)  

_Challenges_  Table: 
 
![](https://s3.amazonaws.com/hr-challenge-images/19506/1458521410-befa8e1cd9-ScreenShot2016-03-21at6.07.25AM.png)

**Sample Output 0**

```
21283 Angela 6
88255 Patrick 5
96196 Lisa 1
```

**Sample Input 1**

_Hackers_  Table: 
 ![](https://s3.amazonaws.com/hr-challenge-images/19506/1458521469-87036deea3-ScreenShot2016-03-21at6.07.48AM.png)  

_Challenges_  Table:
  ![](https://s3.amazonaws.com/hr-challenge-images/19506/1458521490-358215cf0b-ScreenShot2016-03-21at6.07.58AM.png)

**Sample Output 1**

```
12299 Rose 6
34856 Angela 6
79345 Frank 4
80491 Patrick 3
81041 Lisa 1
```

**Explanation**

For  _Sample Case 0_, we can get the following details: 
 
![](https://s3.amazonaws.com/hr-challenge-images/19506/1458521677-fd04c384c0-ScreenShot2016-03-21at6.07.38AM.png)  

Students 5077 and 62743 both created 4 challenges, but the maximum number of challenges created is 6 so these students are excluded from the result.

For  _Sample Case 1_, we can get the following details: 
 
![](https://s3.amazonaws.com/hr-challenge-images/19506/1458521836-24039e7523-ScreenShot2016-03-21at6.08.08AM.png)  

Students 12299 and 34856 both created 6 challenges. Because 6 is the maximum number of challenges created, these students are included in the result.

**My solution**

```sql
SELECT hacker_id, max(name) as max_name, count(hacker_id) as count_id
FROM
(
SELECT row_number() over(partition by h.hacker_id order by h.hacker_id) as rownumber, h.hacker_id, h.name
FROM Hackers h, Challenges c
WHERE h.hacker_id = c.hacker_id
)
GROUP BY hacker_id
HAVING count(hacker_id)=(
    SELECT MAX(cnt)
    FROM (
        SELECT COUNT(hacker_id) as cnt
        FROM Challenges
        GROUP BY hacker_id
    )
)
OR count(hacker_id) in
(
    SELECT cnt
    FROM (
        SELECT COUNT(*) as cnt
        FROM Challenges
        GROUP BY hacker_id
    )
    GROUP BY cnt
    HAVING COUNT(cnt)=1
)
ORDER BY count_id DESC, hacker_id;
```


