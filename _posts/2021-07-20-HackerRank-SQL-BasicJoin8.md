---
title : HackerRank-BasicJoin-Contest Leaderboard

tags:
    - sql
categories:
    - sql 
date: '2021-07-20'

---

# Contest Leaderboard

You did such a great job helping Julia with her last coding contest challenge that she wants you to work on this one, too!

The total score of a hacker is the sum of their maximum scores for all of the challenges. Write a query to print the  _hacker_id_,  _name_, and total score of the hackers ordered by the descending score. If more than one hacker achieved the same total score, then sort the result by ascending  _hacker_id_. Exclude all hackers with a total score of 0 from your result.

**Input Format**

The following tables contain contest data:

-   _Hackers:_  The  _hacker_id_  is the id of the hacker, and  _name_  is the name of the hacker.
 
 ![](https://s3.amazonaws.com/hr-challenge-images/19503/1458522826-a9ddd28469-ScreenShot2016-03-21at6.40.27AM.png)
    
-   _Submissions:_  The  _submission_id_  is the id of the submission,  _hacker_id_  is the id of the hacker who made the submission,  _challenge_id_  is the id of the challenge for which the submission belongs to, and  _score_  is the score of the submission.
 
 ![](https://s3.amazonaws.com/hr-challenge-images/19503/1458523022-771511df90-ScreenShot2016-03-21at6.40.37AM.png)
    
**Sample Input**

_Hackers_  Table:

  ![](https://s3.amazonaws.com/hr-challenge-images/19503/1458523374-7ecc39010f-ScreenShot2016-03-21at6.51.56AM.png)

_Submissions_  Table:

  ![](https://s3.amazonaws.com/hr-challenge-images/19503/1458523388-0896218137-ScreenShot2016-03-21at6.51.45AM.png)

**Sample Output**

```
4071 Rose 191
74842 Lisa 174
84072 Bonnie 100
4806 Angela 89
26071 Frank 85
80305 Kimberly 67
49438 Patrick 43
```

**Explanation**

Hacker  _4071_  submitted solutions for challenges  _19797_  and  _49593_, so the total score = 95 + max(43, 96) = 191 .

Hacker  _74842_  submitted solutions for challenges  _19797_  and  _63132_, so the total score = max(98, 5) + 76 = 174 .

Hacker  _84072_  submitted solutions for challenges  _49593_  and  _63132_, so the total score 100 + 0 = 100 .

The total scores for hackers  _4806_,  _26071_,  _80305_, and  _49438_  can be similarly calculated.

**My solution**

```sql
SELECT hacker_id, name, sum(score)
FROM
(
SELECT rownumber,name,hacker_id,challenge_id,score
FROM
(
    SELECT ROW_NUMBER() OVER(PARTITION BY s.hacker_id, s.challenge_id order by s.score DESC) as rownumber, h.name,s.hacker_id,s.challenge_id,s.score
    FROM HACKERS h, SUBMISSIONS s
    WHERE h.hacker_id=s.hacker_id
)
WHERE rownumber=1
)
GROUP BY hacker_id,name
HAVING sum(score) > 0
ORDER BY sum(score) DESC, hacker_id;
```

**Most vote solution**

```sql
SELECT h.hacker_id, h.name, sum(score)
FROM hackers h,(SELECT hacker_id, max(score) as score
                FROM submissions
                GROUP BY hacker_id, challenge_id) max_score
WHERE h.hacker_id = max_score.hacker_id
GROUP BY h.hacker_id,h.name
HAVING sum(score) > 0
ORDER BY sum(score) DESC, h.hacker_id;
```

