# The PADS



Generate the following two result sets:

1.  Query an  _alphabetically ordered_  list of all names in  **OCCUPATIONS**, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example:  `An ActorName(A)`,  `A DoctorName(D)`,  `A ProfessorName(P)`, and  `A SingerName(S)`.

2. Query the number of ocurrences of each occupation in **OCCUPATIONS**. Sort the occurrences in _ascending order_, and output them in the following format:

```
There are a total of [occupation_count] [occupation]s.
```
where `[occupation_count]` is the number of occurrences of an occupation in **OCCUPATIONS** and `[occupation]` is the _lowercase_ occupation name. If more than one _Occupation_ has the same `[occupation_count]`, they should be ordered alphabetically.

**Note:** There will be at least two entries in the table for each type of occupation.

**Input Format**

The  **OCCUPATIONS**  table is described as follows:


![](https://s3.amazonaws.com/hr-challenge-images/12889/1443816414-2a465532e7-1.png)

_Occupation_  will only contain one of the following values:  **Doctor**,  **Professor**,  **Singer**  or  **Actor**.

**Sample Input**

An  **OCCUPATIONS**  table that contains the following records:

![](https://s3.amazonaws.com/hr-challenge-images/12889/1443816608-0b4d01d157-2.png)

**Sample Output**

```
Ashely(P)
Christeen(P)
Jane(A)
Jenny(D)
Julia(A)
Ketty(P)
Maria(A)
Meera(S)
Priya(S)
Samantha(D)
There are a total of 2 doctors.
There are a total of 2 singers.
There are a total of 3 actors.
There are a total of 3 professors.
```

**Explanation**

The results of the first query are formatted to the problem description's specifications.  
The results of the second query are ascendingly ordered first by number of names corresponding to each profession, and then alphabetically by profession.




```sql
SELECT NAME || '(' || SUBSTR(OCCUPATION,1,1) || ')'
FROM OCCUPATIONS
ORDER BY NAME ASC;

SELECT 'There are a total of ' || count(OCCUPATION) || ' ' || lower(OCCUPATION) ||'s.'
FROM OCCUPATIONS
GROUP BY(OCCUPATION)
ORDER BY count(OCCUPATION) ASC, OCCUPATION ASC;
```

![](https://i.imgur.com/48q2TD6.png)


