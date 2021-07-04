# New Companies

Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy:

![](https://s3.amazonaws.com/hr-challenge-images/19505/1458531031-249df3ae87-ScreenShot2016-03-21at8.59.56AM.png)

Given the table schemas below, write a query to print the  _company_code_,  _founder_  name, total number of  _lead_  managers, total number of  _senior_  managers, total number of  _managers_, and total number of  _employees_. Order your output by ascending  _company_code_.

**Note:**

-   The tables may contain duplicate records.
-   The  _company_code_  is string, so the sorting should not be  **numeric**. For example, if the  _company_codes_  are  _C_1_,  _C_2_, and  _C_10_, then the ascending  _company_codes_  will be  _C_1_,  _C_10_, and  _C_2_.

**Input Format**

The following tables contain company data:

-   _Company:_  The  _company_code_  is the code of the company and  _founder_  is the founder of the company.
![](https://s3.amazonaws.com/hr-challenge-images/19505/1458531125-deb0a57ae1-ScreenShot2016-03-21at8.50.04AM.png)

- _Lead_Manager:_ The _lead_manager_code_ is the code of the lead manager, and the _company_code_ is the code of the working company.
![](https://s3.amazonaws.com/hr-challenge-images/19505/1458534960-2c6d764e3c-ScreenShot2016-03-21at8.50.12AM.png)

- _Senior_Manager:_ The _senior_manager_code_ is the code of the senior manager, the _lead_manager_code_ is the code of its lead manager, and the _company_code_ is the code of the working company.
![](https://s3.amazonaws.com/hr-challenge-images/19505/1458534973-6548194998-ScreenShot2016-03-21at8.50.21AM.png)

- _Manager:_ The _manager_code_ is the code of the manager, the _senior_manager_code_ is the code of its senior manager, the _lead_manager_code_ is the code of its lead manager, and the _company_code_ is the code of the working company.
![](https://s3.amazonaws.com/hr-challenge-images/19505/1458534988-7fc0af46ce-ScreenShot2016-03-21at8.50.29AM.png)

- _Employee:_ The _employee_code_ is the code of the employee, the _manager_code_ is the code of its manager, the _senior_manager_code_ is the code of its senior manager, the _lead_manager_code_ is the code of its lead manager, and the _company_code_ is the code of the working company.
![](https://s3.amazonaws.com/hr-challenge-images/19505/1458535002-d47f63cbb4-ScreenShot2016-03-21at8.50.41AM.png)

**Sample Input**
_Company_ Table:
![](https://s3.amazonaws.com/hr-challenge-images/19505/1458535049-2a207c44b3-ScreenShot2016-03-21at8.50.52AM.png)
_Lead_Manager_ Table:
![](https://s3.amazonaws.com/hr-challenge-images/19505/1458535073-919107f639-ScreenShot2016-03-21at8.51.03AM.png)
_Senior_Manager_ Table:
![](https://s3.amazonaws.com/hr-challenge-images/19505/1458535111-b1c48335b3-ScreenShot2016-03-21at8.51.15AM.png)
_Manager_ Table:
![](https://s3.amazonaws.com/hr-challenge-images/19505/1458535122-888f4bf340-ScreenShot2016-03-21at8.51.26AM.png)
_Employee_ Table:
![](https://s3.amazonaws.com/hr-challenge-images/19505/1458535134-878767e0d9-ScreenShot2016-03-21at8.51.52AM.png)

**Sample Output**

```
C1 Monika 1 2 1 2
C2 Samantha 1 1 2 2
```

**Explanation**
In company  _C1_, the only lead manager is  _LM1_. There are two senior managers,  _SM1_  and  _SM2_, under  _LM1_. There is one manager,  _M1_, under senior manager  _SM1_. There are two employees,  _E1_  and  _E2_, under manager  _M1_.
In company  _C2_, the only lead manager is  _LM2_. There is one senior manager,  _SM3_, under  _LM2_. There are two managers,  _M2_  and  _M3_, under senior manager  _SM3_. There is one employee,  _E3_, under manager  _M2_, and another employee,  _E4_, under manager,  _M3_.

**My solution**
```sql
SELECT max(c.company_code),max(c.founder),count(distinct e.lead_manager_code), count(distinct e.senior_manager_code), count(distinct e.manager_code),count(distinct e.employee_code)
FROM Company c, Employee e
WHERE c.company_code = e.company_code
GROUP BY e.lead_manager_code
ORDER BY max(c.company_code);
```

![](https://i.imgur.com/7O62pTS.png)


