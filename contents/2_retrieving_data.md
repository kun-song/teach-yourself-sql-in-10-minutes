# 第二课 检索数据

**关键字**

诸如 SELECT 等是 SQL 保留的关键字，表名、列名不能使用。

**注意**

* SQL 在不同 DBMS 中不同，相同语句的执行结果也跟 DBMS 有关系。

### 单个列

	SELECT prod_name FROM Products;
	
* **未排序**
	+ 注意，上面语句结果是未排序的，返回数据的顺序是不确定的，可能是插入顺序，也可能不是，不能依赖该顺序。
* **大小写**
	+ 关键字，比如 `SELECT` 是不区分大小写的。
	+ **表名、列名** 是否区分大小写与 DBMS 有关。
	+ 一般关键字大写，表名、列名小写。
* 使用 `;` 结束 SQL 语句（单个语句也可不用）。

### 多个列

	SELECT prod_id, prod_name, prod_price FROM Products;

**数据表示**

* SQL 语句一般返回 **原始的、无格式** 的数据。
* 数据的格式化是表示问题，而不是检索问题。
* 一般应用也不会直接使用 SQL 返回的数据，而是自己做处理。

### 所有列

	SELECT * FROM Products;
	
* **列的顺序**
	+ 一般是 **表定义** 时列出现的顺序，但也不一定。
	+ 应用一般 **自己处理**，所以列的顺序影响不大。
* 通配符 `*`
	+ 缺点：`*` 通常会降低检索性能。
	+ 优点：`*` 可以检索出名字未知的列。

### 检索不同的值

	SELECT DISTINCT vend_id FROM Products;

* `SELECT` 会返回所有匹配的行，但是其中可能会有 **完全相同** 的行，使用 `DISTINCT` 可以消除相同的冗余行。
* `DISTINCT` 修饰 **所有列**，必须放在列名之前。

### 限制检索数量

	SELECT prod_name FROM Products LIMIT 5;
	// 从 index = 5 开始，检索后面 5 个
	SELECt prod_name FROM Products LIMIT 5 OFFSET 5;
	
* 返回 **最多** 5 个匹配结果，如果不足 5 个则返回实际数量。
* 不同 DBMS 实现方式 **不同**，这是 MySQL/PostgreSQL 的实现方式。
* **LIMIT**
	+ 限制返回的行数。
* **OFFSET**
	+ 指定从哪里开始。
	+ 第一个检索出来的是第 0 行，所以 `OFFSET 5` 是从第 6 个开始（包含第 6 个）。

### 注释

```
SELECT prod_name -- 行内注释
FROM Products;

# 整行注释，在 pgAdmin 中报错
SELECT prod_name FROM Products;

/*跨行间

注释*/
SELECT prod_name FROM Products;
```
