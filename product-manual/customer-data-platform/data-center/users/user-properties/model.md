# 用户属性归因模型

## 简介

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

