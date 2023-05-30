--
id: export-from-dw
sidebar_position: 3
---

# 离线数据导出

## 简介

GrowingIO 为开放架构，采集上报的用户数据支持离线导出到客户的自建数仓或数据湖系统，以满足在客户在自身系统中做数据集成应用。

离线数据导出需要较充裕的磁盘空间，它是默认关闭的。若需开启，请联系GrowingIO的技术支持。

## 能力边界和约束

- 用户数据由系统定时生成为文件供下载使用，不支持直连数仓导出数据。
- 系统生成文件的启动时间为每日凌晨，生成完毕的时间跟数据量有关，建议观察稳定后再做下游的使用配置。
- 每天定时生成的文件，按种类分为5组压缩文件：事件明细、用户ID、用户属性、用户标签和用户分群，每组文件在其文件夹中存储。
- 用户ID/属性/标签解压后的文件均是以gio_id（GrowingIO生成的用户编号）为首列（主键）的两列数据，第二列是用户字段的值。比如用户属性为生日的文件，第二列即是用户的生日值。这样设计的优点是文件内容的结构稳定，更接近数据的本质，使用灵活；缺点是在用户宽表的使用场景中，需要将所需字段的文件按主键关联整合成宽表存储，有一定的ETL工作量。
- 事件明细的数据是T+1的增量数据，即今天凌晨生成的文件内容是昨日0点起至23点末的事件；用户ID/属性/标签/分群则为全量用户数据。

## 导出文件的下载与使用

### 导出文件所在的FTP路径

系统每日启动导出任务，将在FTP固定路径下生成前一日的日期名称的文件夹。
> 例子：比如今天是2021-12-02，系统创建的文件夹为：/ftp/admin/gio_data/v1/2021-12-01。

连接FTP的凭证信息请联系GrowingIO技术支持。

### 数据详情

每个日期文件夹下，均有5个文件组，对应不同的数据种类，如事件明细、用户属性等。

| 文件组   | 文件夹         | 文件列表                                                                                                                                   | 文件数据字典         |
|----------|----------------|--------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| 事件明细 | event          | part-XXXX.csv.gz                                                                                                                           | 见附录               |
| 用户ID   | user_id        | user\_id/id\_$anonymous_user/part-XXXX.csv.gz<br/>user\_id/id\_$basic_userId/part-XXXX.csv.gz<br/>user\_id/{其他自定义ID}/part-XXXX.csv.gz | gio\_id {用户ID值}   |
| 用户属性 | user\_props    | user\_props/usr\_{用户属性标识符}/part-XXXX.csv.gz                                                                                         | gio\_id {用户属性值} |
| 用户标签 | user\_tags     | user\_props/tag\_{用户标签标识符}/part-XXXX.csv.gz                                                                                         | gio\_id {用户标签值} |
| 用户分群 | user\_segments | user\_props/seg\_{用户分群标识符}/part-XXXX.csv.gz                                                                                         | gio\_id              |

在服务器上，可以使用一些简单的linux命令查看导出文件的详情，以便更好地理解数据格式。

如下提供事件明细和用户属性的示例供参考：

#### 示例1：事件明细数据

将FTP文件下载到本地：

```bash
hdfs dfs -get /ftp/admin/gio_data/v1/2021-12-15/event/part* ./
```

压缩文件解压命令：

```bash
gunzip -d part*.csv.gz
```

解压后的文件：part-00000-0c57c7a1-4d4c-4b49-ba40-045b802dd6cb-c000.csv

查看文件内容命令：

```bash
head -1 part-00000-0c57c7a1-4d4c-4b49-ba40-045b802dd6cb-c000.csv
```

![picture 1](/img/9a36043772d0349768c10f3dde4f715d4325f10146d26cb9fe40ea6365bc1ede_pic_1639970518912_2021-12-20.png)

数据字段的分隔符是\t，空字符串为英文双引号包裹。各字段的含义见附录。

#### 示例2：用户属性数据

将FTP中用户生日（属性标识符为birthday）的文件下载到本地：

```bash
hdfs dfs -get /ftp/admin/gio_data/v1/2021-12-15/user_props/usr_birthday/part* ./
```

压缩文件解压命令：

```bash
gunzip -d part*.csv.gz
```

解压后的文件：part-00000-39d0854c-6e9b-42cc-a06a-a419975911f7-c000.csv

查看文件内容命令：

```bash
head part-00000-39d0854c-6e9b-42cc-a06a-a419975911f7-c000.csv 
```

![picture 1](/img/ab0a84dc99045edaacf9d609f1051c695ba5757fa38e62386f2272be7dae55a9_pic_1639970681349_2021-12-20.png)

