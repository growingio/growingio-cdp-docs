---
id: realtime-audit
sidebar_position: 1
---

# 事件实时查询

## 简介[](#jian-jie)

通过 SDK 埋点或者历史数据上传进入系统中数据，均可以通过该模块去查询数据的详情，检验数据是否正确，是否完整

## 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

有数据集成权限的用户，如无权限请联系**管理员**

该功能限制 30 天内的数据，最多可查询 300 条。

## 功能说明[](#gong-neng-shuo-ming)

### 进入事件实时查询页面[](#jin-ru-shi-jian-shi-shi-cha-xun-ye-mian)

- 默认展示最新的 10 条数据
- 按照服务器接收时间倒序排列

![picture 1](/img/2f5ed854101be67809b65209201a77d0769a3ca1064c236bd2d3dfad98146907_pic_1654495289820_2022-06-06.png)

进入功能主页

### 查询指定用户的事件数据[](#cha-xun-zhi-ding-yong-hu-de-shi-jian-shu-ju)

- 搜索框中填入所需要搜索的用户，如多个用户用“,”分隔，例如 11,12
- 查询结果最多共 300 条，按照服务器接收时间倒序排列
- 考虑到用户的使用场景，使用频率，查询性能，限制查询最大时间范围为过去 30 天内的事件数据

![](/img/assets-M2qbZInaXgdm8kkNosp-MhXAgZa1AJ0HVQQFrj1-MhXBLoxrzk4kCYlG57bimage.png)

搜索单用户事件数据
