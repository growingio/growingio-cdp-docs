---
id: realtime-audit
sidebar_position: 1
---

# 事件实时查询

## 简介[](#jian-jie)

通过SDK埋点或者历史数据上传进入系统中数据，均可以通过该模块去查询数据的详情，检验数据是否正确，是否完整


## 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

有数据集成权限的用户，如无权限请联系**管理员**

该功能限制30天内的数据，最多可查询300条。


## 功能说明[](#gong-neng-shuo-ming)

### 进入事件实时查询页面[](#jin-ru-shi-jian-shi-shi-cha-xun-ye-mian)

* 默认展示最新的10条数据
    
* 按照服务器接收时间倒序排列
    
![](/img/assets-M2qbZInaXgdm8kkNosp-MhX5FSRxN2LZi8DcOJV-MhXA8ehYRVYHH47S9Q41629439686.png)

进入功能主页


### 查询指定用户的事件数据[](#cha-xun-zhi-ding-yong-hu-de-shi-jian-shu-ju)

* 搜索框中填入所需要搜索的用户，如多个用户用“,”分隔，例如 11,12
    
* 查询结果最多共300条，按照服务器接收时间倒序排列
    
* 考虑到用户的使用场景，使用频率，查询性能，限制查询最大时间范围为过去30天内的事件数据

![](/img/assets-M2qbZInaXgdm8kkNosp-MhXAgZa1AJ0HVQQFrj1-MhXBLoxrzk4kCYlG57bimage.png)

搜索单用户事件数据
