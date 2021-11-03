---
id: heatmap-for-web
sidebar_position: 1
---

# Web端热图

## 简介[](#jian-jie)

热图通过Chrome浏览器的插件绘制，因此需要下载安装Chrome插件，[下载安装](/docs/product-manual/product-analysis/heatmap/web/chrome-plugin#插件下载)。


## 功能说明[](#gong-neng-shuo-ming)

插件登录后，默认查看方式是浏览模式，切换到热图模式，即可在页面绘制出热图效果。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MdwZ9MoqVht77svH0-D%2F-Mdw_0e1qImhkm5Cvaoz%2Fimage.png?alt=media&token=799d9776-1df4-43d0-930f-e1d6fc0fbc12)

| 功能项 | 说明  |
| --- | --- |
| 1-查看方式 | ​* 浏览模式：在浏览模式下切换您要查看的页面。<br></br>* 热图模式：查看当前页面的热图。 |
| 2-功能区 | ​* 时间：选择热图的展现数据范围，最多可查看过去30天的数据。<br></br>* 过滤条件：为热图数据添加过滤条件。<br></br>* 热图详情：查看热图详细数据，包含数据概览、点击率排名。 |
| 3-热图区域 | * 鼠标悬停在热图色块上时，可查看当前元素的点击率详情。 |


### 绘制规则[](#hui-zhi-gui-ze)

热图模式中间的热图区域显示的是在选定的时间段和页面（而不只是热图中的当前可视区域）中，点击量在数据总量里前 1000 的有内容或有链接的元素。没有内容和链接的元素将会被过滤，以防止混淆元素的干扰。

其他绘制规则： 在当前页面的可视区域内的元素可被绘出，如果元素有一半或一半以上超出了当前可视区域，则不绘图。 元素在浏览器层面被识别为可见，即可被绘制。（比如：页面中需要鼠标点击或悬停的下拉菜单，肉眼不可见，但浏览器可见，热图可被绘出。）


### 点击率计算方式[](#dian-ji-shuai-ji-suan-fang-shi)

在热图模式中，当您将鼠标悬停在页面元素上时，会出现红色线框标记出该元素，并且显示出该元素的点击数据：点击次数、点击人数、点击率。

**元素点击率 = 元素点击次数/当前页面 PV**

### 点击率排名[](#dian-ji-shuai-pai-ming)

**热图详情**数据中可查看所选页面中点击率前 15 的元素。

![](https://gblobscdn.gitbook.com/assets%2F-M2qbZInaXgdm8kkNosp%2F-MdwZ9MoqVht77svH0-D%2F-MdwfNrkYlRZR85-gwft%2Fimage.png?alt=media&token=bc450de0-2dd5-4dca-9c65-5fd846973e80)
