# 第五课 高级数据过滤

### 组合 `WHERE` 子句

第 4 课使用的都是 **单个WHERE** 子句，使用 `AND` 和 `OR` 可以组合多个 WHERE 子句，形成更复杂的过滤条件。

#### `AND`

```
SELECT prod_id, prod_price, prod_name FROM Products
WHERE vend_id = 'DLL01' AND prod_price <= 4;
```

#### `OR`

```
SELECT prod_id, prod_price, prod_name FROM Products
WHERE vend_id = 'DLL01' OR vend_id = 'BRS01';
```

#### `AND` `OR` 求值顺序

`WHERE` 子句中可以包含任意数量的 `AND` `OR` 子句，但是 `AND` 优先级要比 `OR` 高。

```
SELECT prod_name, prod_price FROM Products 
WHERE vend_id = 'DLL01' OR vend_id = 'BRS01' AND prod_price >= 10;
```
* 本意：过滤出 vend_id 为 DLL01 或者 BRS01 并且 prod_price 大于等于 10 的产品。
* 但是 `AND` 优先级 > `OR`，所以最后结果是：vend_id 为 DLL01 或者 vend_id 为 BRS01 且产品价格 >= 10 的产品。

使用 `()` 修改如下：

```
SELECT prod_name, prod_price FROM Products 
WHERE (vend_id = 'DLL01' OR vend_id = 'BRS01') 
	AND prod_price >= 10;
```

**在 WHERE 子句中的 AND OR 必须使用（）分组，不能依赖默认的优先级**。

### `IN` 操作符 -> 多个 `OR`

```
SELECT prod_name, prod_price FROM Products 
WHERE vend_id IN ('DLL01', 'BRS01')
ORDER BY prod_name;
```
* 匹配 **一组值**。
* `IN` 功能与 `OR` 类似，写法更简便、更清楚。
* `IN` 还可以包含其他 `SELECT` 语句，可以动态创建 `WHERE` 子句。

### `NOT`

```
SELECT prod_name FROM Products 
WHERE NOT vend_id = 'DLL01'
ORDER BY prod_name;
```
简单场景下，`NOT` 可以用 `<>` `!=` 来实现。

```
SELECT prod_name FROM Products 
WHERE vend_id != 'DLL01'
ORDER BY prod_name;
```
但是更加复杂的场景，比如 `NOT` 与 `IN` 联合使用，就不容易用 `!=` 重写。

```
SELECT prod_name FROM Products 
WHERE NOT vend_id IN ('DLL01', 'BSR01')
ORDER BY prod_name;
```
