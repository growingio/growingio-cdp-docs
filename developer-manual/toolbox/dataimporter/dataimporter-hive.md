# Hive数据导入

导入Hive类型的数据，支持：

* 用户属性数据导入
* 用户行为数据导入

## 用户属性数据导入 <a id="yong-hu-shu-xing-shu-ju-dao-ru"></a>

```text
python3 format_importer.py -m user_variables \
-ds <数据源ID> \
-f <文件格式> \
-db_host <数据库连接地址> \
-db_user <数据库连接用户> \
-db_password <数据库连接密码> \
[-db_port<数据库连接端口号] \
-sql <查询语句>
```

ds：必选参数，数据源ID在前端获得，操作详见[附录](https://docs.growingio.com/op/developer-manual/toolbox/dataimporter/dataimporter-mysql#fu-lu)​

f：必选参数，导入数据格式，填写：hive

db\_host：必选参数，数据库连接地址

db\_user：必选参数，数据库连接用户名

db\_password：必选参数，数据库连接密码

db\_port：可选参数，数据库连接端口，默认10000

sql：必选参数，查询语句，输出列须包含userId字段，其他字段须已在用户属性中定义

例如，数据库中用户表为db.user，需要导入的字段及部分行数据如下：

​

| userid | gender | age | viplevel |
| :--- | :--- | :--- | :--- |
| 123 | 男 | 19 | 初级 |
| 234 | 女 | 38 | 中级 |
| 345 | 男 | 22 | 高级 |

假设待导入的字段gender、age和viplevel已在用户属性中创建，则sql参数可编写为如下：

```text
select userid as userId,gender as gender,age as age,viplevel as viplevel 
from db.user
```

脚本执行成功，用户属性数据导入后，系统将立即进行相关指标的计算，在[前端可以查看计算进度](https://docs.growingio.com/op/product-manual/customer-data-platform/datasource/data-import)​

## 用户行为数据导入 <a id="yong-hu-hang-wei-shu-ju-dao-ru"></a>

```text
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

ds：必选参数，数据源ID在前端获得，操作详见[附录](https://docs.growingio.com/op/developer-manual/toolbox/dataimporter/dataimporter-mysql#fu-lu)​

f：必选参数，导入数据格式，填写：hive

db\_host：必选参数，数据库连接地址

db\_user：必选参数，数据库连接用户名

db\_password：必选参数，数据库连接密码

db\_port：可选参数，数据库连接端口，默认10000

sql：必选参数，查询语句。输出列须包含userId、event和timestamp字段，其中event为埋点事件名，timestamp为事件发生的时间戳，单位是毫秒。其他字段须已在用户属性中定义

s：必选参数，导入用户行为数据的起始日期，格式：YYYY-MM-DD

e：必选参数，导入用户行为数据的结束日期，格式：YYYY-MM-DD

例如，数据库中用户表为db.event，需要导入的用户行为数据如下：

​

| userid | event | event\_time | prod\_id | price | color |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 123 | ViewProd | 2020-01-01 01:01:01 | 1 | 19.0 | 红 |
| 234 | ViewProd | 2020-01-02 02:02:02 | 2 | 38.1 | 绿 |
| 345 | ViewProd | 2020-01-03 03:03:03 | 3 | 22.2 | 蓝 |

假设对应的行为事件属性名prod\_id、price和color已在事件属性中创建，则sql参数可编写为如下：

```text
select userid as userId,
event as event,
unix_timestamp(event_time)*1000 as timestamp,
prod_id as prod_id,
price as price,
color as color 
from db.event
```

脚本执行成功，用户行为数据导入后，系统将立即进行相关指标的计算，在[前端可以查看计算进度](https://docs.growingio.com/op/product-manual/customer-data-platform/datasource/data-import)​

## 其他说明 <a id="qi-ta-shuo-ming"></a>

* ​[辅助工具下载](https://docs.growingio.com/op/developer-manual/toolbox)​

## 附录 <a id="fu-lu"></a>

​[前端创建数据源](https://docs.growingio.com/op/product-manual/customer-data-platform/datasource/datasource-manage#chuang-jian-shu-ju-yuan)，进入数据源管理页面：

* 创建 用户属性数据 导入数据源，操作方式：新建数据源 &gt; 历史数据导入 &gt; 用户属性数据
* 创建 用户行为数据 导入数据源，操作方式：新建数据源 &gt; 历史数据导入 &gt; 用户行为数据

创建后，在数据源管理列表页面查看相应的数据源ID：![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MSwELOQCxWQX2836G8p%2F-MSwEvCr6ld7lu_vujep%2F%E5%9B%BE%E7%89%87.png?alt=media&token=315eebb8-729d-4c40-a5bf-33c07d9c8e7e)

