# SQL 50 - LeetCode
Solutions for [SQL 50 Study Plan](https://leetcode.com/studyplan/top-sql-50/) on LeetCode

---
## SELECT

[1 - Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/)
```sql
SELECT product_id
FROM products
WHERE low_fats = 'Y' AND recyclable = 'Y'
```

[584 - Find Customer Referee](https://leetcode.com/problems/find-customer-referee)
```sql
SELECT name
FROM customer
WHERE referee_id != 2 OR referee_id IS NULL
```

[595 - Big Countries](https://leetcode.com/problems/big-countries/)
```sql
SELECT name, population,  area
FROM world
WHERE area >= 3000000 OR population >= 25000000
```

[1148 - Article Views I](https://leetcode.com/problems/article-views-i)
```sql
SELECT DISTINCT viewer_id AS id 
FROM views 
WHERE author_id = viewer_id
```

[1683 - Invalid Tweets](https://leetcode.com/problems/invalid-tweets/)
```sql
SELECT tweet_id
FROM tweets
WHERE LENGTH(content) > 15
```
## Basic Joins
[1378 - Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier)
```sql
SELECT EmployeeUNI.unique_id, employees.name
FROM employees 
    LEFT JOIN EmployeeUNI ON employees.id = EmployeeUNI.id
```

[1068 - Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/)
```sql
SELECT product_name, year, price
FROM sales
    LEFT JOIN product ON sales.product_id = product.product_id
```

[1581 - Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/)
```sql
SELECT customer_id, COUNT(*) AS count_no_trans
FROM visits
WHERE visit_id NOT IN (SELECT visit_id FROM transactions)
GROUP BY customer_id
ORDER BY count_no_trans 
```

[197 - Rising Temperature](https://leetcode.com/problems/rising-temperature/) 
```sql
SELECT today.id
FROM weather today
    LEFT JOIN weather yesterday ON today.recordDate = yesterday.recordDate + INTERVAL '1' DAY
WHERE today.temperature > yesterday.temperature
```

[1661 - Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/)
```sql
WITH starts AS(
    SELECT *
    FROM activity
    WHERE activity_type = 'start'
),
ends AS(
    SELECT *
    FROM activity
    WHERE activity_type = 'end'
)
SELECT starts.machine_id,
    ROUND(AVG(ends.timestamp-starts.timestamp)::DECIMAL,3) AS processing_time
FROM starts
    LEFT JOIN ends ON starts.machine_id = ends.machine_id 
        AND starts.process_id = ends.process_id
GROUP BY starts.machine_id
```

[577 - Employee Bonus](https://leetcode.com/problems/employee-bonus/solutions/)
```sql
SELECT name, bonus
FROM employee e
    LEFT JOIN bonus b ON e.empid = b.empid
WHERE b.bonus < 1000
    OR b.bonus IS NULL
```

[1280 - Students and Examinations](https://leetcode.com/problems/students-and-examinations/)
```sql
-- Write your PostgreSQL query statement below
SELECT stu.student_id, student_name, sub.subject_name, COUNT(e.subject_name) AS attended_exams
FROM students stu CROSS JOIN Subjects sub
  LEFT JOIN Examinations e ON e.student_id = stu.student_id AND e.subject_name = sub.subject_name
GROUP BY stu.student_id, student_name, sub.subject_name
ORDER BY stu.student_id, sub.subject_name
```
[570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports)
```sql
SELECT name
FROM employee 
WHERE id IN (SELECT managerid FROM employee GROUP BY managerid HAVING COUNT(*) >= 5)
```

[1934. Confirmation Rate](https://leetcode.com/problems/confirmation-rate/)
```sql
SELECT user_id,
  ROUND(AVG(CASE WHEN action = 'confirmed' THEN 1 ELSE 0 END)::DECIMAL,2) AS confirmation_rate
FROM Signups
    LEFT JOIN Confirmations USING (user_id)
GROUP BY user_id
```
## Basic Aggregate Functions

[620. Not Boring Movies](https://leetcode.com/problems/not-boring-movies)
```sql
SELECT *
FROM cinema
WHERE id % 2 = 1 --id % 2 <> 0
    AND description <> 'boring'
ORDER BY rating DESC
```

[1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/)
```sql
SELECT p.product_id,
    IFNULL(ROUND(SUM(units * price) / SUM(units)*1.0,2),0) AS average_price
FROM Prices p
    LEFT JOIN UnitsSold u ON p.product_id = u.product_id
        AND purchase_date BETWEEN start_date AND end_date
GROUP BY p.product_id
```

[1075. Project Employees I](https://leetcode.com/problems/project-employees-i)
```sql
SELECT project_id, ROUND(AVG(experience_years),2) AS average_years
FROM Project p
    LEFT JOIN Employee e USING (employee_id)
GROUP BY project_id
```

[1633. Percentage of Users Attended a Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest)
```sql

```

[1211 Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage)
```sql

```

[1193. Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/)
```sql

```

[1174. Immediate Food Delivery II](https://leetcode.com/problems/immediate-food-delivery-ii/)
```sql

```

[550. Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/)
```sql

```
## Sorting and Grouping

[2356. Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher)
```sql

```

[1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/)
```sql

```

[1070. Product Sales Analysis III
](https://leetcode.com/problems/product-sales-analysis-iii/)
```sql

```

[596. Classes More Than 5 Students](https://leetcode.com/problems/classes-more-than-5-students/)
```sql

```

[1729. Find Followers Count](https://leetcode.com/problems/find-followers-count/)
```sql

```

[619. Biggest Single Number](https://leetcode.com/problems/biggest-single-number/)
```sql

```

[1045. Customers Who Bought All Products](https://leetcode.com/problems/customers-who-bought-all-products/)
```sql

```
## Advanced Select and Joins
[1731. The Number of Employees Which Report to Each Employee
](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/)

```sql

```
[1789. Primary Department for Each Employee
](https://leetcode.com/problems/primary-department-for-each-employee/?envType=study-plan-v2&envId=top-sql-50)
```sql

```

[610. Triangle Judgement](https://leetcode.com/problems/triangle-judgement/)

```sql

```

[180. Consecutive Numbers
](https://leetcode.com/problems/consecutive-numbers/)
```sql

```

[1164. Product Price at a Given Date](https://leetcode.com/problems/product-price-at-a-given-date)
```sql

```

## Subqueries
[1978. Employees Whose Manager Left the Company](https://leetcode.com/problems/employees-whose-manager-left-the-company)
```sql

```

[185. Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries)
```sql

```

## Advanced String Functions / Regex / Clause
[1667. Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table)
```sql

```

[1527. Patients With a Condition](https://leetcode.com/problems/patients-with-a-condition)
```sql

```

[196. Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails)
```sql

```

[176. Second Highest Salary](https://leetcode.com/problems/second-highest-salary)
```sql

```
 
[1517. Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails)
```sql

```

[1204. Last Person to Fit in the Bus](https://leetcode.com/problems/last-person-to-fit-in-the-bus/)
```sql

```

[1907. Count Salary Categories](https://leetcode.com/problems/count-salary-categories/)
```sql

```
[626. Exchange Seats](https://leetcode.com/problems/exchange-seats/)
```sql

```

[1327. List the Products Ordered in a Period](https://leetcode.com/problems/list-the-products-ordered-in-a-period/)
```sql

```

[1484. Group Sold Products By The Date](https://leetcode.com/problems/group-sold-products-by-the-date/)
```sql

```

[1341. Movie Rating](https://leetcode.com/problems/movie-rating/)

```sql

```

[1321. Restaurant Growth](https://leetcode.com/problems/restaurant-growth/)
```sql

```


[602. Friend Requests II: Who Has the Most Friends](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends)

```sql

```

[585. Investments in 2016](https://leetcode.com/problems/investments-in-2016)
```sql


```
