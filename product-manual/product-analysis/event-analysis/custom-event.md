---
id: custom-event
sidebar_position: 3
---

# 计算指标

## 简介[](#jian-jie)

计算指标可以创建自定义运算规则的指标，对事件发生的人数、次数、事件的数值型属性求和进行四则运算。

计算指标适用的常见场景包括：

* **注册按钮点击率(CTR)：**注册按钮点击次数(人数) / 注册页面浏览次数(人数)
    
* **注册转化率：**注册成功事件的次数(人数) / 注册页面的页面浏览次数(人数)
    
* **人均购买金额**：购买成功事件的金额加和 / 购买成功事件的人数
    
* **净收入**：购买成功事件的金额加和 \- 退款成功事件的金额加和
    
## 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

计算指标仅支持在事件分析中创建并使用，不支持保存，不能应用于其他分析中。

## 功能说明[](#gong-neng-shuo-ming)

### 新建计算指标[](#xin-jian-ji-suan-zhi-biao)

一、在**事件分析** 中 **选择指标**，点击 **“+指标“** 后，在弹窗中选择 **“计算指标 \> 新建计算指标**“，进入创建弹窗。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2Fsync%2Fd08755a073d59bbc64798a93c6115b8867eed487.png?alt=media)

二、在弹窗中新建一个计算指标。

您可以依次操作：

1.  填写指标名称
    
2.  选择参与运算的指标
    
3.  选择完毕后会用指标前的符号（A B C D）代表参与四则运算
    
4.  展示百分比，两位小数，或者整数。默认展示百分比
    
![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2F-MVQkwJRs6eFaHkG2bNA%2F-MVQqn0tCmtE9YaN3nIc%2F%E4%BA%8B%E4%BB%B6%E5%88%86%E6%9E%904.png?alt=media&token=56ea6aa1-c91a-467b-a148-f94ada19dc34)

三、配置完成后，点击应用，保存后，您可以在当前事件分析中应用这个计算指标。

### 计算指标的运算规则[](#ji-suan-zhi-biao-de-yun-suan-gui-ze)

计算指标支持对事件发生的人数、次数、事件的数值型属性求和进行加减混合运算，并支持对加减混合运算的两个数值进行除法运算。

> 举例：
> 
> * 加减混合运算：A - B + C - D
>
> * 除法运算：A / B
>
> * 加减除混合运算：( A + B - C ) / ( D - E + F )
>

如果计算指标仅包含加减混合运算(不包含除法)，指标中所有事件的统计口径必须一致，且与混合运算中第一个事件的统计口径保持一致。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2Fsync%2F80630e6089a13f19e087953ad5d4b14051b3ea90.png?alt=media)

加减运算

如果计算指标包含除法，分子和分母内部统计口径需保持一致，且与分子或分母中第一个事件的统计口径保持一致，分子和分母的统计口径可以不一样。

![](https://3953104361-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-M2qbZInaXgdm8kkNosp%2Fsync%2F217dfcff6e85087910fc2fde1ced45a1da0e7877.png?alt=media)

除法运算

## 常见问题[](#chang-jian-wen-ti)

1. 计算指标的运算逻辑为 A(人数) - B(人数)，计算结果要怎么理解？[](#1-ji-suan-zhi-biao-de-yun-suan-luo-ji-wei-aren-shu-bren-shu-ji-suan-jie-guo-yao-zen-mo-li-jie)

计算指标中对于人数的计算方法为分别计算事件A和事件B的使用人数，然后对两个人数做差。

同理，如果运算逻辑为A(人数) + B(人数)，计算结果为做过事件A的人数加做个事件B的人数，而不是做过事件A或做过事件B的人数去重。
