# 第七课 计算字段

### 计算字段

存储在数据库中的数据一般不是应用程序需要的 **格式**，在检索之后，需要进行**转换**、**计算**、**格式化**等处理，此时需要使用计算字段。

计算字段虽然称为字段，但是并不是数据库中的 **实际列**，而是 **运行时** 由 SELECT 语句创建的。

### 拼接字段 `||`

```
SELECT vend_name || ' (' || vend_country || ')' FROM Vendors
ORDER BY vend_name;
```
* PostgreSQL 使用 `||` 而非 `+` 拼接不同列。

#### **别名** `AS`

如果要使用拼接出来的新字段，需要给一个别名，便于引用。

```
SELECT vend_name || ' (' || vend_country || ')'
	AS vend_title
FROM Vendors
ORDER BY vend_name;
```
* 别名既可以是一个 **单词**，也可以是一个字符串，但 **不建议** 用字符串。

### 算术计算

```
SELECT prod_id, quantity, item_price,
	quantity * item_price AS expanded_price
FROM OrderItems
WHERE order_num = 20008;