---
id: web-data-definition
sidebar_position: 4
---

# Web端数据定义

## 圈选准备[](#quan-xuan-zhun-bei)

GrowingIO 全量采集用户行为数据，你可以通过「圈选」来定义元素和页面，作为数据分析的基础指标。

事件定义成功后，GrowingIO默认回溯过去7天的数据。

Chrome插件安装：[请参考Chrome插件](/op/v/2.0/product-manual/shu-ju/auto/web/plugin)​

> Hashtag使用说明：
> 
> 如果您的Web页面URL使用了Hashtag，请在加载SDK进行预先配置，请参考 SDK 帮助文档
> 
> ​[JS SDK 0.7.1](https://assets.giocdn.com/sdk/cdp/gio-0.7.1.js) 支持网站应用无埋点数据采集和圈选
> 
​> [JS SDK 0.8](https://assets.giocdn.com/sdk/cdp/gio.js) 支持App Hybrid采集和圈选，支持SPACE

> URL解读：
> 
> URL**示意：**www.xxx.com**/**12345/678/123**?**id=1&ig=2
> 
> **拆分：**域名**/**路径**?**查询条件
> 
> **即** www.xxx.com **为域名，**/12345/678/123 **为路径，**?id=1&ig=2 **为查询条件**

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MI3JC1TzkGK4ILgFhhs%2F-MI3LKmV6eb9KMO66XB6%2Fimage.png?alt=media&token=bf85fe1e-0d60-4a00-8774-f6270ee2a6ab)

## 圈选操作[](#quan-xuan-cao-zuo)

在 ”**数据 > 事件 \> 无埋点事件**” 中点击 “**新建无埋点事件 \> 网页应用”** 进入Web圈选说明页面。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MI484dYvqV6H6DigVNO%2F-MI48_XneKih-e0-1RVK%2Fimage.png?alt=media&token=07f5038e-b145-40f0-aa40-b2eea354e8b1)

无埋点页面定义：需要在Chrome中打开目标页面，在GIO Web Collection插件中完成页面定义。

在Chrome中打开目标页面后唤起插件，开始定义无埋点事件。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPm7AuIljEQznJboTNI%2F-MPmFzMWX7nq960RMxd3%2Fimage.png?alt=media&token=91a8b617-61d1-4e60-ada1-7bb67f9484c3)

| 项   | 说明  |
| --- | --- |
| 1   | 退出登录按钮：点击后退出登录。 |
| 2   | 浏览模式/定义模式：点击后切换圈选模式，定义模式下可圈选页面元素。 |
| 3   | 定义页面按钮：点击后开始页面定义点击 |

页面定义

点击“**定义页面**“后，进入页面定义流程。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPm7AuIljEQznJboTNI%2F-MPmHgsT5hte9vxGizRS%2Fimage.png?alt=media&token=e1f85a9b-c799-4f51-8dc9-7ba628ac31eb)

| 项   | 说明  |
| --- | --- |
| 1   | (必填) 页面名称，请参考“无埋点事件命名规范“ |
| 2   | 页面事件定义业务场景描述 |
| 3   | (必填) 域名，点击定义后默认识别当前页面域名，支持使用通配符 *。 |
| 4   | (必填) 路径，点击定义后默认识别当前页面路径，支持使用通配符 *。 |
| 5   | 路径启用/仅用状态，禁用后定义规则忽略路径变化。默认开启路径识别 |
| 6   | 查询条件，点击定义后默认识别当前页面查询参数，参数值支持使用通配符 *。 |
| 7   | 添加查询条件，点击后添加新的查询条件定义。 |
| 8   | 查看数据，点击后查看定义规则历史数据趋势。 |

点击保存后，保存定义规则，无埋点页面事件创建成功。

无埋点页面事件创建成功后，仅能修改事件名称和描述。

同一个无埋点页面定义规则全局仅能定义一次。

元素定义

在Chrome中打开目标页面，选择 定义模式 后可以看到已定义的元素被高亮展示。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPm7AuIljEQznJboTNI%2F-MPmIMqH4af4pni60aic%2Fimage.png?alt=media&token=0d9e7ee9-0a17-4384-b8f5-49270b65ef4f)

可以通过 启用/禁用 开关打开或关闭已定义元素的高亮功能。

在定义模式下，点击 **网页元素** 后，进入元素定义流程。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPm7AuIljEQznJboTNI%2F-MPmJ2x8H3ZSAvzjIKSZ%2Fimage.png?alt=media&token=dc09868f-44f8-4954-b84a-3b9f8ba3ba9f)

