---
id: data-importer-mysql
sidebar_position: 4
---

# Mysql 数据导入

## 简介[](#jian-jie)

导入 Mysql 类型的数据，支持：

- 用户属性数据导入
- 用户行为数据导入

使用前，请先阅读[数据导入工具](../../../developer-manual/toolbox/dataimporter)的内容介绍。

## 功能说明[](#yong-hu-shu-xing-shu-ju-dao-ru)

### 用户属性数据导入[](#yong-hu-shu-xing-shu-ju-dao-ru-1)

```sh
python3 format_importer.py -m user_variables \
-ds <数据源ID> \
-f <文件格式> \
-db_host <数据库连接地址> \
-db_user <数据库连接用户> \
-db_password <数据库连接密码> \
[-db_port<数据库连接端口号] \
-sql <查询语句>
```

ds：必选参数，数据源 ID 在前端获得，操作详见[附录](https://docs.growingio.com/op/developer-manual/toolbox/dataimporter/dataimporter-mysql#fu-lu)​

f：必选参数，导入数据格式，填写：mysql

db_host：必选参数，数据库连接地址

db_user：必选参数，数据库连接用户名

db_password：必选参数，数据库连接密码

db_port：可选参数，数据库连接端口，默认 3306

sql：必选参数，查询语句，输出列须包含 userId 字段，其他字段须已在用户属性中定义

例如，数据库中用户表为 db.user，需要导入的字段及部分行数据如下：

| userid | gender | age | viplevel |
| ------ | ------ | --- | -------- |
| 123    | 男     | 19  | 初级     |
| 234    | 女     | 38  | 中级     |
| 345    | 男     | 22  | 高级     |

假设待导入的字段 gender、age 和 viplevel 已在用户属性中创建，则 sql 参数可编写为如下：

select userid as userId,gender as gender,age as age,viplevel as viplevel

from db.user​

### 用户行为数据导入[](#yong-hu-hang-wei-shu-ju-dao-ru)

```sh
python3 format_importer.py -m events \
-ds <数据源ID> \
-f <文件格式> \
-db_host <数据库连接地址> \
-db_user <数据库连接用户> \
-db_password <数据库连接密码> \
[-db_port<数据库连接端口号] \
-sql <查询语句> \
-s <数据起始日期> \
-e <数据结束日期>
```

ds：必选参数，数据源 ID 在前端获得，操作详见[附录](https://docs.growingio.com/op/developer-manual/toolbox/dataimporter/dataimporter-mysql#fu-lu)​

f：必选参数，导入数据格式，填写：mysql

db_host：必选参数，数据库连接地址

db_user：必选参数，数据库连接用户名

db_password：必选参数，数据库连接密码

db_port：可选参数，数据库连接端口，默认 3306

sql：必选参数，查询语句。输出列须包含 userId、event 和 timestamp 字段，其中 event 为埋点事件名，timestamp 为事件发生的时间戳，单位是毫秒。其他字段须已在用户属性中定义

s：必选参数，导入用户行为数据的起始日期，格式：YYYY-MM-DD

e：必选参数，导入用户行为数据的结束日期，格式：YYYY-MM-DD

例如，数据库中用户表为 db.event，需要导入的用户行为数据如下：

| userid | event    | event_time          | prod_id | price | color |
| ------ | -------- | ------------------- | ------- | ----- | ----- |
| 123    | ViewProd | 2020-01-01 01:01:01 | 1       | 19.0  | 红    |
| 234    | ViewProd | 2020-01-02 02:02:02 | 2       | 38.1  | 绿    |
| 345    | ViewProd | 2020-01-03 03:03:03 | 3       | 22.2  | 蓝    |

假设对应的行为事件属性名 prod_id、price 和 color 已在事件属性中创建，则 sql 参数可编写为如下：

```sql
select userid as userId,
event as event,
unix_timestamp(event_time)*1000 as timestamp,
prod_id as prod_id,
price as price,
color as color
from db.event
```
