---
id: minip-data-definition
sidebar_position: 3
---

# 小程序端数据定义

## 圈选准备[](#quan-xuan-zhun-bei)

### SDK版本:[](#sdk-ban-ben)

将想要圈选的 App 升级到 3.x 及以上的 SDK版本。

如需下载微信小程序无埋点SDK，请点击 [链接](https://assets.giocdn.com/sdk/cdp/3.0/gio-minp.js) 下载。

如需下载WePY框架无埋点SDK，请点击 [链接](https://assets.giocdn.com/sdk/cdp/3.0/gio-minp.esm.js) 下载。

## 圈选操作[](#quan-xuan-cao-zuo)

在 ”**数据 > 事件 > 无埋点事件**” 中点击 “**新建无埋点事件 > {小程序应用}”** 进入小程序圈选准备页面。

如果您的手机与电脑处于同一WIFI网络下，使用手机打开小程序后您的头像便可以出现下用户列表区域。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MQpBeu-sZ8P81oEMV5h%2F-MQpCILNNmbKMS50FBbe%2Fimage.png?alt=media&token=ceb6d072-431d-4883-ae5e-6987c8a6fd3e)

如小程序授权头像等信息，您可以在列表区域看到您的头像和微信昵称；如果未授权以上信息，需要根据您微信的国家、省份、城市，或者手机型号、操作系统、微信版本和小程序版本找到您所操作的设备。

如果您的手机与电脑无法处于同一WIFI网络下，您可以点击 **扫码** 按钮。使用手机扫码成功后，您可以在手机端看到添加IP成功提示，之后使用手机打开小程序后您的头像便可以出现下用户列表区域。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MQpBeu-sZ8P81oEMV5h%2F-MQpDqw07iYI5ojMsDOY%2Fimage.png?alt=media&token=a936906b-0022-46fb-b2a3-0b7180545544)

选择您的设备后点击 **开始圈选** ，开始定义无埋点事件。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MQpEdWljs08FPaCzgBA%2F-MQpHQvO3zJhfmakfzMO%2Fimage.png?alt=media&token=67beec6f-41da-439e-990b-a12274c0f4fd)

| 项   | 说明  |
| --- | --- |
| 1   | 实时数据上报区域 |
| 2   | 无埋点数据定义区域 |
| 3   | 数据上报时间 |
| 4   | 数据类型，包含页面浏览、元素点击、输入框修改、表单提交 |
| 5   | 事件状态，包含已定义事件和未定义事件 |
| 6   | 事件名称，仅对已定义事件展示定义名称 |
| 7   | 事件规则，页面浏览事件展示域名、路径和查询条件；元素事件展示名称、位置和跳转链接 |


定义页面

点击 “**页面浏览**” 事件后，进入页面定义流程。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MQpIK0q0whj__-hrfqP%2F-MQpLm4i1NUIC9qK01la%2Fimage.png?alt=media&token=ae22ce49-ec70-4560-aa07-c5d19a0f6c2e)

当定义小程序原生页面时，您可以看到以下配置项：

| 项   | 说明  |
| --- | --- |
| 1   | (必填) 页面名称，请参考“无埋点事件命名规范“ |
| 2   | 页面事件定义业务场景描述 |
| 3   | 所属应用，定义的页面属于哪个应用。该选项不可编辑，默认属于圈选应用 |
| 4   | (必填) 路径，点击定义后默认识别当前页面路径，支持使用通配符 *。 |
| 5   | 路径启用/仅用状态，禁用后定义规则忽略路径变化。默认开启路径识别 |
| 6   | 查询条件，点击定义后默认识别当前页面查询参数，参数值支持使用通配符 *。 |
| 7   | 查看数据，点击后查看定义规则历史数据趋势。 |

小程序域名即为所属应用，因此原生页面不支持定义域名。

点击保存后，保存定义规则，无埋点页面事件创建成功。

> 无埋点页面事件创建成功后，仅能修改事件名称和描述。
> 
> 同一个无埋点页面定义规则全局仅能定义一次。