| 项   | 说明  |
| --- | --- |
| 1   | (必填) 元素名称，请参考“无埋点事件命名规范“ |
| 2   | 元素事件定义业务场景描述 |
| 3   | (必填) 所属页面，选择元素所属页面。 |
| 4   | 限制条件，支持限制元素内容、元素位置和跳转链接。 |
| 5   | 查看数据，点击后查看定义规则历史数据趋势。 |
| 6   | 手动模式，支持手动选择xpath路径并定义元素事件。 |

点击保存后，保存定义规则，无埋点元素事件创建成功。

无埋点元素事件创建成功后，仅能修改事件名称和描述。

同一个无埋点元素定义规则全局仅能定义一次。

#### 限定条件[](#xian-ding-tiao-jian)

* 元素内容

用户可以通过勾选和取消勾选限定是否匹配元素内容。

用户鼠标hover元素内容后出现编辑按钮，点击编辑按钮后可修改匹配的元素内容。支持精准匹配和模糊匹配两种模式。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPm7AuIljEQznJboTNI%2F-MPmJBj_d6KXgXkAEn9a%2Fimage.png?alt=media&token=f940f770-2985-4b09-a912-2e6e0cc6732d)

* 元素位置

用户可以通过勾选和取消勾选限定是否匹配元素位置。

勾选后限制元素位置为当前定义元素位置，取消勾选后不限制元素位置，定义事件包含所有同类元素。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkwyoBJwxZjzm0JPEH%2F-MLkyjvMrSd3ElQD8PWu%2Fimage.png?alt=media&token=cfdea064-6914-451d-8ebb-65911e283ccd)

* 跳转链接

用户可以通过勾选和取消勾选限定是否匹配跳转链接。

用户鼠标hover跳转链接后出现编辑按钮，点击编辑按钮后可修改匹配的跳转链接。支持使用通配符 *。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MPm7AuIljEQznJboTNI%2F-MPmJJgTxGNWgb5RiKeJ%2Fimage.png?alt=media&token=d28cacec-6a2b-44a1-ab3e-679d81ee3bfd)

仅当元素存在名称、位置、跳转链接时，才支持限制以上三种元素信息。

#### 手动模式[](#shou-dong-mo-shi)

点击 “**打开手动模式**“ 后，用户可以自定义元素路径(xpath)。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkwyoBJwxZjzm0JPEH%2F-MLkzE_6EwVdx8w38qA8%2Fimage.png?alt=media&token=9e843ef5-e9a1-437f-bfbd-d169dfb7cc9a)

## 使用案例[](#shi-yong-an-li)

### 案例一：定义GrowingIO官网首页页面浏览事件[](#an-li-yi-ding-yi-growingio-guan-wang-shou-ye-ye-mian-liu-lan-shi-jian)

步骤一：在Chrome中打开 www.growingio.com，进入GrowingIO官网首页。

步骤二：点击“**定义页面**“按钮，进入页面定义流程。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MI4Vb5vtY0zqj-qsw3a%2F-MI4ZMisFEml47IhSozL%2Fimage.png?alt=media&token=47d5c20b-3e52-44cd-aa43-02ed98d18e56)

步骤三：输入页面名称“页面_官网首页"，输入描述"GrowingIO官网首页"，点击保存完成页面定义。

### 案例二：定义GrowingIO官网下所有页面[](#an-li-er-ding-yi-growingio-guan-wang-xia-suo-you-ye-mian)

步骤一：在Chrome中打开 www.growingio.com，进入GrowingIO官网首页。

步骤二：点击“**定义页面**“按钮，进入页面定义流程。

步骤三：禁用路径匹配按钮

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MI4Vb5vtY0zqj-qsw3a%2F-MI4_Fr1kGVlOmt0y6o3%2Fimage.png?alt=media&token=19805dce-1cd1-4fb1-8e51-8241bab45508)

此时定义的页面是 www.growingio.com 域名下的全部页面

步骤四：输入页面名称“页面_官网(全部页面)"，输入描述"GrowingIO官网下全部页面"，点击保存完成页面定义。

案例三：定义GrowingIO官网行业解决方案详情页[](#an-li-san-ding-yi-growingio-guan-wang-hang-ye-jie-jue-fang-an-xiang-qing-ye)

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MI4Vb5vtY0zqj-qsw3a%2F-MI4aCsBSm_05ZHaEpR9%2Fimage.png?alt=media&token=392e852c-4088-4fd5-93f1-87056b217e3d)

步骤一：在Chrome中打开 www.growingio.com/solutions/retail-ecommerce，进入GrowingIO官网电商行业解决方案详情页

步骤二：点击“**定义页面**“按钮，进入页面定义流程。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MI4Vb5vtY0zqj-qsw3a%2F-MI4aeK_6DpZFxFQCiP7%2Fimage.png?alt=media&token=0811626a-fb83-4e18-8386-fb875ed248e9)

