# Top Competitors


Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective  _hacker_id_  and  _name_  of hackers who achieved full scores for  _more than one_  challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending  _hacker_id_.

----------

**Input Format**

The following tables contain contest data:

-   _Hackers:_  The  _hacker_id_  is the id of the hacker, and  _name_  is the name of the hacker.  
![](https://s3.amazonaws.com/hr-challenge-images/19504/1458526776-67667350b4-ScreenShot2016-03-21at7.45.59AM.png)
    
-   _Difficulty:_  The  _difficult_level_  is the level of difficulty of the challenge, and  _score_  is the score of the challenge for the difficulty level.  ![](https://s3.amazonaws.com/hr-challenge-images/19504/1458526915-57eb75d9a2-ScreenShot2016-03-21at7.46.09AM.png)
    
-   _Challenges:_  The  _challenge_id_  is the id of the challenge, the  _hacker_id_  is the id of the hacker who created the challenge, and  _difficulty_level_  is the level of difficulty of the challenge.  
![](https://s3.amazonaws.com/hr-challenge-images/19504/1458527032-f9ca650442-ScreenShot2016-03-21at7.46.17AM.png)
    
-   _Submissions:_  The  _submission_id_  is the id of the submission,  _hacker_id_  is the id of the hacker who made the submission,  _challenge_id_  is the id of the challenge that the submission belongs to, and  _score_  is the score of the submission.  
![](https://s3.amazonaws.com/hr-challenge-images/19504/1458527077-298f8e922a-ScreenShot2016-03-21at7.46.29AM.png)
    

----------

**Sample Input**

_Hackers_  Table:  
![](https://s3.amazonaws.com/hr-challenge-images/19504/1458527241-6922b4ad87-ScreenShot2016-03-21at7.47.02AM.png)  

_Difficulty_  Table:  
![](https://s3.amazonaws.com/hr-challenge-images/19504/1458527265-7ad6852a13-ScreenShot2016-03-21at7.46.50AM.png)  

_Challenges_  Table:  
![](https://s3.amazonaws.com/hr-challenge-images/19504/1458527285-01e95eb6ec-ScreenShot2016-03-21at7.46.40AM.png)  

_Submissions_  Table:  
![](https://s3.amazonaws.com/hr-challenge-images/19504/1458527812-479a74b99f-ScreenShot2016-03-21at8.06.05AM.png)

**Sample Output**

```
90411 Joe
```

**Explanation**

Hacker  _86870_  got a score of  _30_  for challenge  _71055_  with a difficulty level of  _2_, so  _86870_  earned a full score for this challenge.

Hacker  _90411_  got a score of  _30_  for challenge  _71055_  with a difficulty level of  _2_, so  _90411_  earned a full score for this challenge.

Hacker  _90411_  got a score of  _100_  for challenge  _66730_  with a difficulty level of  _6_, so  _90411_  earned a full score for this challenge.

Only hacker  _90411_  managed to earn a full score for more than one challenge, so we print the their  _hacker_id_  and  _name_  as 2 space-separated values.

**My solution**

```sql
SELECT h.hacker_id, h.name
FROM submissions s, challenges c, difficulty d, hackers h
WHERE s.challenge_id=c.challenge_id and s.hacker_id=h.hacker_id and
c.difficulty_level=d.difficulty_level  and s.score=d.score
GROUP BY h.hacker_id, h.name
HAVING COUNT(h.hacker_id) > 1
ORDER BY COUNT(h.hacker_id) DESC, h.hacker_id ASC;
```


