# App端数据定义

## 圈选准备

### SDK版本: 

将想要圈选的 App 升级到 3.x 及以上的 SDK版本。

{% hint style="success" %}
如需使用App内嵌H5圈选功能，JS SDK需要升级到0.8及以上版本。
{% endhint %}

## 圈选操作

在 ”**数据 &gt; 事件 &gt; 无埋点事件**” 中点击 “**新建无埋点事件 &gt; {App应用}”** 进入App唤醒页面。

![](../../.gitbook/assets/image%20%28431%29.png)

使用手机扫码成功唤起App后，开始定义无埋点事件。

![](../../.gitbook/assets/image%20%28435%29.png)

| 项 | 说明 |
| :--- | :--- |
| 1 | 退出圈选按钮：点击后退出圈选。 |
| 2 | 链接状态：显示设备已链接或设备已断开链接 |
| 3 | 定义页面按钮：点击后开始页面定义点击 |
| 4 | 高亮已定义元素：点击后高亮左侧界面中已定义的元素信息，并进入元素定义模式。 |

{% tabs %}
{% tab title="定义页面" %}
点击“**定义页面**“后，进入页面定义流程。

![](../../.gitbook/assets/image%20%28425%29.png)

选择需要定义的页面后，点击“**下一步**“。

{% hint style="success" %}
在App中，一个“页面“的构成可能包含多个「原生页面」和「H5页面」，每个页面\(原生/H5\)承载着不同功能的元素。

您可以在页面列表中选择页面后，通过左侧高亮区域确认该“页面“是否是目标定义“页面“。
{% endhint %}

![](../../.gitbook/assets/image%20%28434%29.png)

| 项 | 说明 |
| :--- | :--- |
| 1 | \(必填\) 页面名称，请参考“无埋点事件命名规范“ |
| 2 | 页面事件定义业务场景描述 |
| 3 | 所属应用，定义的页面属于哪个应用，如内嵌H5页面。该选项不可编辑，默认属于圈选应用 |
| 4 | \(必填\) 域名，点击定义后默认识别当前页面域名，支持使用通配符 \*。 |
| 5 | \(必填\) 路径，点击定义后默认识别当前页面路径，支持使用通配符 \*。 |
| 6 | 路径启用/仅用状态，禁用后定义规则忽略路径变化。默认开启路径识别 |
| 7 | 查询条件，点击定义后默认识别当前页面查询参数，参数值支持使用通配符 \*。 |
| 8 | 查看数据，点击后查看定义规则历史数据趋势。 |

点击保存后，保存定义规则，无埋点页面事件创建成功。

{% hint style="success" %}
无埋点页面事件创建成功后，仅能修改事件名称和描述。

同一个无埋点页面定义规则全局仅能定义一次。
{% endhint %}
{% endtab %}

{% tab title="定义元素" %}
点击开启“**高亮已定义元素**“后可以看到已定义的元素被高亮展示。

![](../../.gitbook/assets/image%20%28447%29.png)

{% hint style="success" %}
可以通过 启用/禁用 开关打开或关闭已定义元素的高亮功能。
{% endhint %}

点击 **网页元素** 后，进入元素定义流程。

![](../../.gitbook/assets/image%20%28444%29.png)

| 项 | 说明 |
| :--- | :--- |
| 1 | \(必填\) 元素名称，请参考“无埋点事件命名规范“ |
| 2 | 元素事件定义业务场景描述 |
| 3 | 所属应用，定义的页面属于哪个应用，如内嵌H5页面。该选项不可编辑，默认属于圈 |
| 4 | \(必填\) 所属页面，选择元素所属页面。 |
| 5 | 限制条件，支持限制元素内容、元素位置和跳转链接。 |
| 6 | 查看数据，点击后查看定义规则历史数据趋势。 |

点击保存后，保存定义规则，无埋点元素事件创建成功。

{% hint style="success" %}
无埋点元素事件创建成功后，仅能修改事件名称和描述。

同一个无埋点元素定义规则全局仅能定义一次。
{% endhint %}

#### 限定条件

* 元素内容

用户可以通过勾选和取消勾选限定是否匹配元素内容。

用户鼠标hover元素内容后出现编辑按钮，点击编辑按钮后可修改匹配的元素内容。支持精准匹配和模糊匹配两种模式。

![](../../.gitbook/assets/image%20%28422%29.png)

* 元素位置

用户可以通过勾选和取消勾选限定是否匹配元素位置。

勾选后限制元素位置为当前定义元素位置，取消勾选后不限制元素位置，定义事件包含所有同类元素。

![](../../.gitbook/assets/image%20%28414%29.png)

{% hint style="success" %}
仅当元素存在名称、位置时，才能支持限制以上三种元素信息。
{% endhint %}
{% endtab %}
{% endtabs %}
