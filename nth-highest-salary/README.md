## 177. Nth Highest Salary

### Description

Write a SQL query to get the *n*th highest salary from the `Employee` table.

```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

For example, given the above Employee table, the *n*th highest salary where *n* = 2 is `200`. If there is no *n*th highest salary, then the query should return `null`.

```
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```



### Solution1

```mysql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  RETURN (
      # Write your MySQL query statement below.
      select distinct salary from employee e where N = (select count(distinct salary) from employee where salary >= e.salary)
  );
END
```





### Solution2

```mysql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
SET N = N-1;
  RETURN (
      # Write your MySQL query statement below.
      select IFNULL (
          (select distinct salary from employee order by salary DESC limit N,1)
          ,null)
  );
END
```

### Note

- 可以参考[Problem 176](<https://github.com/orrrz/Leetcode-database-solution/tree/master/second-highest-salary>) second-highest-salary的解法

If you have a better solution, you can star and fork [Leetcode-database-solution](https://github.com/orrrz/Leetcode-database-solution) then create a pull request. Thank you!