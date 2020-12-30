# 创建流程画布

## 1. 流程画布组件

流程画布总共分为四个组件

### 1.1起始组件

「起始组件」主要功能是圈选「目标人群」、「选择流程类型」以及「设置流程画布的起止时间」，下面依次说明这三个设置项的含义。

![](../../../.gitbook/assets/image%20%28388%29.png)

#### **1.1.1 目标人群**

是指满足一定条件后可进入流程画布的基础客群，比如想针对过去一个季度消费额超过5000元的会员进行一波营销活动，那“过去一个季度消费额超过5000元“就是目标人群

#### **1.1.2 选择流程类型**

流程画布支持三种类型——「一次性」、「循环」、「触发型」

「一次性」适用于临时或者不定期的一次性运营活动

「循环」适用于周期性的运营活动，比如每月一次的会员日等

「触发型」适用于基于需要用户满足一定条件或者目标行为才有资格参与的营销活动，比如消费额满多少，或者新用户完成首次下单的奖励活动等

#### **1.1.3 设置流程画布的起止时间**

「一次性」只需设置开始日期及具体时间，含义是在该时间点，符合条件的目标用户会全部进入流程

![](../../../.gitbook/assets/image%20%28390%29.png)

「循环」需要设置上线日期以及下线日期，同时设置触发频率以及执行的时间，含义是在该时间段内，按照指定频率在对应日的对应时间将符合条件的目标用户推入流程

![](../../../.gitbook/assets/image%20%28387%29.png)

「触发型」需要设置上线时间以及下线时间，含义是在该时间段内，目标人群只要触发目标事件就会进入流程

![](../../../.gitbook/assets/image%20%28382%29.png)

#### **1.1.4 是否可重复进入流程**

当选择「循环」或「触发型」流程画布时，支持配置是否允许用户重复进入流程。比如发券场景一般会限制用户在活动期间不能领取多张券，那么就可以配置不允许用户重复进入流程



### 1.2 用户判断组件

用户判断组件的用途是将用户进一步细分，统计意义是在当前时间点往前追溯一段时间内（追溯时间可配置），将符合/不符合指定条件的用户分为两个群体。

![](../../../.gitbook/assets/image%20%28384%29.png)

![](../../../.gitbook/assets/image%20%28383%29.png)



### 1.3 事件触发组件

事件触发组件的用途是将触发指定事件或事件组合（可配置）的用户，实时推入到下一步流程中，适用于需要在用户完成某个事件时，实时的营销活动，比如消费成功后立即返券等。

![](../../../.gitbook/assets/image%20%28386%29.png)

![](../../../.gitbook/assets/image%20%28385%29.png)



### 1.4 活动组件

活动组件主要是配置触达用户的运营活动，目前支持弹窗和webhook。使用webhook，可支持对接企业已有的push、短信、卡券通道等。

同时微信/企业微信/短信等触点我们会逐步更新，敬请期待。

![](../../../.gitbook/assets/image%20%28393%29.png)



## 2 . 创建流程画布

### 2.1 选择新建流程画布

![](../../../.gitbook/assets/image%20%28392%29.png)

### 2.2 填写流程画布名称

进入流程画布后，可填写流程画布名称，如不填写会自动生成一个流程画布id

![](../../../.gitbook/assets/image%20%28395%29.png)

### 2.3 设置起始设置

在流程画布的编辑页面，可见唯一的起始设置器，单击「起始设置」，屏幕右侧会出现设置页面，进行相关设置项配置即可

![](../../../.gitbook/assets/image%20%28394%29.png)

### 2.4 流程组件设置

当完成「起始设置」配置，点击保存后，会重新回到流程画布编辑页面，同时「起始设置」可见配置内容。当将鼠标悬停在「起始设置」组件上时，组件右侧会出现一个「➕」，单击后可见可添加组件。

![](../../../.gitbook/assets/image%20%28389%29.png)

流程组件设置非常灵活，「用户判断」、「事件触发」、「活动配置」均可自由链接，以灵活支持复杂的业务场景

但每一个分支流程最多支持十个组件

### 2.5 目标设置

设置流程画布的目标，用目标完成率来衡量效果。注意，这里目标窗口期是从**用户进入流程**的时间点开始计的。设置完成之后点击保存即可。

![](../../../.gitbook/assets/image%20%28391%29.png)



### 2.6 保存

点击保存，流程画布即保存为草稿状态，可在流程画布管理页面点击并继续进行画布编辑和修改



### 2.7 上线及发布

#### 2.7.1 上线合法性校验

点击上线时，会先进行流程画布设置的合法性校验，如未通过会有相应提示。合法性校验的目的是保持画布上线后可支持，并且有业务意义。


