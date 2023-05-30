---
id: global_setting
sidebar_position: 10
---

# 全局参数

## 简介[](#jian-jie)

Growing增长平台产品为了能在不同资源配置的硬件上，针对不同的业务分析使用场景及响应速度发挥出最大的效用，放开了全局参数的设置。每个产品功能根据需要，可将约束条件配置在全局参数中，以支持手动调整。比如创建虚拟事件时，支持选用事件的数量默认不超过20个，可根据需要调整参数修改默认值，以突破默认限制。

## 功能说明[](#gong-neng-shuo-ming)

访问入口：元数据管理 -> 全局参数

- 浏览模式

![picture 1](/img/e745345c7315330d502dbdb98020520b444ade854056eea73ef5b38ded98f1bf_pic_1667298791562_2022-11-01.png)  


| 参数  | 默认值  |  说明  |
| --- | --- | --- |
| virtual_event_eventslimit | 20 | 创建虚拟事件时，可选用事件的数量限制。单位：个 |
| virtual_variable_sqllimit | 2000 | 创建虚拟属性时，编写的SQL的长度限制。单位：字符 |
| realtime_event_timelimit | 2 | 数据校验->事件实时查询 查询近期事件的周期，默认近2小时。单位：小时 |
| session_history_days | 180 | 元数据管理->Session管理，创建自定义Session时支持回溯历史数据的周期。单位：天 |
| session_event_limit | 5 | 元数据管理->Session管理，创建自定义Session时支持选用的事件数量。单位：个 |

注：更多参数请联系技术支持咨询。

- 编辑模式

点击“编辑”按钮，切换为编辑模式。编辑模式下可“取消”或“保存”。

![picture 2](/img/58d397adfb97d00d48ba9e0c252f7f1be2e1db870a8aebd65fb353698569cca3_pic_1685426906805_2023-05-30.png)  

注：编辑模式下请按照JSON格式来编写。