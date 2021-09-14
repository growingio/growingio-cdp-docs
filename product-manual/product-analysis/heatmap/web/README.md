# Web端热图

## 使用准备

热图通过Chrome浏览器的插件绘制，因此需要下载安装Chrome插件，[下载安装](chrome-cha-jian.md)。

## 打开热图

插件登录后，默认查看方式是浏览模式，切换到热图模式，即可在页面绘制出热图效果。

![](../../../../.gitbook/assets/image%20%28590%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x529F;&#x80FD;&#x9879;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1-&#x67E5;&#x770B;&#x65B9;&#x5F0F;</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x6D4F;&#x89C8;&#x6A21;&#x5F0F;&#xFF1A;&#x5728;&#x6D4F;&#x89C8;&#x6A21;&#x5F0F;&#x4E0B;&#x5207;&#x6362;&#x60A8;&#x8981;&#x67E5;&#x770B;&#x7684;&#x9875;&#x9762;&#x3002;</li>
          <li>&#x70ED;&#x56FE;&#x6A21;&#x5F0F;&#xFF1A;&#x67E5;&#x770B;&#x5F53;&#x524D;&#x9875;&#x9762;&#x7684;&#x70ED;&#x56FE;&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2-&#x529F;&#x80FD;&#x533A;</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>&#x65F6;&#x95F4;&#xFF1A;&#x9009;&#x62E9;&#x70ED;&#x56FE;&#x7684;&#x5C55;&#x73B0;&#x6570;&#x636E;&#x8303;&#x56F4;&#xFF0C;&#x6700;&#x591A;&#x53EF;&#x67E5;&#x770B;&#x8FC7;&#x53BB;30&#x5929;&#x7684;&#x6570;&#x636E;&#x3002;</li>
          <li>&#x8FC7;&#x6EE4;&#x6761;&#x4EF6;&#xFF1A;&#x4E3A;&#x70ED;&#x56FE;&#x6570;&#x636E;&#x6DFB;&#x52A0;&#x8FC7;&#x6EE4;&#x6761;&#x4EF6;&#x3002;</li>
          <li>&#x70ED;&#x56FE;&#x8BE6;&#x60C5;&#xFF1A;&#x67E5;&#x770B;&#x70ED;&#x56FE;&#x8BE6;&#x7EC6;&#x6570;&#x636E;&#xFF0C;&#x5305;&#x542B;&#x6570;&#x636E;&#x6982;&#x89C8;&#x3001;&#x70B9;&#x51FB;&#x7387;&#x6392;&#x540D;&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3-&#x70ED;&#x56FE;&#x533A;&#x57DF;</td>
      <td style="text-align:left">
        <ul>
          <li>&#x9F20;&#x6807;&#x60AC;&#x505C;&#x5728;&#x70ED;&#x56FE;&#x8272;&#x5757;&#x4E0A;&#x65F6;&#xFF0C;&#x53EF;&#x67E5;&#x770B;&#x5F53;&#x524D;&#x5143;&#x7D20;&#x7684;&#x70B9;&#x51FB;&#x7387;&#x8BE6;&#x60C5;&#x3002;</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### 绘制规则 <a id="hui-zhi-gui-ze"></a>

热图模式中间的热图区域显示的是在选定的时间段和页面（而不只是热图中的当前可视区域）中，点击量在数据总量里前 1000 的有内容或有链接的元素。没有内容和链接的元素将会被过滤，以防止混淆元素的干扰。

其他绘制规则： 在当前页面的可视区域内的元素可被绘出，如果元素有一半或一半以上超出了当前可视区域，则不绘图。 元素在浏览器层面被识别为可见，即可被绘制。（比如：页面中需要鼠标点击或悬停的下拉菜单，肉眼不可见，但浏览器可见，热图可被绘出。）

### 点击率计算方式 <a id="dian-ji-shuai-ji-suan-fang-shi"></a>

在热图模式中，当您将鼠标悬停在页面元素上时，会出现红色线框标记出该元素，并且显示出该元素的点击数据：点击次数、点击人数、点击率。

 **元素点击率 = 元素点击次数/当前页面 PV**

### **点击率排名** <a id="dian-ji-shuai-pai-ming"></a>

**热图详情**数据中可查看所选页面中点击率前 15 的元素。

![](../../../../.gitbook/assets/image%20%28592%29.png)





