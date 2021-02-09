---
layout: post
title: Lab2 SQL Intro
date: 2021-02-09
Author: Hyde
tags: [sample, markdown]
comments: true
toc: true
---

# Geo1006 Lab2: SQL Intro

> First name: Haoyang
> Surname: Dong
> Student number: 5302501
> 
> First name: Maundri
> Surname: Prihanggo
> Student number: 5151279
> 
> First name: Runnan
> Surname: Fu
> Student number: 5213045

##### 1. Give a list (Fname, Minit, Lname) of all male employees with their salaries.

```sql
select Fname, Minit, Lname, salary
from employee
where sex = 'M'
order by salary;
```

 ![image-20201122161829595](C:\Users\Hyde\AppData\Roaming\Typora\typora-user-images\image-20201122161829595.png)



##### 2. Give a list of all different birthdays (month of birth, day of birth) of the employees (Hint: use ‘extract(month from bdate)’ to get the month from the birthdate). Order the list by birthday (month first).

```sql
SELECT DISTINCT EXTRACT (month FROM bdate) AS Month,
EXTRACT (day FROM bdate) AS Day
FROM employee
ORDER BY Month, Day;
```

**![img](https://lh3.googleusercontent.com/CtObKtpgAxRV6_dfYV--bae8GUMVg7SMm6WREichxArWk2veFM8Ip6Wj8mjLncicoDh48P6uvoH6GqljkSRWsCbbPoQX-w67Ko6oQx_OcqIa5YWH3ROLuDdddtFsbypAPbdU7pim)**



##### 3. Give a list of all employees (Lname) who do not have a supervisor in the table EMPLOYEE.

```sql
SELECT lname
FROM employee
WHERE super_ssn IS NULL;
```

**![img](https://lh6.googleusercontent.com/UO9ML7YFRkp1Kls5wRN7PiqR6F03mihTcAT-T2veciGCHmIkNKveh47cxK7ORhsNSwEHEeQ42eiukBlNJV8b_PVaaT37SeJjXSkf4WZHQphgapB0hQW7aUBSzxEpa9sR5TvDV1yF)**



##### 4. Give a list of all employees (Lname, Salary) in the department ‘Research’. Give the list in ascending order of salary.

```sql
SELECT employee.lname, employee.salary
FROM employee, department
WHERE employee.dno = department.dnumber AND department.dname = 'Research'
ORDER BY salary;
```

 <img src="C:\Users\Hyde\AppData\Roaming\Typora\typora-user-images\image-20201123054759874.png" alt="image-20201123054759874" style="zoom:67%;" />



##### 5. Give a list (Fname, Lname, Dname) of all female department managers (N.B. in the PostgreSQL company database the attribute in DEPARTMENT indicating the department manager is called Mgr_ssn).

```sql
SELECT employee.fname, employee.lname, department.dname
FROM employee, department
WHERE department.mgr_ssn = employee.ssn AND employee.sex = 'F';
```

 ![img](https://lh6.googleusercontent.com/2FRvh3RWTjvPnScT7Dm_mTIoOPb_Ao-T6L1M72lbK7XPFuXM1QUjUP-ec2C3tdAPI1u4rWp4WzODvoglNfrP4fFMzZ7ZdIWdx_yDCPWkr5ygb8JiZEAoiY01Q5fblr8UZxulnSwN)



##### 6. Give a list of all employees (Lname) that are supervisors of other employees.

```sql
SELECT DISTINCT SU.lname
FROM employee AS EM, employee AS SU
WHERE EM.super_ssn = SU.ssn;
```

 ![img](https://lh6.googleusercontent.com/M4L3154450zwLNxM9iGBTo-r0dvOvTa1IKTr1QGdjZcmS63jdcMkCRAo6-7vtgYwpLNIcF0Rwfy9T6_kTzlzO4jcGMnExGISh_mjkS1_fJk9rFQBlVvYI9AW41XRQB91BXuRbyww)



##### 7. Give a list of all employees (Lname) that are not supervisors of a department.

```sql
SELECT employee.lname
FROM employee, department
WHERE employee.dno = department.dnumber AND department.mgr_ssn <> employee.ssn;
```

**![img](https://lh4.googleusercontent.com/FN8D-y4wL0264QwhOV1uaNiC3athMCZ9tBSN_2B1SyqUHGVjB1vsUBzugiTBIl3qRU_VAAQxoPmDiVoWLPGMhn0A3l3I8jCJjStDkxJ8IAsD87oo_MRmRQQMTL6RwnjMowuInzro)**



##### 8. Give a list of all names of projects on which at least one employee is working for more than 15 hours a week.

```sql
SELECT DISTINCT Pname
FROM PROJECT JOIN WORKS_ON ON Pnumber = Pno
WHERE Hours > 15;
```

 ![img](https://lh4.googleusercontent.com/vCISMPig7iu_av46gKNsHOGVULiOHpahwo_ffrAWY_0DsWsjF0Rq7dMX6IfNwbhmwVZi11mDZ9LOxF7bRgdAMoYXtGaMjSHjcAZxc6e-OS13dAHCOX4jBJeQc9Ezu0qQeEwyYK8U)



##### 9. Give a list (Lname, Dependent_name) of all employees who have a male spouse in the dependent table.

```sql
SELECT Lname, Dependent_name
FROM EMPLOYEE JOIN DEPENDENT ON Ssn = Essn
WHERE DEPENDENT.Sex = 'M' AND Relationship = 'Spouse';
```

 ![img](https://lh6.googleusercontent.com/vJaRlkxSg9S3kvq7jrGYZ1zXQ4jII_pKbXwd7Qz5NJRE-PrMOc05zVX7dLrsVI1wPDAoUZl4wQFRWIOJGrtndn7qLdcLGWpgtFT02eJYM8_QfwnZirwAntc_FKLJsAJJ_ykcsm9p)



##### 10. Give a list of all employees (Lname) who work in a department that has a location in Houston.

```sql
SELECT Lname
FROM EMPLOYEE JOIN DEPT_LOCATIONS ON Dno = Dnumber
WHERE Dlocation = 'Houston';
```

 ![img](https://lh5.googleusercontent.com/EXW9C7zD5excvAo8WFQQgbhbL_mNkEt_gCqbDJ5NWUt_1wna9IT1bvMVy6iF3n1xtX6kM_ve-AGPwgFeOBUeKtZ0qkzyNX6R_5n55Gy4C9rN37rF978G1ri90Gx8H1fQ1MRRF1qA)



##### 11. Give a list (Dname, Pname, Location) of department names, project names and locations with the property that the department supervises the project and that the department has a location in the place where the project is located.

```sql
SELECT Dname, Pname, Plocation AS Location
FROM (DEPARTMENT NATURAL JOIN DEPT_LOCATIONS) JOIN PROJECT ON Dnumber = Dnum
WHERE Dlocation = Plocation;
```

 ![img](https://lh4.googleusercontent.com/coOgpHNQg4askB9YY9yJ5_FIpO83r8G1_LUO3EXGQPDX_2vUMmFuPzsrUyCVam7VliMn3I__i9m5SWcWsZN57XFLf4QGhWpyaIBzCHc3tat6YsF0_biL1xP4YUGJ4dRrPXGXlpcb)



##### 12. How much does the company spend on salaries each year?

```sql
SELECT SUM(Salary)
FROM EMPLOYEE;
```

 ![img](https://lh6.googleusercontent.com/VMFvphhyFaQ3PJQnSOXVJJSpVeCpilVViu_g7k3DwV_AA6muXQY-Bc7m89H4c_Z1R4poOM7sKg7eBC9DTq1JRBDOucFB3T6lp6R2CHc0xKxKnz0Rt5wZ--jwTc7XGGc3KTGnw_q6)



##### 13. How many different department locations does the company have?

```sql
SELECT COUNT(DISTINCT(Dlocation))
FROM DEPT_LOCATIONS;
```

 ![img](https://lh5.googleusercontent.com/nmrSqTRevFPqsBlajIZyBP0d_fVXdkgcGBVlNfYSkWfQwhknpb_FahozIzrYJxuiVLLkQg_Ai1hR3p9jVS7uatmW4_Z2l3skAu3QhCumJWDxnB4dIsjquMdiHUfRissBeQOZsLxQ)



##### 14. How much time a week is spent on the project Newbenefits?

```sql
SELECT SUM(Hours)
FROM PROJECT JOIN WORKS_ON ON Pnumber = Pno
WHERE Pname = 'Newbenefits';
```

 ![img](https://lh3.googleusercontent.com/_vHL0oSCTBs9mVXwf4F_GxJknAMCR7eAXsU-6BGIn0adB2_6VOxXCezcllw9R05lHuOwgZQfh7eILbq8MT8kJ9pptGFzQWF7_qHDahN1HfPZz1_KG9GqkRi0Eqb1JxlM2cGkpJya)



##### 15. Give a list of all employees ((E)ssn) with the total amount of hours per week that each one spends on projects.

```sql
SELECT essn, SUM(hours)
FROM works_on
GROUP BY essn;
```

 <img src="https://lh6.googleusercontent.com/Vfn6inhLdVDn1i5JqB-615IyiiIUvgCNnTT6ngrAunJVoI0Es0Tn5LOVNCIuXyTMEOmFnF6v9HNy9EhidnNNCk0EkMOwqSmdZhQYYahE-lGzzok0YoMI18rYiiNsF-Kt7bWmCqiJ" alt="img" style="zoom:67%;" />



##### 16. Give the name of each department with the number of locations it has in the table Dept_Locations.

```sql
SELECT dname, COUNT(dlocation)
FROM department NATURAL JOIN dept_locations
GROUP BY dnumber;
```

 <img src="https://lh6.googleusercontent.com/VuHZoQIAr8F5GzwAKh-jY6W-_H3Hy7ZWoBl7kURbNHXbPXNneoReuk-6gIhwThQwI19ouECotdPbYtcERurP3ncRdXq6gCwbFlz2WpM0gIqWxEs6qGHzJ3n0WT0Nfy27MeP1K-PB" alt="img" style="zoom:67%;" />



##### 17. How many employees are actually involved in projects?

```sql
SELECT COUNT ( DISTINCT essn )
FROM works_on
WHERE hours != 0;
```

 <img src="C:\Users\Hyde\AppData\Roaming\Typora\typora-user-images\image-20201123051433315.png" alt="image-20201123051433315" style="zoom:67%;" />



##### 18. Give the name(s) of the department(s) which have the biggest number of locations.

```sql
SELECT MAX(dname)
FROM department NATURAL JOIN dept_locations;
```

 <img src="C:\Users\Hyde\AppData\Roaming\Typora\typora-user-images\image-20201123051931176.png" alt="image-20201123051931176" style="zoom:67%;" />



#####  19. Give the name of the department having the biggest average salary.

```sql
CREATE VIEW avg_salary(dnumber, avg_s) AS
	(SELECT dno, AVG(salary) FROM employee GROUP BY dno);

SELECT dname
FROM department NATURAL JOIN avg_salary
WHERE avg_s = (SELECT MAX(avg_s) FROM avg_salary);
```

 <img src="C:\Users\Hyde\AppData\Roaming\Typora\typora-user-images\image-20201123053247398.png" alt="image-20201123053247398" style="zoom:67%;" />



##### 20. Give from the projects located in Houston with more than one participant, the one (Pname) on which the smallest total amount of hours a week is spent.

```sql
CREATE VIEW sum_works(pnumber, sum_h) AS
	(SELECT pno, SUM(hours) FROM works_on GROUP BY pno);

SELECT pname
FROM project NATURAL JOIN sum_works
WHERE sum_h = (SELECT MIN(sum_h) FROM sum_works);
```

 <img src="C:\Users\Hyde\AppData\Roaming\Typora\typora-user-images\image-20201123054215057.png" alt="image-20201123054215057" style="zoom:67%;" />

