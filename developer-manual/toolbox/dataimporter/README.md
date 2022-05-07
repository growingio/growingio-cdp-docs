---
id: data-importer
sidebar_position: 1
---

# 数据导入工具

## 简介[](#jian-jie)

如下场景，您选用该工具导入历史数据会比较合适

**场景 1：**

当您的公司购买了 GrowingIO 的产品，在实施初期，有大量的历史数据需要一次性导入进来，与实时采集数据做分析。由于前端界面创建的单个导入任务，对导入文件大小和数据量有限制，您按照分天、分周或分月（服务器标准配置下，建议的导入数据时间跨度的最大值）将历史数据拆分成多个文件，手动创建任务导入，费时费力。

**场景 2**：

您公司购买 GrowingIO 产品一段时间后，公司有每日增量的数据需要定时批量导入，比如内部系统计算的用户属性值，需要导入到 GrowingIO 中。这种情况下，导入的数据量虽然不大，预计在千万行以内，但需要每日定时导入，如果人工操作肯定不合适。

在如上两个场景下，将需要分批或定时导入的操作，交给工具去执行，是更高效的。

## 功能边界或约束[](#gong-neng-bian-jie-huo-yue-shu)

- 多事件的历史数据导入，推荐使用[Json 数据导入](../../../developer-manual/toolbox/dataimporter/data-importer-json)​
- 导入性能更强的方式，推荐使用[Json 数据导入](../../../developer-manual/toolbox/dataimporter/data-importer-json)​
- 支持导入用户行为和用户属性数据，不支持导入维度表数据

文本、Mysql 和 Hive 等类型数据，辅助工具需要做本地转换，对导入性能会有损耗。建议您提前转成 Json 格式，使用 Json 数据导入的方式高效完成导入任务。

​

## 功能说明[](#gong-neng-shuo-ming)

### 下载辅助工具[](#xia-zai-fu-zhu-gong-ju)

​[辅助工具的安装和配置](../../../developer-manual/toolbox#辅助工具的安装和配置)​

### 选择合适的导入方式[](#xuan-ze-he-shi-de-dao-ru-fang-shi)

历史数据导入工具支持导入用户行为数据和用户属性数据，[固定数据格式](../../../product-manual/customer-data-platform/data-integration/data-import#数据导入格式)，可选择的工具类型如下

- ​[Json 数据导入](../../../developer-manual/toolbox/dataimporter/data-importer-json)​
- ​[文本数据导入](../../../developer-manual/toolbox/dataimporter/data-importer-txt)​
- ​[Mysql 数据导入](../../../developer-manual/toolbox/dataimporter/data-importer-mysql)​
- ​[Hive 数据导入](../../../developer-manual/toolbox/dataimporter/data-importer-hive)​

### 指定数据源[](#zhi-ding-shu-ju-yuan)

导入数据前，需要先指定所属的数据源 ID。数据源的创建位置见：[数据源管理](../../../product-manual/customer-data-platform/data-integration/datasource-manage)​

- 创建"用户属性数据"的数据源，操作方式：新建数据源 > 历史数据导入 > 用户属性数据
- 创建"用户行为数据"的数据源，操作方式：新建数据源 > 历史数据导入 > 用户行为数据

创建后，在数据源管理列表页面查看相应的数据源 ID：![](/img/assets-M2qbZInaXgdm8kkNosp-MQMBHo2WMWoLWAEcUix-MQMD0b5FH58iKBUe3Noimage.png)​

### 任务查看[](#ren-wu-cha-kan)

历史数据导入工具的命令执行成功后，系统为其生成一个调度任务。任务执行的进度见：[数据导入管理](../../../product-manual/customer-data-platform/data-integration/data-import)​

![](/img/assets-M2qbZInaXgdm8kkNosp-MkW6V7nyui6VOb3sD6--MkW7w-vSJlkhumeTU5Vimage.png)
