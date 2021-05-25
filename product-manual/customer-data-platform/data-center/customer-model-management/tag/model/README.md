# 用户标签模型

## 简介：

目前GrowingIO提供了 **五种** **规则标签，**分别为

* [基础指标值](basic.md)
* [最大值/最小值的事件属性](max-nd-min.md)
* [首次/末次的事件属性](first-nd-last.md)
* [列表类的事件属性](list.md)
* [分层标签](rule.md)

![](../../../../../../.gitbook/assets/image%20%28547%29.png)

定义标签时，第一步需要定义标签的名称、标识符、描述 等信息。

{% hint style="success" %}
标识符默认以 tag\_ 开头，用于 [API接口](../../../../../../developer-manual/api-reference/cdp/) 和 [开放数据表](../../../../../../introduction/data-model/) 使用
{% endhint %}

![](../../../../../../.gitbook/assets/image%20%28546%29.png)

第二步需要定义标签计算规则，详情请参考五种规则标签说明。

