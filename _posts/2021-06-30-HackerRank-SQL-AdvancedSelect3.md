# Occupations - pivot, row_number


[Pivot](https://en.wikipedia.org/wiki/Pivot_table)  the  _Occupation_  column in  **OCCUPATIONS**  so that each  _Name_  is sorted alphabetically and displayed underneath its corresponding  _Occupation_. The output column headers should be  _Doctor_,  _Professor_,  _Singer_, and  _Actor_, respectively.

**Note:**  Print  **NULL**  when there are no more names corresponding to an occupation.

**Input Format**

The  **OCCUPATIONS**  table is described as follows:

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
Jenny    Ashley     Meera  Jane
Samantha Christeen  Priya  Julia
NULL     Ketty      NULL   Maria
```

**Explanation**

The first column is an alphabetically ordered list of Doctor names.  
The second column is an alphabetically ordered list of Professor names.  
The third column is an alphabetically ordered list of Singer names.  
The fourth column is an alphabetically ordered list of Actor names.  
The empty cell data for columns with less than the maximum number of names per occupation (in this case, the Professor and Actor columns) are filled with **NULL** values.

```sql
SELECT Doctor, Professor, Singer, Actor
FROM
(
SELECT ROW_NUMBER() OVER (PARTITION BY OCCUPATION ORDER BY NAME) AS RowNumber,NAME, OCCUPATION
FROM OCCUPATIONS
)
PIVOT
(
MAX(NAME)
FOR OCCUPATION IN ('Doctor' as Doctor,'Professor' AS Professor,'Singer' AS Singer,'Actor' AS Actor)
)
ORDER BY RowNumber ASC;
```

![](https://i.imgur.com/xCvIOik.png)


