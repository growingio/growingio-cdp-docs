---
id: create-process
sidebar_position: 1
---

# 创建流程画布

## 流程画布组件[](#1-liu-cheng-hua-bu-zu-jian)

流程画布总共分为四个组件

### 起始组件[](#1-1-qi-shi-zu-jian)

「起始组件」主要功能是圈选「目标人群」、「选择流程类型」以及「设置流程画布的起止时间」，下面依次说明这三个设置项的含义。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLNY7v2EjD4tcURr-iK%2F-MLWrfl8STaFEhmVArrI%2Fimage.png?alt=media&token=c4158059-69fb-4ebf-be3d-c60185abf343)


#### 目标人群[](#1-1-1-mu-biao-ren-qun)

是指满足一定条件后可进入流程画布的基础客群，比如想针对过去一个季度消费额超过5000元的会员进行一波营销活动，那“过去一个季度消费额超过5000元“就是目标人群


#### 选择流程类型[](#1-1-2-xuan-ze-liu-cheng-lei-xing)

流程画布支持三种类型——「一次性」、「循环」、「触发型」

「一次性」适用于临时或者不定期的一次性运营活动

「循环」适用于周期性的运营活动，比如每月一次的会员日等

「触发型」适用于基于需要用户满足一定条件或者目标行为才有资格参与的营销活动，比如消费额满多少，或者新用户完成首次下单的奖励活动等


#### 设置流程画布的起止时间[](#1-1-3-she-zhi-liu-cheng-hua-bu-de-qi-zhi-shi-jian)

「一次性」只需设置开始日期及具体时间，含义是在该时间点，符合条件的目标用户会全部进入流程

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLNY7v2EjD4tcURr-iK%2F-MLWxzasELJSWvzmX4VE%2Fimage.png?alt=media&token=dd0a2d27-c6da-489c-bc28-9ffdde2de16e)

「循环」需要设置上线日期以及下线日期，同时设置触发频率以及执行的时间，含义是在该时间段内，按照指定频率在对应日的对应时间将符合条件的目标用户推入流程

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLNY7v2EjD4tcURr-iK%2F-MLWy4R-_mupwfiy2T1J%2Fimage.png?alt=media&token=d90f7b59-fce4-4c13-b779-79ba9795c428)

「触发型」需要设置上线时间以及下线时间，含义是在该时间段内，目标人群只要触发目标事件就会进入流程

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLNY7v2EjD4tcURr-iK%2F-MLWywkhJnDSAUe53--6%2Fimage.png?alt=media&token=d3f70453-bf06-4d57-b846-6eae3fc1fffe)


#### 是否可重复进入流程[](#1-1-4-shi-fou-ke-zhong-fu-jin-ru-liu-cheng)

当选择「循环」或「触发型」流程画布时，支持配置是否允许用户重复进入流程。比如发券场景一般会限制用户在活动期间不能领取多张券，那么就可以配置不允许用户重复进入流程


### 用户判断组件[](#12-yong-hu-pan-duan-zu-jian)

用户判断组件的用途是将用户进一步细分，统计意义是在当前时间点往前追溯一段时间内（追溯时间可配置），将符合/不符合指定条件的用户分为两个群体。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLWz-hCf5KHGM40rvhL%2F-MLX-cqx_GO9xpAlWqmV%2Fimage.png?alt=media&token=3bc94769-2c4b-4330-9e5c-a47253bc03b5)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLWz-hCf5KHGM40rvhL%2F-MLX-kVR-83XTAJ9eKCL%2Fimage.png?alt=media&token=87627eee-e486-41d3-8ad5-2935c455d1cf)


### 事件触发组件[](#13-shi-jian-chu-fa-zu-jian)

事件触发组件的用途是将触发指定事件或事件组合（可配置）的用户，实时推入到下一步流程中，适用于需要在用户完成某个事件时，实时的营销活动，比如消费成功后立即返券等。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLWz-hCf5KHGM40rvhL%2F-MLX0mUpYaivMQMQTyOK%2Fimage.png?alt=media&token=a43dcdea-5f16-466e-847c-be79dbfb86ee)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLWz-hCf5KHGM40rvhL%2F-MLX0stTKJ-1yaR8BQcV%2Fimage.png?alt=media&token=e5b59a4e-5f17-45cb-b00f-d8e2a7601473)


### 活动组件[](#14-huo-dong-zu-jian)

活动组件主要是配置触达用户的运营活动，目前支持弹窗和webhook。使用webhook，可支持对接企业已有的push、短信、卡券通道等。

同时微信/企业微信/短信等触点我们会逐步更新，敬请期待。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLWz-hCf5KHGM40rvhL%2F-MLX1UAFKR7UD5m8loUp%2Fimage.png?alt=media&token=77f610de-189e-4381-aa80-083952eefb9e)


## 创建流程画布[](#2-chuang-jian-liu-cheng-hua-bu)

### 选择新建流程画布[](#21-xuan-ze-xin-jian-liu-cheng-hua-bu)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLX3B-jDtXdvacgOqsg%2F-MLX3D-Ox5nGi_jkAkXu%2Fimage.png?alt=media&token=e8d5e9ab-6f29-4a8d-ac83-f2fe38913ac6)


### 填写流程画布名称[](#22-tian-xie-liu-cheng-hua-bu-ming-cheng)

进入流程画布后，可填写流程画布名称，如不填写会自动生成一个流程画布id

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLX3B-jDtXdvacgOqsg%2F-MLX3aF_B_gXZQgWLZQ9%2Fimage.png?alt=media&token=0e9d3294-0720-4073-9522-afe40302f04a)


### 设置起始设置[](#23-she-zhi-qi-shi-she-zhi)

在流程画布的编辑页面，可见唯一的起始设置器，单击「起始设置」，屏幕右侧会出现设置页面，进行相关设置项配置即可

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLX3B-jDtXdvacgOqsg%2F-MLX45tPJ5DhVgyHuxqT%2Fimage.png?alt=media&token=113da037-51c5-48ce-873d-85dff6f88c71)


### 流程组件设置[](#24-liu-cheng-zu-jian-she-zhi)

当完成「起始设置」配置，点击保存后，会重新回到流程画布编辑页面，同时「起始设置」可见配置内容。当将鼠标悬停在「起始设置」组件上时，组件右侧会出现一个「➕」，单击后可见可添加组件。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLX3B-jDtXdvacgOqsg%2F-MLX4r5mljdVBNUE87fe%2Fimage.png?alt=media&token=0f5703c7-6b4c-43e2-bd8c-00df29d48c09)

流程组件设置非常灵活，「用户判断」、「事件触发」、「活动配置」均可自由链接，以灵活支持复杂的业务场景

但每一个分支流程最多支持十个组件


### 目标设置[](#25-mu-biao-she-zhi)

设置流程画布的目标，用目标完成率来衡量效果。注意，这里目标窗口期是从**用户进入流程**的时间点开始计的。设置完成之后点击保存即可。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLX5T-Lu9zKAQHwbN3j%2F-MLX6P6FQfDBy5-oNEd4%2Fimage.png?alt=media&token=5e6c1055-3959-4264-b64a-9218b7be7558)

​
### 保存[](#26-bao-cun)

点击保存，流程画布即保存为草稿状态，可在流程画布管理页面点击并继续进行画布编辑和修改


### 上线及发布[](#27-shang-xian-ji-fa-bu)

#### 上线合法性校验[](#2-7-1-shang-xian-he-fa-xing-xiao-yan)

点击上线时，会先进行流程画布设置的合法性校验，如未通过会有相应提示。合法性校验的目的是保持画布上线后可支持，并且有业务意义。
