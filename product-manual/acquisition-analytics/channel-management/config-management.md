---
id: config-management
sidebar_position: 3
---

# 配置管理

## 简介[](#jian-jie)

对活动管理中的表单字段、名称管理中类型的范围等进行配置，以满足不同业务不同端的活动管理诉求。

## 功能说明[](#gong-neng-shuo-ming)

### 实例管理

支持为多个端创建不同的实例配置信息，以便于活动管理中区分不同端的活动。

#### 实例列表

![picture 7](/img/6b72456a5f59fded0da0d3276f1c7fb4fe157d879ecd8f300a8184398402cc71_pic_1660115844692_2022-08-10.png)  

#### 新建实例

点击“新建实例”按钮，弹出新建窗口。

![picture 8](/img/db0ac5c048c98b8774d7763e9b312255e9b9ff14e8b17ecde396cf32d01935d3_pic_1660115919778_2022-08-10.png)  

注明：状态默认为生效，当修改为禁用时，该实例不被“名称管理”、“活动管理”中使用。

#### 查看实例详情

点击表格中的实例行，查看实例详情。

![picture 9](/img/0741a18f74babe156b077320845501ed491ba3e0ad00f2848c7a7dc76e792b88_pic_1660115984355_2022-08-10.png)  

点击实例详情中的“编辑”按钮，弹出编辑窗口。

![picture 10](/img/f9522e524b76bf1e28ca1e10c634882aca857033ca59fec9eeab3d486eba983d_pic_1660116158291_2022-08-10.png)  




### 实例配置

点击实例表格中的某实例的名称，进入实例的配置内容页。

![picture 4](/img/b792a53cb1f458b178ae675c159f8324c0f5d6621d2710edf0e617859c346494_pic_1660111533883_2022-08-10.png)  

配置内容的格式为JSON，点击“编辑”按钮时，配置内容切换为编辑模式，编辑保存后实时生效。

#### 1、给“名称管理”增加新的类型

在“name_types”部分添加新的类型，支持中英文。比如添加名称为“标签”、“场景”的类型，如下：

```JSON
    "name_types": [
        "utm_source",
        "utm_campaign",
        "utm_medium",
        "utm_content",
        "utm_term_1",
        "utm_term_2",
        "utm_term_3",
        "utm_term_4",
        "标签",
        "场景"
    ],
```

注：内置类型不可删除。内置类型包括：utm_source、utm_campaign、utm_medium、utm_content、utm_term_1、utm_term_2、utm_term_3、utm_term_4

#### 2、给“活动管理”增加新的元素字段

在“form”部分添加新的元素，支持中英文。比如添加名称为“标签”、“场景”的元素，且设值方式为下拉框选择，如下：

```JSON
"form": {
        "elements": [
            {
                "label": "名称",
                "is_select": "0"
            },
            {
                "label": "落地页",
                "is_select": "0"
            },
            {
                "label": "短链通道",
                "is_select": "1",
                "from": "webhooks"
            },
            {
                "label": "二维码通道",
                "is_select": "1",
                "from": "webhooks"
            },
            {
                "label": "状态",
                "is_select": "1",
                "from": "options",
                "options": [
                    {
                        "value": "1",
                        "text": "生效"
                    },
                    {
                        "value": "0",
                        "text": "禁用"
                    }
                ]
            },
            {
                "label": "utm_source",
                "is_select": "1",
                "from": "name_types"
            },
            {
                "label": "utm_campaign",
                "is_select": "1",
                "from": "name_types"
            },
            {
                "label": "utm_medium",
                "is_select": "1",
                "from": "name_types"
            },
            {
                "label": "utm_content",
                "is_select": "1",
                "from": "name_types"
            },
            {
                "label": "标签",
                "is_select": "1",
                "from": "name_types"
            },
            {
                "label": "场景",
                "is_select": "1",
                "from": "name_types"
            }
        ]
    },
```

|  项目   | 描述  |
|  ----  | ----  |
| label  | 元素名称 |
| is_select  | 元素交互控件。0为输入框，1为下拉框 |
| from  | 元素交互控件为下拉框时，定义可选值的来源。name_types为“名称管理”中定义可选值范围，options为自定义 |
| options | 元素交互控件为下拉框，且可选值来源为options时，options的格式为数组。数组元素的内容包含value值和名称显示text|

#### 3、给“活动管理”的表格增加新的列

在“table”部分添加新的列，支持中英文。比如增加“标签”、“场景”列

```JSON
    "table": {
        "cols": [
            "名称",
            "状态",
            "创建日期",
            "创建人",
            "标签",
            "场景"
        ]
    },
```

#### 4、给“活动管理”的活动详情增加新的字段

在“detail”部分添加新的字段，支持中英文。比如增加“标签”、“场景”

```JSON
    "detail": {
        "cols": [
            "名称",
            "状态",
            "创建日期",
            "创建人",
            "最近修改人",
            "最近修改日期",
            "标签",
            "场景"
        ]
    }
```

#### 5、定义活动导出的字段

在“export”部分添加新的字段，支持中英文。比如添加“标签”、“场景”
```JSON
    "export": {
        "export_all_page": "1",
        "export_cols": [
            "名称",
            "短链",
            "二维码",
            "状态",
            "utm_source",
            "utm_medium",
            "utm_campaign",
            "utm_content",
            "utm_term",
            "标签",
            "场景"
        ]
    }
```

|  项目   | 描述  |
|  ----  | ----  |
| export_all_page  | 是否全量导出。0是近导出当前页，1是导出所有页 |
| export_cols | 导出字段 |


#### 6、同步活动信息到维度表

需要先在 维度表管理 中定义维度表，再在配置内容中将维度表的标识符、字段信息关联到活动。

如定义一张标识符为itemtable_0的维度表

![picture 6](/img/099e67be0261c6c9ab8e774022b0a664a9a2ad08a3edb482d25145ddd8441a31_pic_1660114698385_2022-08-10.png)  

给该维度表定义“标签”、“场景”两个字段

![picture 5](/img/7b218f79d0c2f0919d26a3f02c645441e42d93b29c773c0fecf7f6ee6102718a_pic_1660114649068_2022-08-10.png)  


在“import_item”部分定义维度表的关联信息，如下：

```JSON
    "import_item": {
        "item_key": "itemtable_0",
        "item_id": "",
        "item_cols": [
            {
                "name": "标签",
                "key": "itemtable_0_tag"
            },
            {
                "name": "场景",
                "key": "itemtable_0_scene"
            }
        ]
    }
```

|  项目   | 描述  |
|  ----  | ----  |
| item_key  | 维度表的标识符，为空则不会同步 |
| item_id  | 维度表记录的ID，不填写则默认为活动的link_id，填写某字段则用该字段为维度表记录的ID。 |
| item_cols  | 维度表字段与活动字段的映射。name为活动字段，key为维度表字段的标识符 |
