---
id: recongnize_task
sidebar_position: 3
---

# 敏感数据发现

## 简介[](#jian-jie)
基于数据的“敏感级别”和“所属分类定义数据识别规则”，识别出企业内的敏感信息。该模块主要是帮助企业发现采集端的敏感信息分布情况以及对敏感信息泄露的安全风险进行统一管理。


## 功能说明[](#gong-neng-shuo-ming)
![picture draw.io](/img/data-black-pic/10.drawio.png)  

## 规则识别
基于【识别规则管理】模块所创建的识别规则，通过任务方式识别当前项目下Event、User、Item三张表内敏感信息的分布情况，支持手动识别任务。


### 新建/创建
用户需填写识别任务名称、选择已创建的识别规则，完成识别任务配置。
![picture xinjian](/img/data-black-pic/11guizeshibie.png)  
![picture chuangjian](/img/data-black-pic/12guizeshibie02.png)  

### 查看示例
用户可查看手动识别任务每次运行的实例情况
![picture chakanshili](/img/data-black-pic/13chakanshili.png)  


### 识别结果
用户可查看识别任务的最新识别结果
![shibiejieguo ](/img/data-black-pic/14jieguo.png)  

### 禁用
用户可删除识别任务
![jinyong ](/img/data-black-pic/15jinyong.png)  

### 删除
用户可删除识别任务
![shanchu ](/img/data-black-pic/16shanchu.png)  


## 常见问题
Q1：创建识别任务的识别规则是怎么定义的？
A1:是在【敏感数据规则-识别规则管理】模块，基于敏感类别所创建的识别规则。
Q2：已经识别完成的任务，怎么重新启动？
A1:当前支持的是手动识别任务，通过手动触发「启用/禁用」按钮管控任务状态。如果已经识别完成想再启用重新识别，用户需要先禁用该任务再点击启用。
