---
id: utm-management
sidebar_position: 1
---

# 活动管理


## 简介[](#jian-jie)

管理广告投放的活动信息，包括投放的UTM参数，生成的短链、二维码等。

![](/img/qudaoguanli6.png)

## 功能说明[](#gong-neng-shuo-ming)

### 新建活动

新建表单包含的元素，见配置管理中的配置项form

![](/img/qudaoguanli7.png)

### 活动详情

活动详情页展示配置管理中设置的字段，配置项为detail

![](/img/qudaoguanli8.png)

### 编辑活动

活动详情页点击“编辑”按钮，进入编辑页。

### 下载活动

支持下载生效活动和全部活动到csv文件。

下载的字段见配置管理中的配置项export

![](/img/qudaoguanli9.png)

## 相关规则说明

### utm_term的生成规则

utm_term是组合生成的，生成规则为utm_term_1、utm_term_2...utm_term_N按顺序以短横线“-”拼接得到。

比如：utm_term_1 = A、utm_term_2 = B、utm_term_3 = C、utm_term_4 = D

则生成的utm_term为：A-B-C-D

### 短链通道的接口要求

请求方式：POST

请求参数：

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| ---- | ---- | ---- | ---- | ------ |
| url   |  String    |  是    |  落地页URL    |   /pages/index/index?&utm_source=searchEngine&utm_medium=baidu&link_id=123   |

返回数据：

| 名称 | 类型   | 描述     |
| ---- | ------ | -------- |
| code   | Int | 返回码。0为成功，其他为失败  |
| msg | String | 接口调用失败的错误信息 |
| url | String | 短链URL |

返回示例：

```
{
    "code"=>0,
    "msg"=>"SUCC",
    "url"=>"weixin://dl/business/?t=XXXXXXXXXXX"
}
```


### 二维码通道的接口要求

请求方式：POST

请求参数：

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| ---- | ---- | ---- | ---- | ------ |
| url   |  String    |  是    |  落地页URL    |   /pages/index/index?&utm_source=searchEngine&utm_medium=baidu&link_id=123   |

返回数据：

| 名称 | 类型   | 描述     |
| ---- | ------ | -------- |
| code   | Int | 返回码。0为成功，其他为失败  |
| msg | String | 接口调用失败的错误信息 |
| url | String | 图片URL |

返回示例：

```
{
    "code"=>0,
    "msg"=>"SUCC",
    "url"=>"http://xxx.com/xxx.jpg"
}
```