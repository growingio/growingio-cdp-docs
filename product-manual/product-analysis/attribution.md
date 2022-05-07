---
id: attribution
sidebar_position: 9
---

# 归因分析

## 简介[](#jian-jie)

运营人员关注产品内运营位（广告banner、推广商品等）的用户点击事件对订单转化的贡献，以便及时调整运营策略达到活动期间最佳的营收，这类场景下，推荐使用归因分析工具。在归因分析中，运营位的点击事件被称为触点事件，提交订单或订单支付等事件被称为目标事件。

目前，支持4种主流的归因模型：

* 首次触点归因：在回溯期内，首次触点转化贡献分配 100%。其余触点分配 0%。
    
* 末次触点归因：在回溯期内，最后一次触点转化贡献分配 100%，其余触点分配 0%。
    
* 线性归因：在回溯期内，一次转化被各触点平均分配。例如用户的一次转化有 5 个触点事件，那么 5 个触点中每个都被分配 20%。
    
* 位置归因：在回溯期内，首次触点分配 40%，末次分配 40%，其余中间各触点平均分配 20%。
    

## 功能说明[](#gong-neng-shuo-ming)

![](/img/assets-M2qbZInaXgdm8kkNosp-Maup1f7wL-Wv1YktAUG-Mav8BRk0ZPK7RyMudtJimage.png)


### 目标事件选择[](#1-mu-biao-shi-jian-xuan-ze)

支持基于代码埋点事件的单选操作。

![](/img/assets-M2qbZInaXgdm8kkNosp-Mav9ENC428NY5Sm8ZUq-MavBKwamnQZ7iIo705vimage.png)


### 目标事件过滤条件[](#2-mu-biao-shi-jian-guo-lv-tiao-jian)

支持事件属性/访问属性/用户属性下的多条件 '且' 过滤。

![](/img/assets-M2qbZInaXgdm8kkNosp-MavCHgGVbJ-7NMUAx6g-MavDA3laRlNDcTDFG5Qimage.png)


### 目标事件计算指标[](#3-mu-biao-shi-jian-ji-suan-zhi-biao)

目标事件的计算指标支持总次数，比如订单支付的总次数，用来作为总贡献值按照归因配置计算到每个触点和直接转化的事件上。


### 触点事件选择[](#4-chu-dian-shi-jian-xuan-ze)

支持代码埋点事件的多选操作。

![](/img/assets-M2qbZInaXgdm8kkNosp-MavE3hfiPKdhtNSJyPq-MavFvceCW42Flioe6m0image.png)


### 触点事件筛选条件[](#5-chu-dian-shi-jian-shai-xuan-tiao-jian)

支持事件属性/访问属性/用户属性下的多条件 '且' 过滤，所选条件作用在每一个触点事件上。


### 关联属性设置[](#6-guan-lian-shu-xing-she-zhi)

支持设置触点事件和目标事件的关联属性，更准确地获得归因结果。比如某用户在商品A上发生的触点，带来商品A的订单支付，通过设置关联属性为商品，则被归因；反之若该用户在商品A发生的触点，订单支付为商品B，当设置了关联属性为商品时，商品B的订单支付不被归因到该触点上。

支持分别为每个触点事件设置与目标事件的关联属性，默认不设，具体请根据运营目标和策略而定。

![](/img/assets-M2qbZInaXgdm8kkNosp-MavE3hfiPKdhtNSJyPq-MavJ9PTKRuHaiHLYEScimage.png)


### 直接转化事件[](#7-zhi-jie-zhuan-hua-shi-jian)

在本次设置的归因参数下，目标事件中未被归因的部分都算作直接转化。当勾选直接转化后，归因结果中展现直接转化的数据，反之则不展现。特别地，当未勾选直接转化时，各触点事件的贡献度为其在所有被归因下的占比，比如两个触点事件A和B，分别带来1次和4次的订单转化，这时不论有多少直接转化，计算A的贡献度为1/(1+4)\*100%=20%，B的贡献度为4/(1+4)\*100%=80%。

![](/img/assets-M2qbZInaXgdm8kkNosp-Max7cunWvA0B7ZtP8eF-MaxbR8lizJE_gPs7K6vimage.png)


### 归因模型选择[](#8-gui-yin-mo-xing-xuan-ze)

支持按照运营评估需求，选择首次触点归因、末次触点归因、线性归因和位置归因中的一种。

![](/img/assets-M2qbZInaXgdm8kkNosp-Max7cunWvA0B7ZtP8eF-MaxbJC5JMiz57homjqyimage.png)


### 归因窗口期设置[](#9-gui-yin-chuang-kou-qi-she-zhi)

* 当天：触点事件和目标事件发生在同一天，且触点事件在目标事件之前发生。
    
* 自定义：支持1~180的分钟/小时/天的回溯期设置，比如设置为10分钟，则目标事件发生之前的10分钟内的触点事件将可能被归因（需结合其他参数，比如关联属性等）。
    
![](/img/assets-M2qbZInaXgdm8kkNosp-MavLx6oncTGFoMQvMSC-MavMEeHz_Nr5lWvm7HBimage.png)


### 目标用户选择[](#10-mu-biao-yong-hu-xuan-ze)

支持选择某个分群的用户作为归因的对象，缩小分析范围。


### 归因结果的属性维度对比设置[](#11-gui-yin-jie-guo-de-shu-xing-wei-du-dui-bi-she-zhi)

* 支持选择某个事件属性/访问属性/用户属性，对归因结果进行细分对比
    
* 仅支持单个维度细分对比
    
* 对比维度在归因表格增加列显示
    
![](/img/assets-M2qbZInaXgdm8kkNosp-Max7cunWvA0B7ZtP8eF-MaxaKeouu8A-zmv0wuzimage.png)


### 归因结果的分群用户对比设置[](#12-gui-yin-jie-guo-de-fen-qun-yong-hu-dui-bi-she-zhi)

支持选择N个分群，对归因结果进行群用户之间的对比。

![](/img/assets-M2qbZInaXgdm8kkNosp-Max7cunWvA0B7ZtP8eF-Maxc-IbxUX-h_X2l-x5image.png)


### 全局过滤[](#13-quan-ju-guo-lv)

支持对目标事件和触点事件设置统一的过滤条件。


### 目标事件发生时间段[](#14-mu-biao-shi-jian-fa-sheng-shi-jian-duan)

支持设置目标事件发生的任意时间段。


### 归因分析结果表格[](#15-gui-yin-fen-xi-jie-guo-biao-ge)

![](/img/assets-M2qbZInaXgdm8kkNosp-MauojUXFSlSVG3ixZ3d-MauouzERCWKPu-HcrK4image.png)

* 触点事件：归因设置中的各触点事件
    
* 总点击量：该行触点在目标事件时间段（外加归因窗口期）内发生点击事件的总次数
    
* 有效转化点击量：总点击量中，被归因的点击数
    
* 有效转化点击率：有效转化点击量/总点击量
    
* {所选目标事件}总次数：该行触点的点击事件带来的被归因的目标事件的总次数（归因模型选择线性和位置归因时计算加权次数）
    
* 贡献度：各触点带来的{目标事件}总次数占所有触点（若勾选了直接转化，则直接转化也将被计算在内）带来{目标事件}总次数的比例
