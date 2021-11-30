---
id: property-selector
sidebar_position: 4
---

# 属性筛选

对属性进行过滤的操作

## 简介[](#jian-jie)

属性筛选可以通过一个或多个属性条件的组合来找到想要分析的目标用户或核心关注的事件行为。比如我们希望筛选今天过生日的用户并对这群用户发送生日祝福礼物；或者筛选订单支付金额大于10元的订单，统计有效支付订单数量。

## 名词解释[](#ming-ci-jie-shi)

属性：GrowingIO系统包含事件模型、物品模型、用户模型三类事物模型，属性是描述一个事物与性质的关系。

## 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

适用于事件分析、漏斗分析等多个分析模块。

## 功能说明[](#gong-neng-shuo-ming)

在GrowingIO的分析功能中，当我们看到![](/img/-M2qbZInaXgdm8kkNosp-M9c2ZZ4iwg4xey1Pm5s-M9c4OtusPzzDdQjyYQJimage.png)全局过滤按钮和“属性为”选项时，点击该按钮或选择属性后可以对用户或事件添加过滤条件，具体操作流程如下：

​![](/img/-M2qbZInaXgdm8kkNosp-M9c2ZZ4iwg4xey1Pm5s-M9c4OtusPzzDdQjyYQJimage.png)全局过滤按钮

step 1: 点击按钮后弹出全局过滤弹窗

step 2: 在1处选择事件或用户维度

step 3: 在2处选择计算规则

step 4: 在3处选择筛选维度值

step 5: 点击保存

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M9bybE_pmoK9_6cCY1j%2F-M9c0ez5qHBsoFo3Zh03%2Fimage.png?alt=media&token=2ca008cd-f468-4a3a-a9b1-e1fe67f74c50)

全局过滤弹窗

> 注意：
> 
> 1. 如需添加多个过滤条件可点击“添加过滤条件”按钮
>
> 2. 最多支持添加5个过滤条件
>
> 3. 过滤结果会按"且"逻辑处理多个过滤条件，即同时满足每个过滤条件
    

属性为

step 1: 在1处选择事件或用户维度

step 2: 在2处选择计算规则

step 3: 在3处选择筛选维度值

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M9c4wRhlW1UjBCqhV7w%2F-M9c5gXLP2W-hstSwLIf%2Fimage.png?alt=media&token=c340c606-3fd4-4b6b-8ee9-66c28e6c245e)

属性为

### 筛选条件[](#shai-xuan-tiao-jian)

### 字符串[](#zi-fu-chuan)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M9c6QU8fuVKrk5hv2zN%2F-M9c8-Pj8ix6i-oJHu-W%2Fimage.png?alt=media&token=0b4524ec-4224-4cdd-b08c-d8ea5a434b66)

字符串筛选条件

| 筛选条件 | 描述说明 |
| --- | --- |
| = 等于 | 精准匹配，<br></br>只有属性完全等于输入值时事件才会进入统计分析 |
| != 不等于 | 精准匹配，<br></br>只有属性不等于输入值时事件才会进入统计分析 |
| in 在...范围内 | 精准匹配，<br></br>只有属性完全等于输入的某个值时事件才会进入统计分析 |
| not in 不在范围内 | 精准匹配，<br></br>只有属性不等于输入的任意值时事件才会进入统计分析 |
| like 包含 | 模糊匹配，<br></br>只有属性字段包含输入值时事件才会进入统计分析 |
| not like 不包含 | 模糊匹配，<br></br>只有属性字段不包含输入值时事件才会进入统计分析 |
| 有值  | 属性值不为NULL、空字符串或任意个空格时<br></br>才会进入统计分析 |
| 没值  | 属性值为NULL、空字符串或任意个空格时<br></br>才会进入统计分析 |

注意：除没值外，其它筛选条件均默认在有值条件下进行筛选，即值不为NULL、空字符串或任意个空格

### 整数和小数[](#zheng-shu-he-xiao-shu)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M9c6QU8fuVKrk5hv2zN%2F-M9c93Wfaqi-wfZ6CSrI%2Fimage.png?alt=media&token=0dcec48e-1eb4-4cf6-966b-d0554bd4fdc9)

整数和小数筛选条件

| 筛选条件 | 描述说明 |
| --- | --- |
| = 等于 | 属性数值等于输入数值时事件才会进入统计分析 |
| != 不等于 | 属性数值不等于输入数值时事件才会进入统计分析 |
| < 小于 | 属性数值小于输入数值时事件才会进入统计分析 |
| <= 小于等于 | 属性数值小于等于输入数值时事件才会进入统计分析 |
| \> 大于 | 属性数值大于输入数值时事件才会进入统计分析 |
| >= 大于等于 | 属性数值大于等于输入数值时事件才会进入统计分析 |
| between 区间 | 属性数值介于输入数值区间时事件才会进入统计分析<br></br>如输入值为10到100时，统计区间为\[10,100\] (包含边界值) |
| 有值  | 属性值不为NULL时才会进入统计分析 |
| 没值  | 属性值为NULL时才会进入统计分析 |

注意：除没值外，其它筛选条件均默认在有值条件下进行筛选，即值不为NULL

