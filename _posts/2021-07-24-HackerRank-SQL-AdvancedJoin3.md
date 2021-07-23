# Interviews

Samantha interviews many candidates from different colleges using coding challenges and contests. Write a query to print the  _contest_id_,  _hacker_id_,  _name_, and the sums of  _total_submissions_,  _total_accepted_submissions_,  _total_views_, and  _total_unique_views_  for each contest sorted by  _contest_id_. Exclude the contest from the result if all four sums are 0 .

**Note:**  A specific contest can be used to screen candidates at more than one college, but each college only holds 1 screening contest.

----------

**Input Format**

The following tables hold interview data:

-   _Contests:_  The  _contest_id_  is the id of the contest,  _hacker_id_  is the id of the hacker who created the contest, and  _name_  is the name of the hacker. 
 ![](https://s3.amazonaws.com/hr-challenge-images/19596/1458517426-e017c3460e-ScreenShot2016-03-21at4.57.47AM.png)
    
-   _Colleges:_  The  _college_id_  is the id of the college, and  _contest_id_  is the id of the contest that Samantha used to screen the candidates. 
 ![](https://s3.amazonaws.com/hr-challenge-images/19596/1458517503-fd4aa63111-ScreenShot2016-03-21at4.57.56AM.png)
    
-   _Challenges:_  The  _challenge_id_  is the id of the challenge that belongs to one of the contests whose contest_id Samantha forgot, and  _college_id_  is the id of the college where the challenge was given to candidates. 
 ![](https://s3.amazonaws.com/hr-challenge-images/19596/1458517661-a642f750ce-ScreenShot2016-03-21at4.58.04AM.png)
    
-   _View_Stats:_  The  _challenge_id_  is the id of the challenge,  _total_views_  is the number of times the challenge was viewed by candidates, and  _total_unique_views_  is the number of times the challenge was viewed by unique candidates.
  ![](https://s3.amazonaws.com/hr-challenge-images/19596/1458517983-b4302286a8-ScreenShot2016-03-21at4.58.15AM.png)
    
-   _Submission_Stats:_  The  _challenge_id_  is the id of the challenge,  _total_submissions_  is the number of submissions for the challenge, and  _total_accepted_submission_  is the number of submissions that achieved full scores.
![](https://s3.amazonaws.com/hr-challenge-images/19596/1458518090-80983c916a-ScreenShot2016-03-21at4.58.27AM.png)
    
----------

**Sample Input**

_Contests_  Table:
  ![](https://s3.amazonaws.com/hr-challenge-images/19596/1458519044-d788f8a6ee-ScreenShot2016-03-21at4.58.39AM.png)  

_Colleges_  Table:
  ![](https://s3.amazonaws.com/hr-challenge-images/19596/1458519098-912836d6ac-ScreenShot2016-03-21at4.59.22AM.png)  

_Challenges_  Table:
    ![](https://s3.amazonaws.com/hr-challenge-images/19596/1458519120-c531743caf-ScreenShot2016-03-21at4.59.32AM.png)  

_View_Stats_  Table:
  ![](https://s3.amazonaws.com/hr-challenge-images/19596/1458519152-107a67866b-ScreenShot2016-03-21at4.59.43AM.png)  

_Submission_Stats_  Table:
  ![](https://s3.amazonaws.com/hr-challenge-images/19596/1458519173-091aba871a-ScreenShot2016-03-21at4.59.55AM.png)

**Sample Output**

```
66406 17973 Rose 111 39 156 56
66556 79153 Angela 0 0 11 10
94828 80275 Frank 150 38 41 15
```

**Explanation**

The contest 66406 is used in the college 11219 . In this college 11219 , challenges 18765 and 47127 are asked, so from the  _view_  and  _submission_  stats:

-   Sum of total submissions = 27 + 56 + 28 = 111
    
-   Sum of total accepted submissions = 10 + 18 + 11 = 39
    
-   Sum of total views = 43 + 72 + 26 + 15 = 156
    
-   Sum of total unique views = 10 + 13 + 19 + 14 = 56
    

Similarly, we can find the sums for contests 66556 and 94828 .

**My solution**

```sql
SELECT CONTESTS.contest_id, CONTESTS.hacker_id,CONTESTS.name,sum(NVL(ts,0)),sum(NVL(tas,0)),sum(NVL(tv,0)),sum(NVL(tuv,0))
FROM CONTESTS 
join COLLEGES on CONTESTS.contest_id = COLLEGES.contest_id
join CHALLENGES on COLLEGES.college_id = CHALLENGES.college_id
LEFT JOIN (SELECT challenge_id,sum(total_views) as tv, sum(total_unique_views) as tuv
           FROM VIEW_STATS
           GROUP BY challenge_id
           ) vs on CHALLENGES.challenge_id = vs.challenge_id
LEFT JOIN  (SELECT challenge_id,sum(total_submissions) as ts, sum(total_accepted_submissions) as tas
            FROM SUBMISSION_STATS
            GROUP BY challenge_id
            ) ss on CHALLENGES.challenge_id = ss.challenge_id
GROUP BY CONTESTS.contest_id,CONTESTS.hacker_id,CONTESTS.name
HAVING sum(NVL(ts,0))+sum(NVL(tas,0))+sum(NVL(tv,0))+sum(NVL(tuv,0)) > 0
ORDER BY CONTESTS.contest_id;
```
