---
id: data-model
--- 

# 数据模型

## 简介
GrowingIO采集的原始行为数据分为四种不同类型，分别为访问（visit）、页面（page）、埋点（custom_event）和行为（action）。

* 访问（visit）： 代表用户开启了一个新的访问会话，访问行为的生命周期与会话（session）绑定，新的session代表一个新的访问。
* 页面浏览（page）：代表用户的一次页面浏览，SDK采集以及发送浏览事件中的数据。
* 埋点（custom_event）： 代表用户触发了客户埋的点发送的事件。事件触发的时间以及发送的行为数据信息都由客户指定。
* 行为（action）： 代表用户操作了页面上的某些元素发送的行为，包括点击了按钮、修改了数据框的内容等等。

过去，GrowingIO数据平台将上述四种行为数据存储至多张表中，这种模型导致后续的统计逻辑非常复杂。为了串联多种行为数据，我们在查询时进行了多表关联计算，因此导致部分极端场景下数据计算结果不一致的问题偶有发生。另外，该种数据模型数据比较分散，没有统一的接口，不易与其他组件进行对接。

在[9.0版本](../../update-log.md#v-2020-9-0-2020-nian-9-yue-30-ri-fa-bu)后，我们将多种行为数据统一抽象为EVENT模型，即四种行为数据统一到一张表中。该种模型简化了平台计算逻辑，并且通过Thrift Server方便GrowingIO数据平台与其他组件进行对接，进而提升开发效率和降低维护成本。

最新的数据模型同时具备了提供实时数据的能力，行为数据从触点触发再到客户可以观察到，时间间隔一般在10秒以内。

## 客户操作手册
GrowingIO CDP为客户安装了Zeppelin，客户可以通过Zeppelin SQL解释器查询数据平台中的数据库、数据表和表中数据。

SQL语法：

* 查询所有的数据库：show databases
* 查询数据库中的数据表：show tables in {database_name}
* 查询数据表结构：desc {database_name}.{table_name}
* 查询数据表创建语句：show create table {database_name}.{table_name}
* 查询表分区：select partition from system.parts where database='{databasename}' and table='{table_name}'
* 查询数据表数据： select {field} from {database_name}.{table_name}

## 数据表
* 事件表：event
* 用户表：user
* 用户融合表：user_merged