### 日期[](#ri-qi)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M9c6QU8fuVKrk5hv2zN%2F-M9c9OV9lGJV5GiGRwfF%2Fimage.png?alt=media&token=f36f5ca7-6984-47af-8dc0-61d0e13ccd62)

日期筛选条件

| 筛选条件 | 描述说明 |
| --- | --- |
| = 等于 | 属性日期等于输入日期时事件才会进入统计分析 |
| != 不等于 | 属性日期不等于输入日期时事件才会进入统计分析 |
| < 在某天之前 | 属性日期小于输入日期时事件才会进入统计分析 |
| <= 在某天之前(包含当天) | 属性日期小于等于输入日期时事件才会进入统计分析 |
| \> 在某天之后 | 属性日期大于输入日期时事件才会进入统计分析 |
| >= 在某天之后(包含当天) | 属性日期大于等于输入日期时事件才会进入统计分析 |
| between 区间 | 属性日期介于输入日期区间时事件才会进入统计分析<br></br>如输入日期为2020-05-01和2020-05-05<br></br>统计区间为2020-05-01(包含)至2020-05-05(包含) |
| 相对现在 | （见下方说明） |
| 相对区间 | （见下方说明） |
| 有值  | 属性值不为NULL时才会进入统计分析 |
| 没值  | 属性值为NULL时才会进入统计分析 |

注意：除没值外，其它筛选条件均默认在有值条件下进行筛选，即值不为NULL

#### 相对现在

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-M9cAVOHrFsohkauXBwU%2F-M9cBD5bJ2kT5wDn_rRN%2Fimage.png?alt=media&token=1d5a88f8-158c-451d-94ec-4599fb8295e2)

日期筛选条件 \- 相对现在

过去N天之前：表示当前日期 - N + 1 天(不包含这天)之前的所有日期

> 当前日期：2020年5月10日
> 
> 筛选条件：过去5天之前
> 
> 计算结果：2020年5月6日之前的所有日期，不包含2020年5月6日

过去N天之内：表示当前日期 - N + 1 天(包含这天)之内的所有日期

> 当前日期：2020年5月10日
> 
> 筛选条件：过去5天之内
> 
> 计算结果：2020年5月6日至2020年5月10日之间的所有日期，包含2020年5月6日和2020年5月10日

未来N天之内：表示当前日期 + N - 1 天(包含这天)之内的所有日期

> 当前日期：2020年5月10日
> 
> 筛选条件：未来5天之内
> 
> 计算结果：2020年5月10日至2020年5月14日之间的所有日期，包含2020年5月10日和2020年5月14日

未来N天之后：表示当前日期 + N - 1 天(不包含这天)之后的所有日期

> 当前日期：2020年5月10日
> 
> 筛选条件：未来5天之后
> 
> 计算结果：2020年5月14日之后的所有日期，不包含2020年5月14日

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MA9DjPj_pYHnKQDWb0h%2F-MA9GmmdkKCBmJgWTkaW%2Fimage.png?alt=media&token=c827fc41-9399-419c-9e22-95311bf53069)

过去5天之内 & 未来5天之内

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MA9DjPj_pYHnKQDWb0h%2F-MA9HoSC0Ekm_TDNO3zw%2Fimage.png?alt=media&token=de88c447-70f0-42fc-b4fd-75e7c0988a79)

过去5天之前 & 未来5天之后

注：N = 1, 2, 3, 4 ... ( 正整数 )

#### 相对区间

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MA9Ne-F7PdyzBRKJ7Gs%2F-MA9POTIxusDeV8XDYa0%2Fimage.png?alt=media&token=e2ac7817-417f-4137-973e-8dc1bd13c4b6)

日期筛选条件 \- 相对区间

在过去M天至过去N天之内：表示 当前日期 - M + 1 天(包含)至 当前日期 - N + 1 天(包含) 之间的所有日期

> 当前日期：2020年5月10日
> 
> 筛选条件：过去3天至过去1天之内
> 
> 计算结果：2020年5月8日至2020年5月10日之间的所有日期，包含2020年5月8日和2020年5月10日

即： \[ 当前日期 \- M + 1 , 当前日期 - N + 1 \]

注：M, N = 1, 2, 3, 4 ... ( 正整数 ) 且 M >= N

在未来M天至未来N天之内：表示 当前日期 + M - 1 天(包含)至 当前日期 + N - 1 天(包含) 之间的所有日期

> 当前日期：2020年5月10日
> 
> 筛选条件：未来3天至未来6天之内
> 
> 计算结果：2020年5月12日至2020年5月15日之间的所有日期，包含2020年5月12日和2020年5月15日

即： \[ 当前日期 \+ M - 1 , 当前日期 + N - 1 \]

注：M, N = 1, 2, 3, 4 ... ( 正整数 ) 且 M <= N

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MA9Ne-F7PdyzBRKJ7Gs%2F-MA9S6Zx6es4cxo9wlGw%2Fimage.png?alt=media&token=9210f6ad-8368-441f-85c5-93fe5f7d676d)

过去3天至过去1天之内 & 未来3天至未来6天之内
