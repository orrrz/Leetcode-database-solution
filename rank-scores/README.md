# [178. Rank Scores](https://leetcode-cn.com/problems/rank-scores/)

### Description

编写一个 SQL 查询来实现分数排名。如果两个分数相同，则两个分数排名（Rank）相同。请注意，平分后的下一个名次应该是下一个连续的整数值。换句话说，名次之间不应该有“间隔”。

```
+----+-------+
| Id | Score |
+----+-------+
| 1  | 3.50  |
| 2  | 3.65  |
| 3  | 4.00  |
| 4  | 3.85  |
| 5  | 4.00  |
| 6  | 3.65  |
+----+-------+
```

例如，根据上述给定的 `Scores` 表，你的查询应该返回（按分数从高到低排列）：

```
+-------+------+
| Score | Rank |
+-------+------+
| 4.00  | 1    |
| 4.00  | 1    |
| 3.85  | 2    |
| 3.65  | 3    |
| 3.65  | 3    |
| 3.50  | 4    |
+-------+------+
```

### Solution

```mysql
select Score, (select count(distinct score) from scores where score >= s.score) as Rank from scores s order by score desc;

SELECT Score, 

CASE 
WHEN @prevRank = Score THEN @curRank 
WHEN @prevRank := Score THEN @curRank := @curRank + 1
END AS Rank

FROM Scores s, 
(SELECT @curRank := 0, @prevRank := 0) r
ORDER BY s.Score desc;

-- Oracle 可以使用窗口函数dense_rank()
 DENSE_RANK() over(order by 列名 desc）as Rank
```

### Note

If you have a better solution, you can star and fork [Leetcode-database-solution](https://github.com/orrrz/Leetcode-database-solution) then create a pull request. Thank you!

