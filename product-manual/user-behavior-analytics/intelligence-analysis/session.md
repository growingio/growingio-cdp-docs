---
id: session
sidebar_position: 9
---

# Session分析

## 简介[](#jian-jie)
和事件分析相比，Session分析是基于会话的分析，支持用户基于实际业务场景，自定义session包含的事件和切割规则，并在独立的分析模块中进行分析。
## 功能说明[](#gong-neng-shuo-ming)

### 新建Session
在数据中心的Session管理里，可以新建Session，Session中至少包含两个事件，默认时间切割是30分钟。可选添加开始事件和结束事件作为session的切割点。
![图 11](/img/4f8da564efc5d80c6d7ba6919d8ab323fd851d408b13556a6731640ca6479e43.png)  
![图 12](/img/13e829c2e33090b5b28c592d48fad1593b85e54bbb70e5dd0fb9b5b531c25e20.png)  

### Session分析
创建Session之后，就可以在Session分析中进行分析了，整体的分析流程和事件分析是基本相同的，区别在于，在Session分析中，首先选择的是需要分析的session，然后选择对Session整体或者Session中的事件进行分析：
![图 13](/img/3f2157fb10ac723fe101c18f7e791e958b6fe50776ea92eddfd0976de886cba6.png)  