数据字段的分隔符是\t，空字符串为英文双引号包裹

## 常见问题

Q：事件明细是否有历史数据一次性导出的方案？
A：由于事件明细的每日例行定时导出任务是导出T+1的数据，因此在开启离线数据导出能力后，可以每日下载前一日的事件数据。若需要将历史数据一次性导出，请联系GrowingIO项目经理获得支持。

Q：下载压缩文件前，如何知道文件是完整的？
A：每个压缩文件生成完毕后，都会在同级路径下生成名称为 _SUCCESS 的完整性校验文件，获取到该文件后再下载数据文件。

## 附录：事件明细文件的字段详情

| 序号 | 字段                | 含义                                               | 备注                                                                     |
|------|---------------------|----------------------------------------------------|--------------------------------------------------------------------------|
| 1    | event_key           | 事件标识                                           | visit事件$visit、访问事件$page、自定义事件如paySuccess                   |
| 2    | event_time          | 事件接收时间                                       | 示例：2021-06-01 23:59:20.912                                            |
| 3    | event_id            | 事件ID                                             | 事件内容hash后的长度为32位的字符串，也支持导入数据中自定义event_id值     |
| 4    | event_type          | 事件类型                                           | visit, page, custom_event类型                                            |
| 5    | client_time         | 事件采集时间                                       | 示例：2021-06-01 23:59:20.912                                            |
| 6    | anonymous_user      | 访问用户ID                                         |                                                                          |
| 7    | user                | 登录用户ID                                         |                                                                          |
| 8    | user_key            | 用户身份                                           | 访问状态：$anonymous_user；登录状态：$basic_userId；自定义身份：自定义值 |
| 9    | gio_id              | 用户编号                                           | GrowingIO id-service服务给用户生成的唯一编号                             |
| 10   | session             | 会话标识                                           |                                                                          |
| 11   | attributes          | 事件属性                                           | 事件属性的KV值                                                           |
| 12   | $package            | 包名                                               |                                                                          |
| 13   | $platform           | 平台标识                                           | Web                                                                      |
| 14   | $referrer_domain    | 来源域名或包名                                     |                                                                          |
| 15   | $utm_source         | 广告来源，标识投放的网站                           |                                                                          |
| 16   | $utm_medium         | 广告媒介或营销媒介                                 |                                                                          |
| 17   | $utm_campaign       | 广告名称，产品的具体广告系列名称、标语、促销代码等 |                                                                          |
| 18   | $utm_term           | 广告关键字，标识付费搜索关键字                     |                                                                          |
| 19   | $utm_content        | 广告内容，用于区分相似内容或同一广告内的链接。     |                                                                          |
| 20   | $ads_id             | 广告ID                                             |                                                                          |
| 21   | $key_word           | 访问来源广告关键字（通用维度）                     |                                                                          |
| 22   | $country_code       | 国家码                                             | 示例：CN                                                                 |
| 23   | $country_name       | 国家名称                                           | 示例：中国                                                               |
| 24   | $region             | 省份                                               | 示例：江苏                                                               |
| 25   | $city               | 城市                                               | 示例：南京                                                               |
| 26   | $browser            | 浏览器名称                                         |                                                                          |
| 27   | $browser_version    | 浏览器版本                                         |                                                                          |
| 28   | $os                 | 操作系统名称                                       |                                                                          |
| 29   | $os_version         | 操作系统版本                                       |                                                                          |
| 30   | $client_version     | 客户端版本，移动端存在                             |                                                                          |
| 31   | $channel            | 客户端渠道来源                                     |                                                                          |
| 32   | $device_brand       | 设备品牌名称                                       |                                                                          |
| 33   | $device_model       | 设备型号                                           |                                                                          |
| 34   | $device_type        | 设备类型                                           | 0：平板 1：手机                                                          |
| 35   | $device_orientation | 设备方向                                           |                                                                          |
| 36   | $resolution         | 屏幕尺寸                                           |                                                                          |
| 37   | $language           | 语言                                               | 示例：zh-cn                                                              |
| 38   | $referrer_type      | 来源类型                                           |                                                                          |
| 39   | account_id          | GrowingIO的AI值                                    |                                                                          |
| 40   | $domain             | 域名或包名                                         |                                                                          |
| 41   | $ip                 | 客户端IP地址                                       |                                                                          |
| 42   | $user_agent         | 浏览器 agent 详细信息                              |                                                                          |
| 43   | $sdk_version        | SDK版本号                                          |                                                                          |
| 44   | $data_source_id     | 数据源ID                                           |                                                                          |
