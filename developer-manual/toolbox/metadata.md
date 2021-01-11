# 元数据创建工具

GrowingIO分析数据模型元数据主要包括事件定义、事件属性定义、用户属性定义等，通过元数据创建工具，可以在命令行模式下直接创建元数据。

元数据创建工具有如下几个功能： 

* 创建事件
* 创建事件属性
* 创建用户属性
* 绑定事件与事件属性
* 导出元数据
* 导入元数据

{% hint style="info" %}
请注意，元数据创建工具不提供删除功能，请创建前确认无误。可以在前端使用管理员账号登录后在数据界面删除不需要的事件或属性。
{% endhint %}

## 创建事件

```text
python3 meta_importer.py -m create_event \
--key <事件名> \
[--name <事件显示名>] \
[--desc <事件描述>] \
```

{% hint style="info" %}
key：必须参数，事件名必须是合法的变量名，仅允许大小写英文、数字、以及下划线，并且不能以数字开头，限长30字符；

name：可选参数，事件显示名可在界面上配置，不加该参数则默认同事件名；

desc：可选参数，事件描述中若有空格则需要加双引号；
{% endhint %}

例如创建事件ViewProd，显示名是“浏览商品”：

```text
python3 meta_importer.py -m create_event \
--key ViewProd \
--name 浏览商品
```

{% hint style="info" %}
若key已存在，则将该事件的name、desc修改为新的输入值
{% endhint %}

## 创建事件属性

```text
python3 meta_importer.py -m create_event_variables \
--key <事件属性名> \
--type <事件属性数据类型> \
[--name <事件属性显示名>] \
[--desc <事件属性描述>] \
```

{% hint style="info" %}
key：必须参数，事件属性名必须是合法的变量名，仅允许大小写英文、数字、以及下划线，并且不能以数字开头，限长30字符；

type：必选参数，事件属性数据类型可选值：string/int/double；

name：可选参数，可在界面上配置，不加该参数则默认同事件属性名；

desc：可选参数，事件属性描述中若有空格则需要加双引号；
{% endhint %}

例如创建事件属性Price，显示名是“价格”，类型是double：

```text
python3 meta_importer.py -m create_event_variables \
--key Price \
--type double \
--name 价格 \
```

{% hint style="info" %}
若key已存在，则将该事件属性的type、name、desc修改为新的输入值
{% endhint %}

## 创建用户属性

```text
python3 meta_importer.py -m create_user_variables \
--key <用户属性名> \
--type <用户属性数据类型> \
[--name <用户属性显示名>] \
[--desc <用户属性描述>] \
```

{% hint style="info" %}
key：必须参数，用户属性名必须是合法的变量名，仅允许大小写英文、数字、以及下划线，并且不能以数字开头，限长30字符；

type：必选参数，用户属性数据类型可选值：string/int/date

name：可选参数，可在界面上配置，不加该参数则默认同用户属性名；

desc：可选参数，用户属性描述中若有空格则需要加双引号；
{% endhint %}

## 绑定事件与事件属性

```text
python3 meta_importer.py -m bind_event_variables \
--key <事件名> \
--attr <绑定事件属性名集合> \
```

{% hint style="info" %}
key：必须参数，若事件不存在则创建；

attr：必须参数，多个属性名之间用英文逗号分隔；
{% endhint %}

例如将ViewProd事件与Price和Color绑定：

```text
python3 meta_importer.py -m bind_event_variables \
--key ViewProd
--attr Price,Color
```

## 导出元数据

导出的元数据可以直接用于导入（下一节介绍）。

```text
python3 meta_importer.py -m export_meta \
--file <文件名> \
```

{% hint style="info" %}
file：必须参数，指定导出元数据的文件名
{% endhint %}

运行后会导出元数据信息，例如：

```text
python3 meta_importer.py -m export_meta \
--file meta.json
```

导出的样例格式如下：

```text
{
    "events": [
        {
            "key": "ViewProd", 
            "name": "浏览商品", 
            "description": ""
        }
    ], 
    "event_variables": [
        {
            "name": "Price", 
            "cname": "价格", 
            "data_type": "double", 
            "description": ""
        }, 
        {
            "name": "Color", 
            "cname": "颜色", 
            "data_type": "string", 
            "description": ""
        }
    ], 
    "user_variables": [
        {
            "name": "PhoneNumber", 
            "cname": "电话号码", 
            "data_type": "string", 
            "description": ""
        }
    ], 
    "bind_event_variables": [
        {
            "event": "ViewProd", 
            "properties": [
                "Price", 
                "Color"
            ]
        }
    ]
}
```

## 导入元数据

导入元数据的格式请见导出元数据中输出的JSON

```text
python3 meta_importer.py -m import_meta \
--file <文件名> \
```

{% hint style="info" %}
file：可选参数，指定导入元数据所在的文件；
{% endhint %}

其他说明：

{% hint style="info" %}
导入元数据按导入内容的顺序执行，每项内容的校验规则同其单项的校验规则；

若其中一项内容执行失败，则程序退出，该项后面的内容停止执行，该项前面已导入的内容立即生效；

可将执行失败的内容重新编辑后再次导入，相同的内容更新而不创建
{% endhint %}

[辅助工具下载](./)