步骤三：修改路径规则为 /solutions/*。

该规则的含义为路径规则为以 /solutions/ 开头，后续包含任意字符的路径。

> 电商行业解决方案页面：www.growingio.com/solutions/retail-ecommerce
> 
> 保险行业解决方案页面：www.growingio.com/solutions/insurance
> 
> 运营商行业解决方案页面：www.growingio.com/solutions/telecom-carrier
> 
> 在线旅游行业解决方案页面：www.growingio.com/solutions/online-travel
> 
> 企业服务行业解决方案页面：www.growingio.com/solutions/saas

步骤四：输入页面名称“页面_解决方案详情页"，输入描述"GrowingIO官网下全部解决方案详情页“，点击保存完成页面定义。

### 案例四：定义从百度渠道访问的GrowingIO官网的全部页面[](#an-li-si-ding-yi-cong-bai-du-qu-dao-fang-wen-de-growingio-guan-wang-de-quan-bu-ye-mian)

步骤一：在Chrome中打开 www.growingio.com，进入GrowingIO官网。

步骤二：点击“**定义页面**“按钮，进入页面定义流程。

步骤三：禁用路径匹配按钮；添加查询条件，输入参数为utm_source，参数值为baidu。

步骤四：输入页面名称“页面_官网(baidu来源)"，输入描述"通过baidu搜索访问GrowingIO的全部页面“，点击保存完成页面定义。

### 案例五：定义登录按钮点击事件[](#an-li-wu-ding-yi-deng-lu-an-niu-dian-ji-shi-jian)

步骤一：在Chrome中打开 www.growingio.com，进入GrowingIO官网。

步骤二：点击“**定义模式**“按钮，进入元素圈选模式。

步骤三：在Chrome界面中点击“登录”按钮

步骤四：输入元素名称“点击_官网首页_登录按钮"，选择所属页面为“页面_官网首页“，输入描述”GrowingIO官网首页登录按钮点击“，点击保存完成元素定义。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkz_fOsq6oJExgP3aV%2F-MLl-l5nTrrgF0YEHOGQ%2Fimage.png?alt=media&token=ab98c77e-9ec3-4461-bf5e-3f612ecc9c19)

### 案例六：定义下载点击事件[](#an-li-liu-ding-yi-xia-zai-dian-ji-shi-jian)

步骤一：在Chrome中打开 www.growingio.com，进入GrowingIO官网。

步骤二：点击“**定义模式**“按钮，进入元素圈选模式。

步骤三：在Chrome界面中点击 下载区域

步骤四：输入元素名称“点击_官网首页_下载按钮"，选择所属页面为“页面_官网首页“，取消勾选元素内容、元素位置和跳转链接，输入描述”GrowingIO官网下载，包含白皮书、分析手册、帮助文档“，点击保存完成元素定义。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MLkz_fOsq6oJExgP3aV%2F-MLl0Q_2fjgsics-pTOv%2Fimage.png?alt=media&token=a2c8e95f-8354-4292-883b-f16ad444bd33)

## 常见问题[](#chang-jian-wen-ti)

### 定义查询参数的计算规则是什么？[](#1-ding-yi-cha-xun-can-shu-de-ji-suan-gui-ze-shi-shi-mo)

定义查询参数后，计算规则为包含该查询参数的全部页面。

举例：

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MI4cwVOEHy3FxkkwvnV%2F-MI4dYM-koVxRCS-dGWD%2Fimage.png?alt=media&token=7e4fbef6-e127-42c8-a408-41a87774adaa)

该规则定义的页面是，域名为 www.growingio.com，不限制路径，查询参数包含 utm_source 且参数值为 baidu 的全部页面。

因此该页面规则包含页面 www.growingio.com/cdp?utm_source=baidu&keyword=growingio

不包含页面 www.growingio.com/product?keyword=growingio

### 为什么查询参数值与URL输入框中不一致？[](#2-wei-shi-mo-cha-xun-can-shu-zhi-yu-url-shu-ru-kuang-zhong-bu-yi-zhi)

在Chrome中打开页面 www.growingio.com?city=%e5%8c%97%e4%ba%ac 后，我们可以在URL输入框看到页面路径为 www.growingio.com?city=北京。

此时“定义页面“后，我们可以看到插件中识别的路径规则为

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MI4cwVOEHy3FxkkwvnV%2F-MI4exmv30XpW219Uevx%2Fimage.png?alt=media&token=2cef3e82-dda3-442d-be08-f53e4c564f4e)

此时插件中识别的查询参数与URL输入框中参数不一致。

原因是浏览器展示时，URL输入框会默认将中文进行解码( 即“%e5%8c%97%e4%ba%ac“解码后为“北京“ )，但SDK实际采集上报数据仍为编码路径数据( 即%e5%8c%97%e4%ba%ac )。

为保证页面定义规则与采集数据一致，插件识别域名、路径、查询条件时默认不做解码处理，仍保持原始路径格式。
