---
id: utm-management
sidebar_position: 1
---

# 活动管理


## 简介[](#jian-jie)

管理广告投放的活动信息，包括投放的UTM参数，生成的短链、二维码等。

![](/img/qudaoguanli6.png)

## 功能说明[](#gong-neng-shuo-ming)

### 实例列表

在配置管理中，所有生效的实例都是一套活动管理的载体。

![picture 13](/img/762c7cc27a2aed8047d3f01b5caa25c4b1718d763aef09c6e648b4b2f40a7819_pic_1660117626907_2022-08-10.png)  


### 活动管理

点击实例列表中的某行实例的名称，进入该实例下的活动管理页。

![picture 14](/img/82f5bbdf501f34340537c53bb190013ee2c59289ec589ff072c0a89ae9cdc8fd_pic_1660117717257_2022-08-10.png)  


#### 新建活动

点击“新建活动”按钮，弹出新建窗口。

![](/img/qudaoguanli7.png)

注：新建表单包含的元素，见配置管理中该实例的配置项form

#### 活动详情

点击某活动行，进入该活动的详情页。

![](/img/qudaoguanli8.png)

注：活动详情页的字段，见配置管理中该实例的配置项detail

#### 编辑活动

点击活动详情页中的“编辑”按钮，弹出编辑窗口。

![picture 15](/img/f48d01c247eb87debed13faaa825c5f32ad8ba77cb25b14c41fb82ffe6192358_pic_1660117945188_2022-08-10.png)  


#### 导出活动

点击“导出活动”按钮，可导出当前页或所有页的活动信息到文件。

![picture 16](/img/1377f85cd144b3e0e6fc7989e22b297695555d78dc3518ce0f844739e737a50c_pic_1660118015435_2022-08-10.png)  

注：导出活动的字段，见配置管理中该实例的配置项export

#### 导入活动

点击“导入活动”按钮，进入导入页面。

![picture 17](/img/69084d029f2f1285af36e7a4aa008db7e0564e22a7d8a4ef27fa4a66dace31d9_pic_1660118184093_2022-08-10.png)  

点击“下载模板”，可下载excel文件。

![picture 18](/img/031906b0063e278984a02fd71be6045c09722791c0bd6104bacc6af4fd7bf576_pic_1660118337159_2022-08-10.png)  

填写模板文件后，点击“点击上传或拖拽文件到此区域”上传本地文件后导入。

![picture 19](/img/147cfc2ebf57960850ae417d2445379c36ed7d9d295053325dbf1d905d2523cb_pic_1660120452601_2022-08-10.png)  

上传文件并校验成功后，进一步选择为导入活动使用的短链通道或唯独吗通道，最后点击“保存并创建”完成导入。

#### 同步维度表

点击“同步维度表”，可将所有页的活动信息自动同步到实例配置中指定的维度表。


### 相关规则说明

#### utm_term的生成规则

utm_term是组合生成的，生成规则为utm_term_1、utm_term_2...utm_term_N按顺序以短横线“-”拼接得到。

比如：utm_term_1 = A、utm_term_2 = B、utm_term_3 = C、utm_term_4 = D

则生成的utm_term为：A-B-C-D

注：更多配置信息见配置实例中的form部分。

#### 短链通道的接口要求

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


#### 二维码通道的接口要求

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