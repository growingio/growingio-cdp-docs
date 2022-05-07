---
id: app-data-definition
sidebar_position: 2
---

# APP端数据定义

## 圈选准备[](#quan-xuan-zhun-bei)

### SDK版本:[](#sdk-ban-ben)

将想要圈选的 App 升级到 3.x 及以上的 SDK版本。

如需使用App内嵌H5圈选功能，JS SDK需要升级到3.x 及以上版本。

## 圈选操作[](#quan-xuan-cao-zuo)

在 ”**数据 > 事件 > 无埋点事件**” 中点击 “**新建无埋点事件 > {App应用}”** 进入App唤醒页面。

![](/img/assets-M2qbZInaXgdm8kkNosp-MPmMF-oMi3YNjkQSnay-MPmPb2Rsc4nM3-9OO97image.png)

使用手机扫码成功唤起App后，开始定义无埋点事件。

![](/img/assets-M2qbZInaXgdm8kkNosp-MPmMF-oMi3YNjkQSnay-MPmR889yZXlnpid6ch7image.png)

| 项   | 说明  |
| --- | --- |
| 1   | 退出圈选按钮：点击后退出圈选。 |
| 2   | 链接状态：显示设备已链接或设备已断开链接 |
| 3   | 定义页面按钮：点击后开始页面定义点击 |
| 4   | 高亮已定义元素：点击后高亮左侧界面中已定义的元素信息，并进入元素定义模式。 |

定义页面

点击“**定义页面**“后，进入页面定义流程。

![](/img/assets-M2qbZInaXgdm8kkNosp-MPmS_5rMtgiubkRmuel-MPmWcfRrxBdtJGCiGH_image.png)

选择需要定义的页面后，点击“**下一步**“。

在App中，一个“页面“的构成可能包含多个「原生页面」和「H5页面」，每个页面(原生/H5)承载着不同功能的元素。

您可以在页面列表中选择页面后，通过左侧高亮区域确认该“页面“是否是目标定义“页面“。

![](/img/assets-M2qbZInaXgdm8kkNosp-MPmS_5rMtgiubkRmuel-MPmakGllDW8BYmIz_sDimage.png)

| 项   | 说明  |
| --- | --- |
| 1   | (必填) 页面名称，请参考“无埋点事件命名规范“ |
| 2   | 页面事件定义业务场景描述 |
| 3   | 所属应用，定义的页面属于哪个应用，如内嵌H5页面。该选项不可编辑，默认属于圈选应用 |
| 4   | (必填) 域名，点击定义后默认识别当前页面域名，支持使用通配符 *。 |
| 5   | (必填) 路径，点击定义后默认识别当前页面路径，支持使用通配符 *。 |
| 6   | 路径启用/仅用状态，禁用后定义规则忽略路径变化。默认开启路径识别 |
| 7   | 查询条件，点击定义后默认识别当前页面查询参数，参数值支持使用通配符 *。 |
| 8   | 查看数据，点击后查看定义规则历史数据趋势。 |

点击保存后，保存定义规则，无埋点页面事件创建成功。

> 无埋点页面事件创建成功后，仅能修改事件名称和描述。
> 
> 同一个无埋点页面定义规则全局仅能定义一次。
