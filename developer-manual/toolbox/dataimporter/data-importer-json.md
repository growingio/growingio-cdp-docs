---
id: data-importer-json
sidebar_position: 2
---

# Json 数据导入

## 简介[](#jian-jie)

导入Json格式的数据，支持：

* 用户属性数据导入
    
* 用户行为数据导入
    
使用前，请先阅读[数据导入工具](../../../developer-manual/toolbox/dataimporter/data-importer)的内容介绍。


## 功能说明[](#yong-hu-shu-xing-shu-ju-dao-ru)

### 用户属性数据导入[](#yong-hu-shu-xing-shu-ju-dao-ru-1)

用户属性数据导入的命令及参数如下：

```sh
python3 data_importer.py -m user_variables \
-ds <数据源ID> \
-p <文件路径>
```

ds：必选参数，数据源ID，需在页面上创建数据源后获得，详见附录
p：必选参数，需要导入数据所在文件的路径
例如，需要导入的数据文件是user.json，内容如下：
```
{"userId": "156xxx", "attrs": {"sex": "男", "age": "16"}}
{"userId": "157xxx", "attrs": {"sex": "女", "age": "28"}}
```

假设数据源ID为123456789（实际以系统中定义的为准），且数据文件放在执行命令的同级目录下，则实际执行的语句如下：

```sql
python3 data_importer.py -m user_variables \
-ds 123456789 \
-p user.json
```

### 用户行为数据导入[](#yong-hu-hang-wei-shu-ju-dao-ru)

用户行为数据导入的命令及参数如下：

```sh
python3 data_importer.py -m events \
-ds <数据源ID> \
-p <文件路径> \
-s <数据起始日期> \
-e <数据结束日期>
```
ds：必选参数，数据源ID，需在页面上创建数据源后获得，详见附录
p：必选参数，需要导入数据所在文件的路径
s：必选参数，导入用户行为数据的起始日期，格式：YYYY-MM-DD
e：必选参数，导入用户行为数据的结束日期，格式：YYYY-MM-DD
例如，需要导入的数据文件是event.json，内容如下：
```
{"event": "paySuccess", "userId": "156xxx", "timestamp": 1609453363001, "attrs": {"type": "Wechat"}}
{"event": "paySuccess", "userId": "157xxx", "timestamp": 1609453363002, "attrs": {"type": "Wechat"}}
{"event": "paySuccess", "userId": "158xxx", "timestamp": 1609453363003, "attrs": {"type": "Wechat"}}
```

假设数据源ID为123456789（实际以系统中定义的为准），且数据文件放在执行命令的同级目录下，则实际执行的语句如下：

```sql
python3 data_importer.py -m events \
-ds 123456789 \
-p event.json \
-s 2021-01-01 \
-e 2021-01-02
```

导入用户行为数据时，起始和结束日期的两个参数必须设定，若导入数据中任意一条的时间超过了设定的起始和结束日期范围，将校验失败，无法导入成功。
