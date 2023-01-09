---
id: app-integrate-management
sidebar_position: 1
---

# 集成应用管理

## 简介

GrowingIO 为开放架构，支持您将利用 GrowingIO 采集的用户行为数据做二次开发，并将开发的产品应用集成进来形成统一访问的门户。
![图 1](/img/workbench-entegrate_app-integrate-management.png)  

## 功能说明

功能管理入口：【开放平台】 - 【集成应用管理】

### 创建应用

![![创建新的应用](/img/9bbcc3e77adb7e64962ee19ecb7cf2a7f0546c1205817c59bd5d5cfddb0ab955_pic_1639971163802_2021-12-20.png) 1](/img/create-app_app-integrate-management.png)  

| 信息项   | 含义                                                                                   |
| -------- | -------------------------------------------------------------------------------------- |
| 应用名称 | 设置应用展示的名称                                                                     |
| 应用描述 | 设置应用展示的描述                                                                     |
| 应用地址 | 设置应用被打开的首页地址。如：[https://www.growingio.com/](https://www.growingio.com/) |
| 回调地址 | 设置登录后获取用户信息的接口地址                                                       |
| 项目角色 | 授权该应用到项目角色的用户 |使用，支持选择多个角色；不选择时，表示开放给所有角色
| 展示类型 | 设置应用被打开时，页面是否带顶部导航                                      |
| 状态     | 应用的展示状态。未上线时，不展示在项目工作台的“集成应用”区域。                    |

#### 回调地址的使用流程

集成应用可以使用**分析云**的单点账户体系，获取登录用户的信息，在应用做用户权限管控。获取登录用户信息的流程步骤如下：

##### step 1：获取授权码

判断应用处于非登录状态，重定向到如下 URL，以获取授权码

```
https://{分析云的host}/oauth/authorize?client_id={给应用颁发client_id}&response_type=code
```

##### step 2：获取 access_token

回调地址解析出 URL 参数中的 code 值，调用如下接口获取 access_token

```
https://{分析云的host}/oauth/token?grant_type=authorization_code&code={code值}&client_id={给应用颁发的client_id}&client_secret={给应用颁发的secret}
```

返回值样例：

```json
{
  "access_token": "94a51e08-232d-4352-a52b-3a548a6e18d1",
  "token_type": "bearer",
  "refresh_token": "ad95ec5a-bf65-4007-a941-7ba3aca80473",
  "scope": "admin"
}
```

##### step 3：获取用户信息

利用 access_token，调用如下接口获取用户信息

```
https://{growing产品的host}/userinfo?access_token={access_token值}
```

返回值样例：

```json
{
  "id": "7RDYaeDA",
  "name": "xxx@growingio.com",
  "source": "ldap",
  "identity": "xxx@growingio.com",
  "createdAt": "2021-09-16T08:01:39.322",
  "disabled": false,
  "lastVisitAt": "2021-12-24T08:37:54.57729"
}
```



### 应用预览

点击已创建的应用，弹出该应用的详情页。在详情页中点击“进入应用”按钮，即可预览该应用的展示样式。

![图 3](/img/appdetail_app-integrate-management.png)  

#### 认证信息

对于创建的应用，分析云颁发其客户端 client_id 和 secret，便于兑换凭证调用开放接口。您也可以通过重置按钮来刷新认证信息。
备注：应用的上/线状态，不影响凭证兑换。

### 调整应用展示顺序

点击“展示顺序”按钮，弹出所有已创建的应用列表，鼠标移动到应用前的 6 点图标可拖动应用重新排序，点击“确定”后保存新的顺序。

![](/img/appsort_app-integrate-management.png) 

### 删除应用

点击某个应用卡片右上角的3点图标，弹窗中点击“删除”按钮可删除该应用。

![图 5](/img/appdelete_app-integrate-management.png)  

