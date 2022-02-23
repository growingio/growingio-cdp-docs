---
id: metadata-creator
sidebar_position: 3
---

# 元数据创建工具

## 简介[](#jian-jie)

GrowingIO 数据模型的元数据主要包括事件、事件属性、用户属性，通过元数据创建工具，可以在命令行模式下直接创建元数据。

元数据创建工具支持的操作：

- 创建事件
- 创建事件属性
- 创建用户属性
- 绑定事件与事件属性
- 导出元数据
- 导入元数据

> 该工具不提供删除功能。若需删除已创建但无用的元数据，需在 GrowingIO 前端功能里操作。

使用前，请先阅读[辅助工具](../../developer-manual/toolbox/dataimporter#功能边界或约束)的内容介绍。

## 功能说明[](#chuang-jian-shi-jian)

### 创建事件[](#chuang-jian-shi-jian-1)

```sh
python3 meta_importer.py -m create_event \
--key <事件名> \
[--name <事件显示名>] \
[--desc <事件描述>]
```

key：必须参数，事件名必须是合法的变量名，仅允许大小写英文、数字、以及下划线，并且不能以数字开头，限长 30 字符；

name：可选参数，事件显示名可在界面上配置，不加该参数则默认同事件名；

desc：可选参数，事件描述中若有空格则需要加双引号；

例如创建事件 ViewProd，显示名是“浏览商品”：

```sh
python3 meta_importer.py -m create_event \
--key ViewProd \
--name 浏览商品
```

若 key 已存在，则将该事件的 name、desc 修改为新的输入值

### 创建事件属性[](#chuang-jian-shi-jian-shu-xing)

```sh
python3 meta_importer.py -m create_event_variables \
--key <事件属性名> \
--type <事件属性数据类型> \
[--name <事件属性显示名>] \
[--desc <事件属性描述>]
```

key：必须参数，事件属性名必须是合法的变量名，仅允许大小写英文、数字、以及下划线，并且不能以数字开头，限长 30 字符；

type：必选参数，事件属性数据类型可选值：string/int/double；

name：可选参数，可在界面上配置，不加该参数则默认同事件属性名；

desc：可选参数，事件属性描述中若有空格则需要加双引号；

例如创建事件属性 Price，显示名是“价格”，类型是 double：

```sh
python3 meta_importer.py -m create_event_variables \
--key Price \
--type double \
--name 价格
```

若 key 已存在，则将该事件属性的 type、name、desc 修改为新的输入值

### 创建用户属性[](#chuang-jian-yong-hu-shu-xing)

```sh
python3 meta_importer.py -m create_user_variables \
--key <用户属性名> \
--type <用户属性数据类型> \
[--name <用户属性显示名>] \
[--desc <用户属性描述>]
```

key：必须参数，用户属性名必须是合法的变量名，仅允许大小写英文、数字、以及下划线，并且不能以数字开头，限长 30 字符；

type：必选参数，用户属性数据类型可选值：string/int/date；

name：可选参数，可在界面上配置，不加该参数则默认同用户属性名；

desc：可选参数，用户属性描述中若有空格则需要加双引号；

### 绑定事件与事件属性[](#bang-ding-shi-jian-yu-shi-jian-shu-xing)

```sh
python3 meta_importer.py -m bind_event_variables \
--key <事件名> \
--attr <绑定事件属性名集合>
```

key：必须参数，若事件不存在则创建；

attr：必须参数，多个属性名之间用英文逗号分隔；

例如将 ViewProd 事件与 Price 和 Color 绑定：

```sh
python3 meta_importer.py -m bind_event_variables \
--key ViewProd \
--attr Price,Color
```

### 导出元数据[](#dao-chu-yuan-shu-ju)

导出的元数据可以直接用于导入（下一节介绍）。

```sh
python3 meta_importer.py -m export_meta \
--file <文件名>
```

file：必须参数，指定导出元数据的文件名

运行后会导出元数据信息，例如：

```sh
python3 meta_importer.py -m export_meta \
--file meta.json
```

导出的样例格式如下：

请不要修改以下示例数据中任意 key 名称（如 events、key、name、description 等），否则系统将无法识别，无法导入数据

```json
{
  "events": [
    {
      "key": "webhook",
      "name": "webhook",
      "description": ""
    },
    {
      "key": "webhookb",
      "name": "webhookb",
      "description": ""
    }
  ],
  "event_variables": [
    {
      "key": "webhook_variable_test_string_1",
      "name": "Webhook测试字符串变量1",
      "valueType": "String",
      "description": ""
    },
    {
      "key": "queryTimeRange",
      "name": "查询时间范围",
      "valueType": "Int",
      "description": ""
    }
  ],
  "user_variables": [
    {
      "key": "ml02",
      "name": "ml测试02",
      "valueType": "String",
      "description": "21111111111333312333333"
    },
    {
      "key": "lyce",
      "name": "ly测试",
      "valueType": "String",
      "description": ""
    }
  ],
  "bind_event_variables": [
    {
      "key": "webhook",
      "attributes": [
        {
          "key": "webhook_variable_test_string"
        }
      ]
    },
    {
      "key": "webhookb",
      "attributes": [
        {
          "key": "webhook_variable_test_string"
        },
        {
          "key": "webhook_variable_test_integer"
        }
      ]
    }
  ]
}
```

| 数据类型             | 含义               | 参数        | 含义                                                           |
| -------------------- | ------------------ | ----------- | -------------------------------------------------------------- |
| events               | 事件               | key         | 标识符（允许大小写英文、数字、以及下划线，并且不能以数字开头） |
| ​                    | ​                  | name        | 展示名称                                                       |
| ​                    | ​                  | description | 描述                                                           |
| event_variables      | 事件属性           | key         | 标识符（允许大小写英文、数字、以及下划线，并且不能以数字开头） |
| ​                    | ​                  | name        | 展示名称                                                       |
| ​                    | ​                  | valueType   | 数据类型（Int、String、Double）                                |
| ​                    | ​                  | description | 描述                                                           |
| user_variables       | 用户属性           | key         | 标识符（允许大小写英文、数字、以及下划线，并且不能以数字开头） |
| ​                    | ​                  | name        | 展示名称                                                       |
| ​                    | ​                  | valueType   | 数据类型（Int、String、Double）                                |
| ​                    | ​                  | description | 描述                                                           |
| bind_event_variables | 事件与事件属性绑定 | key         | 事件标识符                                                     |
| ​                    | ​                  | attributes  | key 为事件属性的标识符                                         |

### 导入元数据[](#dao-ru-yuan-shu-ju)

导入元数据的格式请见导出元数据中输出的 JSON

```sh
python3 meta_importer.py -m import_meta \
--file <文件名>
```

file：可选参数，指定导入元数据所在的文件；

其他说明：

导入元数据按导入内容的顺序执行，每项内容的校验规则同其单项的校验规则；

若其中一项内容执行失败，则程序退出，该项后面的内容停止执行，该项前面已导入的内容立即生效；

可将执行失败的内容重新编辑后再次导入，相同的内容更新而不创建；
