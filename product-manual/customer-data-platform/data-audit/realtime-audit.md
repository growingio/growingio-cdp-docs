---
id: realtime-audit
sidebar_position: 1
---

# 事件实时查询

## 简介[](#jian-jie)

通过SDK埋点或者历史数据上传进入系统中数据，均可以通过该模块去查询数据的详情，检验数据是否正确，是否完整


## 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

* 由于是校验实时入库的数据，为了确保查询性能，事件数据仅返回上小时到当前时刻内的数据，单次返回的事件数量最多300条。
* 打开自动刷新时，需要设置用户ID以保障刷新的查询性能

## 功能说明[](#gong-neng-shuo-ming)

### 进入事件实时查询页面[](#jin-ru-shi-jian-shi-shi-cha-xun-ye-mian)

* 默认展示最新的10条数据，超过10条则分页展示
    
* 按照服务器接收时间倒序排列

* 查询结果区域的左侧事件卡片点击后，右侧展示事件详情
    
![](/img/shishichaxun.png)


### 查询指定用户的事件数据[](#cha-xun-zhi-ding-yong-hu-de-shi-jian-shu-ju)

* 用户ID输入框中填入所需要搜索的用户，如多个用户用“,”分隔，例如 zhangsan,lisi
    
* 查询结果最多共300条，按照服务器接收时间倒序排列

![](/img/shishichaxun2.png)

### 查询指定用户的用户属性[](#cha-xun-zhi-ding-yong-hu-de-yong-hu-shu-ju)

* 用户ID输入框中填入所需要搜索的用户，如多个用户用“,”分隔，例如 zhangsan,lisi

* 查询结果区域的左侧卡片点击后，右侧展示用户属性详情
    
![](/img/shishichaxun3.png)

### 查询指定IP/事件的事件数据[](#cha-xun-zhi-ding-IP-shijian-de-shj-jian-shu-ju)

* IP地址、事件标识符输入框中填入需要过滤的值，点击查询获得过滤后的结果
    
![](/img/shishichaxun4.png)


### 设置自动刷新[](#she-zhi-zi-dong-shua-xin)

* 填写用户ID后，设置自动刷新的时间，查询结果则定时请求最新的数据进行展示

* 设置自动刷新后，其他的查询条件不可输入，关闭自动刷新后方可修改
    
![](/img/shishichaxun5.png)
