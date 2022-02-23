---
id: data-importer-txt
sidebar_position: 3
---

# 文本数据导入

## 简介[](#jian-jie)

导入文本类型的数据，支持：

* 用户属性数据导入
    
* 用户行为数据导入
    
使用前，请先阅读[数据导入工具](../../../developer-manual/toolbox/dataimporter)的内容介绍。


## 功能说明[](#yong-hu-shu-xing-shu-ju-dao-ru)

### 用户属性数据导入[](#yong-hu-shu-xing-shu-ju-dao-ru-1)

```sh
python3 data_importer.py -m user_variables \
-p <文件路径> \
-ds <数据源ID> \
[-f <文件格式>] \
[-qf <文本限定符>] \
[-sep <文本分隔符>] \
[-skh <自动跳过文件首行>] \
[-attr <映射属性名>] 
```

p：必选参数，需要导入数据所在的文件路径

ds：必选参数，数据源ID在前端获得，操作详见附录​

f：可选参数，文件格式支持JSON、CSV、TSV三种格式，默认JSON

qf：可选参数，CSV、TSV格式文本限定符默认："

sep：可选参数，CSV、TSV格式文本分隔符默认：,

skh：可选参数，CSV、TSV格式设置则自动跳过首行，此参数无需设置值

attr：可选参数，CSV、TSV格式文件的各列按顺序映射到属性名，英文逗号分隔，必须指定userId列

例如，需要导入的用户属性数据如下：

| 用户ID | 性别  | 年龄  | 会员级别 |
| --- | --- | --- | --- |
| 123 | 男   | 19  | 初级  |
| 234 | 女   | 38  | 中级  |
| 345 | 男   | 22  | 高级  |

导入文件为user.csv：

用户ID,性别,年龄,会员级别

123,男,19,初级

234,女,38,中级

345,男,22,高级

假设对应的用户属性名gender、age和viplevel已创建，导入这三个属性数据的命令：

```sh
python3 data_importer.py -m user_variables \
-p user.csv \
-ds <数据源ID> \
-f CSV \
-sep , \
-skh \
-attr userId,gender,age,viplevel
```

若只导入文件中的部分属性，如导入age和viplevel两个属性，命令如下：

```sh
python3 data_importer.py -m user_variables \
-p user.csv \
-ds <数据源ID> \
-f CSV \
-sep , \
-skh \
-attr userId,,age,viplevel
```

注意，attr中的用户ID为userId，必须指定列；

attr中的列跟文件列需要按顺序匹配，不需要导入的列为空列占位，attr按照英文逗号拆分列的个数与文件列个数不一致将导致校验失败，无法导入；​


### 用户行为数据导入[](#yong-hu-hang-wei-shu-ju-dao-ru)

```sh
python3 data_importer.py -m events \
-p <文件路径> \
-ds <数据源ID> \
[-f <文件格式>] \
[-qf <文本限定符>] \
[-sep <文本分隔符>] \
[-skh <自动跳过文件首行>] \
[-attr <映射属性名>] \
-s <数据起始日期> \
-e <数据结束日期>
```

p：必选参数，需要导入数据所在的文件路径

ds：必选参数，数据源ID需在前端创建数据源后获得，详见附录

f：可选参数，文件格式支持JSON、CSV、TSV三种格式，默认JSON

qf：可选参数，CSV、TSV格式文本限定符默认："

sep：可选参数，CSV、TSV格式文本分隔符默认：,

skh：可选参数，CSV、TSV格式设置则自动跳过首行，此参数无需设置值

attr：可选参数，CSV、TSV格式文件的各列按顺序映射到属性名，英文逗号分隔，必须指定用户IDuserId、事件类型event、事件时间戳timestamp三列

s：必选参数，导入用户行为数据的起始日期，格式：YYYY-MM-DD

e：必选参数，导入用户行为数据的结束日期，格式：YYYY-MM-DD

例如，需要导入的用户行为数据如下：

| 用户ID | 事件标识 | 事件时间 | 商品ID | 价格  | 颜色  |
| --- | --- | --- | --- | --- | --- |
| 123 | ViewProd | 2020-01-01 01:01:01 | 1   | 19.0 | 红   |
| 234 | ViewProd | 2020-01-02 02:02:02 | 2   | 38.1 | 绿   |
| 345 | ViewProd | 2020-01-03 03:03:03 | 3   | 22.2 | 蓝   |

导入的文件为events.csv（事件时间已转换为毫秒时间戳）：

用户ID,事件标识,事件时间戳,商品ID,价格,颜色

123,ViewProd,1577811661000,1,19.0,红

234,ViewProd,1577901722000,2,39.1,绿

345,ViewProd,1577991783000,3,22.2,蓝

假设对应的行为事件属性名prod_id、price和color已创建，导入该行为事件的命令：

```sh
python3 data_importer.py -m events \
-p events.csv \
-ds <数据源ID> \
-f CSV \
-sep , \
-skh \
-attr userId,event,timestamp,prod_id,price,color \
-s 2020-01-01 \
-e 2020-01-03
```

注意，attr中的用户ID为userId，事件类型为event，事件时间戳为timestamp，三个字段必须指定列；

attr中的列跟文件列需要按顺序匹配，不需要导入的列为空列占位，attr按照英文逗号拆分列的个数与文件列个数不一致将导致校验失败，无法导入；

导入用户行为数据时，起始和结束日期的两个参数必须设定，若导入数据的时间超过了起始和结束的范围，将校验失败，无法导入成功，以确保导入如何预期​
