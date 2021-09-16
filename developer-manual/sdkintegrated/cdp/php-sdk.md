# PHP SDK

## 集成 PHP SDK

直接从 [GitHub](https://github.com/growingio/growingio-php-sdk/tree/op) 获取 SDK 的源码并集成到项目中。

参考如下Demo程序：

```text
<?php

include_once "GrowingIO.php";

// 请在您调试前，将accountID修改为您的项目AccountID
// 所有自定义事件需要提前在GrowingIO产品中进行定义
// 所有自定义事件的属性也需要提前在GrowingIO产品中进行定义

$accountID = "YOUR_ACCOUNT_ID"; // 项目 ID，见数据源配置
$host = "http://YOUR_COLLECTOR_DOMAIN"; // 数据收集服务域名，请参考运维手册或联系技术支持获取
$dataSourceId = "YOUR_DATASOURCE_ID"; // 数据源 ID，见数据源配置
$props = array("debug"=>false); // debug 模式，此模式仅打印日志，不发送数据

$gio = GrowingIO::getInstance($accountID, $host, $dataSourceId, $props);

function currentMillisecond() {
    list($msec, $sec) = explode(' ', microtime());
    $msectime = (float)sprintf('%.0f', (floatval($msec) + floatval($sec)) * 1000);
    return $msectime;
}

$start = currentMillisecond();
printf($start."\n");
$gio->track("testUserId","testEvent", array("eventKey2"=>"v1", "eventKey2"=>"v2"));
$gio->setUserAttributes("testUserId", array("userKey1"=>"v1", "userKey2"=>"v2"));
$stop = currentMillisecond();
printf($stop."\n");
printf(($stop-$start)."\n");
?
```

## 配置PHP SDK <a id="pei-zhi-php-sdk"></a>

目前PHP SDK支持Debug模式，可以在标准输出中输出实际的自定义事件内容，如：

```text
$props = array("debug"=>false);
```

## 程序调试 <a id="cheng-xu-tiao-shi"></a>

GrowingIO建议您按照如下步骤进行埋点数据的开发联调

1. 在GrowingIO的网站中创建自定义事件以及对应的自定义事件属性
2. 在您的PHP项目中集成GrowingIO PHP SDK的依赖（首次集成需要）
3. 参考上面的文档使用debug模式初始化GrowingIO PHP SDK
4. 在您的项目中找到合适的埋点位置，参考上面的例子填入自定义事件需要的字段
5. 执行对应修改部分的单元测试，或者编写一段测试程序运行修改部分的代码，确保触发埋点事件
6. 在输出的日志中查找是否包含期望事件内容
7. 去掉debug参数，再运行一次程序，确保能在后台数据中查到上传的事件，后台数据查看方式可联系技术支持
8. 在事件分析模块中，延迟1小时可以看到当天的统计结果

