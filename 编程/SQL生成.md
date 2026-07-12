# SQL 生成

## 适用平台
ChatGPT / Claude / Kimi / DeepSeek / 通义千问 / 豆包

## 使用方法
告诉 AI 你有什么表、想查什么，它帮你写 SQL。

## 提示词

```
你是一位 SQL 专家。请根据我的需求生成 SQL 查询语句。

数据库类型：「如：MySQL 8.0 / PostgreSQL / SQLite」

表结构：
「粘贴你的 CREATE TABLE 语句或者描述表结构」

我想查询：「用大白话描述你想查什么」

要求：
1. 如果查询涉及多表，先说明 JOIN 逻辑
2. 注释关键行
3. 如果有性能优化的写法（如索引建议），一并说明
4. 如果查询结果可能很大，建议加 LIMIT
5. 考虑 NULL 值的处理
```

## 示例

**输入：**
```
数据库：MySQL
表：orders（id, user_id, amount, status, created_at）
表：users（id, name, level）
想查：上月每个会员等级的订单总额，按总额从高到低排列
```

**输出：**
```sql
SELECT 
    u.level AS '会员等级',
    COUNT(o.id) AS '订单数',
    SUM(o.amount) AS '订单总额'
FROM orders o
JOIN users u ON o.user_id = u.id
WHERE o.created_at >= DATE_FORMAT(DATE_SUB(NOW(), INTERVAL 1 MONTH), '%Y-%m-01')  -- 上月1号
  AND o.created_at < DATE_FORMAT(NOW(), '%Y-%m-01')  -- 本月1号（不含）
  AND o.status = 'completed'  -- 只统计完成的订单
GROUP BY u.level
ORDER BY SUM(o.amount) DESC;
```

## 技巧
- 永远在 WHERE 条件里先测试，确认数据对了再写正式查询
- AI 生成的 SQL 可能没有考虑 NULL，检查关键字段
- 更新/删除语句务必先 SELECT 确认要操作的数据范围
