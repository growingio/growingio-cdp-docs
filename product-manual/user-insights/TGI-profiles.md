---
id: tgi-profiles
sidebar_position: 3
---

# 腾讯画像

## 简介[](#jian-jie)

数据源的丰富性缺乏是绝大多传统客户线上转型过程中的难点，腾讯生态系统中，提供丰富的用户画像可补充部分数据缺失，提供便捷、丰富的用户群体画像洞察，辅助业务人员更精准的决策 。


## 名词解释[](#ming-ci-jie-shi)

* 什么是TGI指数?
    
> Q：什么是TGI指数？
> 
> A：TGI，即_Target Group Index_，指某一群体的某一指标，与总体人群中同一指标比例之比，再乘以100所得的值。

根据不同的业务场景与业务需求，可以对总体人群的范围进行划分。例如，在衡量某一分群在产品内的标签行为习惯倾向，可将产品的总体用户作为总体人群，若想衡量某一个分群在整体行业内的偏好程度，可将腾讯生态内的全体用户作为总体人群。

* TGI指数的数值代表什么意思？
    
在某个偏好中，“此人群” 对比于 “腾讯整体用户” ，是高或低 。 ‌ TGI指数等于100表示平均水平。 当TGI > 120，代表此人群的人比较喜欢这个“标签” ; ‌ 当TGI < 80，代表此人群的人比较不喜欢这个“标签”。

TGI指数计算公式 ：

(目标群体中具有某一特征的群体所占比例/总体中具有相同特征的群体所占比例)*标准数100。

举例：

想知道某一个分群，对于【资讯 \- 健身】的偏好程度 此分群覆盖率 ：83% 腾讯覆盖率 : 56 % TGI = 83% / 56% * 100 = 148.2 由此可知，此群体相比于腾讯生态全体用户，对【资讯 - 健身】的偏好程度更明显。

| 名詞  | 註釋  |
| --- | --- |
| 分群用户数 | GIO 发起查询时的分群用户数 |
| 查询人数 | 上传的ID减去重复的數量 |
| 腾讯识别人数 | 上传用户中，可被腾讯人群数据库识别的用户数量。例如用户上传人群含1w个ID，其中8000个可被识别，则该人群的腾讯识别人数为8000 |
| GIO识别率 | 腾讯识别人数 / 分群用户数 |
| 腾讯识别率 | 腾讯识别人数 / 查询用户数。例如用户上传人群含1w个ID，其中8000个可被识别，则该人群识别率等于80% |


## 功能说明[](#gong-neng-shuo-ming)

### 新建TGI画像[](#xin-jian-tgi-hua-xiang)

点击 **新建腾讯画像** 按钮，进入新建画像页面

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MVoQKu3lR98UoPXdBAU%2F-MVoXEXhmOoD9t518P4V%2F%E8%9E%A2%E5%B9%95%E6%88%AA%E5%9C%96%202021-03-15%20%E4%B8%8B%E5%8D%882.17.33.png?alt=media&token=ee6dd5bf-a9c9-4565-8fd2-87ec55290960)

### 选择分群[](#xuan-ze-fen-qun)

选择系统中已创建好的分群，用于请求腾讯画像信息。

根据用户隐私安全规定，画像信息查询不得低于10000人，因此分群中只可选择分群人数为10000人以上的分群。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2Fsync%2F55c5b743985b471d85c973427c2797ecf167363f.png?alt=media)


### 填写画像信息[](#tian-xie-hua-xiang-xin-xi)

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MVoQKu3lR98UoPXdBAU%2F-MVoWcJdb8mQAvblPNAC%2F%E8%9E%A2%E5%B9%95%E6%88%AA%E5%9C%96%202021-03-15%20%E4%B8%8B%E5%8D%882.15.20.png?alt=media&token=54c57863-6c7d-4a29-bac1-67af4f99d116)


### 选择匹配模式[](#xuan-ze-pi-pei-mo-shi)

选择一种用户标识将分群用户与腾讯生态数据进行匹配，覆盖率高低程度会影响TGI画像精准度。

> 覆盖率 = 分群中有设备号/手机号的人数 / 分群

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MVoQKu3lR98UoPXdBAU%2F-MVoXPbcM2byKa7tRqJU%2F%E8%9E%A2%E5%B9%95%E6%88%AA%E5%9C%96%202021-03-15%20%E4%B8%8B%E5%8D%882.15.20.png?alt=media&token=f41ffd3b-1821-455f-bf9a-cede8162b163)

依据相关用户隐私信息规定，用户画像信息查询不得低于 10000 人


### 选择洞察维度[](#xuan-ze-dong-cha-wei-du)

选择需要分析的洞察维度 ，一次查询最多支持20个。

TGI画像生成后，会从已选洞察维度上与总体用户进行对比，生成每个维度的覆盖率、TGI指数等。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MVoQKu3lR98UoPXdBAU%2F-MVoW5ogLJj7quU9pcD-%2F%E8%9E%A2%E5%B9%95%E6%88%AA%E5%9C%96%202021-03-15%20%E4%B8%8B%E5%8D%882.12.47.png?alt=media&token=76491816-1ec5-44ae-8ef2-72bd25bc96a6)
​

### 数据安全与隐私[](#shu-ju-an-quan-yu-yin-si)

Growing IO 坚守重视用户信息安全及隐私的原则，本功能均在符合国家法规基础上进行开展，具体的隐私保护措施包括且不限于以下几个方面：

* 本功能所有用户信息，缺进行了匿名化、去标识化的处理。
    
* 不提供任何个体数据，最小限度数据结果需 > 10000人。
    
* 输出结果均为基于间接画像数据、结合公开数据建模后的推测值 。
    
* 不提供实时统计功能 。
    
> 基于必要的用户信息保护措施，数据统计结果可能出现等式不成立的可能性，均属正常现象
