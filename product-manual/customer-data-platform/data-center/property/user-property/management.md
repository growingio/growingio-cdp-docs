# 用户属性管理

## 归因模型 - 最终（Final） <a id="gui-yin-mo-xing"></a>

GrowingIO的用户属性采用最终归因的计算模型，即如果一个用户同一个用户属性上传过多个不同数值，按时间排序后距今最近一次上传的用户属性值会保留下来。

### 案例

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x65E5;&#x671F;</th>
      <th style="text-align:left">&#x884C;&#x4E3A;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Day 1</td>
      <td style="text-align:left">&#x5C0F;&#x660E;&#x4F7F;&#x7528; &#x8BBE;&#x5907;X &#x8BBF;&#x95EE;GrowingIO&#x5B98;&#x7F51;</td>
    </tr>
    <tr>
      <td style="text-align:left">Day 2</td>
      <td style="text-align:left">
        <p>&#x5C0F;&#x660E;&#x4F7F;&#x7528; &#x8BBE;&#x5907;X &#x767B;&#x5F55;GrowingIO&#x5B98;&#x7F51;&#xFF0C;&#x586B;&#x5199;&#x804C;&#x4F4D;&#x4E3A;
          &#x6570;&#x636E;&#x5206;&#x6790;&#x5E08;</p>
        <p>( &#x5373;&#x4E0A;&#x4F20;&#x7528;&#x6237;&#x5C5E;&#x6027; &#x804C;&#x4F4D;
          = &#x6570;&#x636E;&#x5206;&#x6790;&#x5E08; )</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Day 3</td>
      <td style="text-align:left">&#x5C0F;&#x660E;&#x4F7F;&#x7528; &#x8BBE;&#x5907;X &#x767B;&#x5F55;GrwoingIO&#x5B98;&#x7F51;&#xFF0C;&#x4FEE;&#x6539;&#x804C;&#x4F4D;&#x4E3A;
        &#x4EA7;&#x54C1;&#x7ECF;&#x7406;</td>
    </tr>
  </tbody>
</table>

说明：

Day 1：此时在GrowingIO系统中，小明的用户属性职位为空

Day 2：此时在GrowingIO系统中，小明的用户属性职位为“数据分析师”

Day 3：此时在GrowingIO系统中，小明的用户属性职位为“产品经理”

{% hint style="warning" %}
时效性：

用户属性上传后T+1生效，即今天上传的用户属性次日凌晨更新入GrowingIO系统中。
{% endhint %}

## 创建用户属性

一、在顶部导航栏选择 “数据 &gt; 属性 &gt; 用户属性“ ，进入用户属性管理页面。

二、单击右上角**添加用户属性**，进入**新建用户属性**页面。

![](../../../../../.gitbook/assets/image%20%28503%29.png)

| 参数 | 说明 |
| :--- | :--- |
| 名称 | GrowingIO平台上属性的名称。 |
| 标识符 | 此属性在代码中的标识，仅允许大小写英文、数字、下划线，并且不能以数字开头。 |
| 类型 | 支持选择字符串、整数、日期类型用户属性。 |
| 所属分类 | 选择自定义的用户属性分类，如人口属性、交易特征 etc. |
| 描述 | 属性的描述。 |

三、填写完成后单击**确定**，完成一个用户属性的创建。

{% hint style="success" %}
在完成了配置，以及正确的代码实施后。我们即可开始在GrowingIO 使用用户属性。
{% endhint %}

## 用户属性管理页面

在用户属性管理页面可以查看用户属性的名称、标识符、类型、预置、所属分类、创建日期、创建人、最后编辑时间。

![](../../../../../.gitbook/assets/image%20%28499%29.png)

您也可以对用户属性进行以下操作：

**搜索：**您可以在页面中列表上方的搜索框按用户属性名称和标识符来搜索用户属性。

**QuickView：**单击任一用户属性，您可以在右侧弹出的用户属性详情中，查看用户属性的基本信息。

**编辑：**在QuickView界面单击用户属性的参数进行修改，修改后单击保存。

**删除：**单击单条用户属性右侧的 ![](https://docs.growingio.com/.gitbook/assets/-Lo08UtW7H58ehFKeZ4g-LsycTyZaItbL8_Wigcx-LsyfkaafJ-8X2utJ9BbE782B9E782B9E782B9.png) 选择删除，可删除不需要的用户属性。

**批量删除**：在列表中使用复选框选择多个用户属性，可以进行批量删除。

**批量移动**：在列表中使用复选框选择多个用户属性，可以进行批量移动，将用户属性移动到目标分类中。

