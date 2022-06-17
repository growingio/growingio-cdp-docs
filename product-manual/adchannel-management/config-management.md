---
id: config-management
sidebar_position: 3
---

# 配置管理


## 简介[](#jian-jie)

对活动管理中的表单字段、名称管理中类型的范围等进行在线配置，以满足不同业务的投放管理诉求。

![](/img/qudaoguanli1.png)


## 功能说明[](#gong-neng-shuo-ming)

在线配置的内容格式为JSON，编辑并保存后实时生效。

### 编辑

当点击“编辑”按钮时，配置内容切换为可视化编辑模式。编辑模式下，可修改配置内容

#### 新增内容

鼠标移动到组节点上，自动展示添加的小图标

![](/img/qudaoguanli2.png)

#### 编辑/删除内容

鼠标移动到元素上，自动展示编辑和删除的小图标

![](/img/qudaoguanli3.png)


可编辑的组如下：

#### 名称管理的类型

设置名称管理中的类型下拉框的可选值范围

```json
name_types:[
    0:"utm_source"
    1:"utm_campaign"
    2:"utm_medium"
    3:"utm_content"
    4:"utm_term_1"
    5:"utm_term_2"
    6:"utm_term_3"
    7:"utm_term_4"
]
```

#### 活动表单的元素

设置新建活动的表单元素，以及每个元素的类型和可选值范围

```json
form:{
    elements:[
    0:{
        is_select:"0"
        label:"名称"
    }
    1:{
        is_select:"0"
        label:"落地页"
    }
    2:{
        from:"webhooks"
        is_select:"1"
        label:"短链通道"
    }
    3:{
        from:"webhooks"
        is_select:"1"
        label:"二维码通道"
    }
    4:{
        from:"options"
        is_select:"1"
        label:"状态"
        options:[
        0:{
            text:"生效"
            value:"1"
        }
        1:{
            text:"禁用"
            value:"0"
        }
    ]
    }
    5:{
        from:"name_types"
        is_select:"1"
        label:"utm_source"
    }
    6:{
        from:"name_types"
        is_select:"1"
        label:"utm_campaign"
    }
    7:{
        from:"name_types"
        is_select:"1"
        label:"utm_medium"
    }
    8:{
        from:"name_types"
        is_select:"1"
        label:"utm_content"
    }
    9:{
        from:"name_types"
        is_select:"1"
        label:"utm_term_1"
    }
    10:{
        from:"name_types"
        is_select:"1"
        label:"utm_term_2"
    }
    11:{
        from:"name_types"
        is_select:"1"
        label:"utm_term_3"
    }
    12:{
        from:"name_types"
        is_select:"1"
        label:"utm_term_4"
    }
    ]
}
```

#### 活动列表组

设置活动列表展示的表格列

```json
table:{
    cols:[
        0:"名称"
        1:"状态"
        2:"创建日期"
        3:"创建人"
    ]
}
```

#### 活动详情组

设置活动详情页中展示的字段

```json
detail:{
    cols:[
        0:"名称"
        1:"状态"
        2:"创建日期"
        3:"创建人"
        4:"最近修改人"
        5:"最近修改日期"
    ]
}
```

#### 活动下载组

```json
export:{
    export_all_page:"1"
    export_cols:[
        0:"名称"
        1:"短链"
        2:"二维码"
        3:"状态"
    ]
}
```

export_all_page为1，下载时下载全部页

export_all_page为0，下载时仅下载当前页

export_cols中设置字段将按顺序下载
