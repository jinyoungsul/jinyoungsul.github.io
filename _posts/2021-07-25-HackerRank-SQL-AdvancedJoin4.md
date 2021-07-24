
# SQL Project Planning

You are given a table,  _Projects_, containing three columns:  _Task_ID_,  _Start_Date_  and  _End_Date_. It is guaranteed that the difference between the  _End_Date_  and the  _Start_Date_  is equal to  _1_  day for each row in the table.

![](https://s3.amazonaws.com/hr-challenge-images/12894/1443819551-639948acc0-1.png)

If the  _End_Date_  of the tasks are consecutive, then they are part of the same project. Samantha is interested in finding the total number of different projects completed.

Write a query to output the start and end dates of projects listed by the number of days it took to complete the project in ascending order. If there is more than one project that have the same number of completion days, then order by the start date of the project.

**Sample Input**

![](https://s3.amazonaws.com/hr-challenge-images/12894/1443819440-1c40e943a1-2.png)

**Sample Output**

```
2015-10-28 2015-10-29
2015-10-30 2015-10-31
2015-10-13 2015-10-15
2015-10-01 2015-10-04

```

  
**Explanation**

The example describes following  _four_  projects:

-   _Project 1_: Tasks  _1_,  _2_  and  _3_  are completed on consecutive days, so these are part of the project. Thus start date of project is  _2015-10-01_  and end date is  _2015-10-04_, so it took  _3 days_  to complete the project.
-   _Project 2_: Tasks  _4_ and _5_ are completed on consecutive days, so these are part of the project. Thus, the start date of project is _2015-10-13_ and end date is _2015-10-15_, so it took _2 days_ to complete the project.
-   _Project 3_: Only task  _6_ is part of the project. Thus, the start date of project is _2015-10-28_ and end date is _2015-10-29_, so it took _1 day_ to complete the project.
-   _Project 4_: Only task _7_ is part of the project. Thus, the start date of project is _2015-10-30_ and end date is _2015-10-31_, so it took _1 day_ to complete the project.

관련된 함수[Tabibitosan Method](https://community.oracle.com/tech/developers/discussion/4417554/pl-sql-101-grouping-sequence-ranges-tabibitosan-method)

**Most Vote solution**

```sql
SELECT MIN(Start_Date), MAX(End_Date)
FROM
(
    SELECT Start_Date, End_Date, Start_Date - ROW_NUMBER() OVER(ORDER BY Start_Date) as rnk
    FROM Projects
)
GROUP BY rnk
ORDER BY COUNT(*), MIN(Start_Date);
```
