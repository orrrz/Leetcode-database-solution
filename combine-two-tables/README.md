## 175.combine-two-tables

### Description

表1: `Person`

```
+-------------+---------+
| 列名         | 类型     |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
PersonId 是上表主键
```

表2: `Address`

```
+-------------+---------+
| 列名         | 类型    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
AddressId 是上表主键
```

 

编写一个 SQL 查询，满足条件：无论 person 是否有地址信息，都需要基于上述两表提供 person 的以下信息：

 

```
FirstName, LastName, City, State
```



### Solution

```mysql
SELECT p.FirstName, p.LastName, a.City, a.State FROM Person p LEFT JOIN Address a ON p.PersonId = a.PersonId
```



### Note

1. 表 Address 中的 personId 是表 Person 的外关键字 

2. 并非每个人都有地址信息，所以使用外连接，left outer join  (等于left join)

3. 数据库在通过连接两张或多张表来返回记录时，都会生成一张中间的临时表，然后再将这张临时表返回给用户。

4. 在使用left jion时，on和where条件的区别如下：
   - on条件是在生成临时表时使用的条件。
   - where条件是在临时表生成好后，再对临时表进行过滤的条件。

If you have a better solution, you can star and fork [Leetcode-database-solution](https://github.com/orrrz/Leetcode-database-solution) then create a pull request. Thank you!
