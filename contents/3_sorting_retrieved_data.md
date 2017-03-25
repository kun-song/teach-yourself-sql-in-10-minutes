# 第三课 检索排序结果

### 单列排序

```
SELECT prod_name FROM Products 
ORDER BY prod_name;
```
* 排序规则
	+ 字母顺序排序。
	+ DBMS 一般不区分大小写，如果需要区分，需配置 DBMS。
* `ORDER BY` 必须是 `SELECT` 语句的 **最后** 一个子句。
* 可以使用 **任意列** 来排序。

### 多列排序

```
SELECT prod_id, prod_price, prod_name FROM Products 
ORDER BY prod_price, prod_name;
```
* 排序规则
	+ 首先按照 `prod_price` 排序，如果 `prod_price` 相同，则按照 `prod_name` 排序。
	+ 如果 `prod_price` 都不相同，则 `prod_name` 不参与排序。

### 相对位置排序

```
SELECT prod_id, prod_price, prod_name FROM Products 
ORDER BY 2, 3;
```
* 相对位置是指在 `SELECT` 后面的 `prod_id, prod_price, prod_name` 中的相对位置，其分别为：1，2，3.
* 效果与 `ORDER BY prod_price, prod_name` 相同。
* 优点：打字少。
* 缺点：容易出错，如果要排序的列不在 `SELECT` 后面则无法使用。

可以与直接指定列名结合使用：

```
SELECT prod_id, prod_price, prod_name FROM Products 
ORDER BY 2, prod_name;
```
### 排序方向

```
SELECT prod_id, prod_price, prod_name FROM Products 
ORDER BY prod_price DESC;
```
* `ORDER BY` **默认升序**
* `DESC` 显式指定 **降序排序**

```
SELECT prod_id, prod_price, prod_name FROM Products 
ORDER BY prod_price DESC, prod_name;
```
* 效果：`prod_price` 降序，`prod_name` 升序。
* `DESC` 只能修饰其前面的列，如果要对多个列降序，必须在每个列后面指定 `DESC`。