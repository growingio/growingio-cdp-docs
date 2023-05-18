---
id: recongnize_rule_management
sidebar_position: 2
---

# 识别规则管理

## 简介[](#jian-jie)
基于已分级的敏感数据类别以及企业内数据特征进行具体识别规则的设置，用于识别应用内的敏感数据信息。属于敏感数据发现的前置准备工作。


## 功能说明[](#gong-neng-shuo-ming)

### 新增/创建
用户可基于企业的安全管控场景，新建基于某个敏感数据类别的识别规则。支持两种方式进行创建，分别是自定义正则和自动匹配。
![picture chuangjian](/img/data-black-pic/05guizeguanli.png)  
![picture chuangjian02](/img/data-black-pic/06zidingyiguize.png)  

·自定义正则
用户需自行写正则表达式规则。选择敏感数据类别、识别方式、识别类型完成识别规则配置。
![picture chuangjian02](/img/data-black-pic/06zidingyiguize02.png)  

·自动匹配
根据敏感类别自动生成正则表达式。用户选择所需的敏感类别完成识别规则配置。
![picture zidingyi](/img/data-black-pic/07peipei02.png)  
![picture zidingyi](/img/data-black-pic/07zidongpipei.png)  

### 编辑
用户可修改识别方式、识别类型以及对应的正则规则。
![shanchu ](/img/data-black-pic/08bianji.png)  

### 删除
用户可删除已创建的识别规则。
![shanchu ](/img/data-black-pic/09shanchu.png)  


## 常见问题
Q1：自定义规则支持哪些识别方式？
A1:目前可支持正则表达式、通用符应用两种。且用户可在页面查看到每种识别方式的具体书写规范样例。

Q2：自定义正则表达式的识别类型是仅支持单选吗？
A1“可支持多选场景。识别类型可支持内容识别和列名识别，用户可基于需求进行内容或列名识别，也可两个同时配置，识别结果会更精准。

