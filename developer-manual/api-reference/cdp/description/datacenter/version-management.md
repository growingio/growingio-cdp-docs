# 旧版本接口

## submitTagUserExportJob

描述：提交导出标签用户任务

请求类型：Mutation

接口签名：submitTagUserExportJob\(tagId: HashId!, properties: \[String!\], charset: String, detailExport: Boolean\): TagUserExportJob!

参数说明：

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#x53C2;&#x6570;&#x540D;&#x79F0;</b>
      </th>
      <th style="text-align:left"><b>&#x53C2;&#x6570;&#x7C7B;&#x578B;</b>
      </th>
      <th style="text-align:left"><b>&#x53C2;&#x6570;&#x63CF;&#x8FF0;</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">tagId</td>
      <td style="text-align:left">HashId!</td>
      <td style="text-align:left">&#x8981;&#x5BFC;&#x51FA;&#x7684;&#x7528;&#x6237;&#x6807;&#x7B7E;&#x7684;ID</td>
    </tr>
    <tr>
      <td style="text-align:left">properties</td>
      <td style="text-align:left">[String!]</td>
      <td style="text-align:left">&#x9700;&#x8981;&#x5BFC;&#x51FA;&#x7684;&#x7528;&#x6237;&#x5C5E;&#x6027;&#x6807;&#x793A;</td>
    </tr>
    <tr>
      <td style="text-align:left">charset</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x7F16;&#x7801;&#x683C;&#x5F0F;&#xFF0C;&#x5982; &#x201C;UTF-16LE&#x201D;</td>
    </tr>
    <tr>
      <td style="text-align:left">detailExport</td>
      <td style="text-align:left">Boolean</td>
      <td style="text-align:left">
        <p>&#x5F53;detailExport&#x4E3A;True&#x65F6;&#xFF0C;&#x4E3A;&#x670D;&#x52A1;&#x7AEF;&#x63A5;&#x53E3;&#x8C03;&#x7528;&#x65F6;&#x9009;&#x7528;&#xFF0C;&#x5BFC;&#x51FA;&#x683C;&#x5F0F;&#x4E3A;&#x8BE6;&#x60C5;&#xFF0C;</p>
        <p>False&#x4E3A;&#x524D;&#x7AEF;&#x63A5;&#x53E3;&#x8C03;&#x7528;&#x65F6;&#x9009;&#x7528;&#xFF0C;&#x8FD4;&#x56DE;&#x7ED3;&#x679C;&#x4E3A;&#x7B80;&#x6D01;&#x683C;&#x5F0F;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>

新版本：[submitTagUserExportJobByKey](./#submittaguserexportjobbykey)

新功能：支持根据自定义标签标识符\(tagKey\)导出用户标签

