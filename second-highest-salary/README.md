## 176.第二高的薪水

### Description

Write a SQL query to get the second highest salary from the `Employee` table.

```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

For example, given the above Employee table, the query should return `200` as the second highest salary. If there is no second highest salary, then the query should return `null`.

```
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
```

### Solution1

```mysql
select MAX(Salary) AS SecondHighestSalary from employee where  Salary < (select MAX(Salary) from employee)
```

### Solution2

```mysql
-- 需要注意的是数据库可能只存在一条记录，需要解决“NULL”的显示问题，将查询出来的数据作为临时表，再加一层select
select(
    select DISTINCT salary FROM Employee ORDER BY Salary DESC LIMIT 1,1) 
AS SecondHighestSalary

-- 使用IFNULL子句可读性更高更规范。
select IFNULL((
    select distinct salary from Employee order by salary DESC LIMIT 1,1
),null) AS SecondHighestSalary 
```



### Note

- Solution1需要实现的步骤：
  - 先查询出最大值
  - 在筛选小于 子查询的结果 的最大值
- Solution2需要实现的步骤：
  - `DISTINCT`去重 
  - `ORDER BY`排序
  - `LIMIT`子句取出第二 
  - 查询不到返回null，作为临时表或使用`IFNULL`函数

If you have a better solution, you can star and fork [Leetcode-database-solution](https://github.com/orrrz/Leetcode-database-solution) then create a pull request. Thank you!