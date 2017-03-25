# 附录 搭建测试环境

## 在 mac 下搭建测试环境

使用一个玩具经销商的订单录入系统作为例子，主要功能有：

* 管理供应商
* 管理产品目录
* 管理客户列表
* 录入客户订单

该系统中有 5 个表，下面分别描述。

### Vendors 表

存储产品的供应商，每个供应商对应 Vendors 表中的一行。

| 		 列名 		| 		说明 		|
| 		:---: 		| 		:---: 		|
| vend_id		 	| 唯一的供应商 ID 	|
| vend_name 		| 供应商名 			|
| vend_address 	| 供应商地址 		|
| vend_city 		| 供应商所在城市	|
| vend_state 		| 供应商所在州		|
| vend_zip 		| 供应商地址邮编	|
| vend_country 	| 供应商所在国家	|

* 主键：vend_id
* Vendors 通过 vend_id 与 Products 表关联

### Products 表

存储产品信息，每个产品对应一行。

| 		 列名 		| 		说明 		|
| 		:---: 		| 		:---: 		|
| prod_id		 	| 唯一的产品 ID 	|
| **vend_id**		| 供应商 ID（外键）|
| prod_name		| 产品名		 	|
| prod_price		| 价格			 	|
| prod_desc		| 产品描述		 	|

* 主键：prod_id
* 外键：vend_id，与 Vendors 表关联

### Customers 表

存储顾客信息，每个顾客对应一行。

| 		 列名 		| 		说明 		|
| 		:---: 		| 		:---: 		|
| cust_id		 	| 唯一的顾客 ID 	|
| cust_name		| 顾客名		 	|
| cust_address	| 顾客地址		 	|
| cust_city		| 顾客所在城市		|
| cust_state		| 顾客所在州		|
| cust_zip		| 顾客地址的邮编	|
| cust_country	| 顾客所在国家 		|
| cust_contact	| 顾客的联系名 		|
| cust_email		| 顾客邮件地址 		|

* 主键：cust_id

### Orders 表

存储顾客订单（不是订单细节），每个订单对应一行。

| 		 列名 		| 		说明 		|
| 		:---: 		| 		:---: 		|
| order_num		| 唯一的订单号 		|
| order_date		| 订单日期	 		|
| **cust_id**		| 订单顾客 ID 		|

* 主键：order_num
* 外键：cust_id，关联到 Customers 表。

### OrderItems 表

存储每个订单中的实际物品，**每个订单** 的 **每个物品** 对应一行，对于 Orders 表中一行，在 OrderItems 中可能对应 **一行或者多行**，因为一个订单中可能有多个物品。

| 		 列名 		| 		说明 		|
| 		:---: 		| 		:---: 		|
| **order_num**	| 订单号 			|
| order_item		| 订单物品号（订单内的顺序）|
| **prod_id**		| 产品 ID	 		|
| quantity		| 物品数量	 		|
| item_price		| 物品价格	 		|

* 主键：order_num + order_item
* 外键：
	+ order_num 关联 Orders 表
	+ prod_id 关联 Products 表

### 创建表 & 填充数据

使用 create.txt 和 populate.txt 中的命令创建、填充表。

#### PostgreSQL 基本操作

**psql 基本用法**

* `\n statement` 查看 statement 命令的用法
* `\l` 列出所有数据库
* `\c db_name` 连接其他数据库
* `\d` 列出当前数据库中的所有表格
* `\d table_name` 列出某个表的表结构
* `\du` 列出所有用户
* `\e` 打开文本编辑器
* `\conninfo` 列出当前数据库和连接的信息
* `\?` 列出所有可用命令

**pgAdmin**

mac 下也可以使用 pgAdmin，不过很挫。

**创建数据库**

	createdb mydb

**删除数据库**

	dropdb mydb
