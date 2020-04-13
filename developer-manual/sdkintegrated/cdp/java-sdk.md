# JAVA SDK

> Java SDK支持的Java版本为java 1.6+。

## **添加依赖**

在pom.xml文件中添加依赖，我们推荐使用Maven 管理Java项目，请在 pom.xml 文件中，添加以下依赖信息，Maven 将自动获取Java SDK并更新配置。

```text
<dependency>
<groupId>io.growing.sdk.java</groupId>
<artifactId>growingio-java-sdk</artifactId>
<version>1.0.6-cdp-SNAPSHOT</version>
</dependency>
```

如果出现依赖冲突的问题（例如运行时找不到类），可以使用standalone 版本。

```text
<dependency>
<groupId>io.growing.sdk.java</groupId>
<artifactId>growingio-java-sdk</artifactId>
<version>1.0.6-cdp-SNAPSHOT</version>
<classifier>standalone</classifier>
</dependency>
```

在项目的classpath 路径下，增加 gio.properties 文件，文件内容如下：

```text
#项目采集端地址
api.host=https://api.growingio.com
#消息发送间隔时间,单位ms（默认 100）
send.msg.interval=100
#消息发送线程数量 （默认 3）
send.msg.thread=3
#消息队列大小 （默认 500）
msg.store.queue.size=500
#日志级别输出 (debug | error)
logger.level=debug
#自定义日志输出实现类
logger.implementation=io.growing.sdk.java.logger.GioLoggerImpl
#运行模式，test:仅输出消息体，不发送消息，production: 发送消息
run.mode=test
```

## **API**

### **项目信息**

| 参数名称 | 类型 | 是否必填 | 说明 |
| :--- | :--- | :--- | :--- |
| setProjectKey | string | 是 | 项目ID。 |
| setDataSourceId | string | 是 | 数据源ID。 |

### **自定义事件API**

| 参数名称 | 类型 | 是否必填 | 说明 |
| :--- | :--- | :--- | :--- |
| eventKey | string | 是 | 埋点事件的Key。 |
| loginUserId | string | 是 | 登录用户ID。 |
| eventTine | long | 否 | 事件发生时间。 |
| addEventVariable | \(string, string\|double\|Int\) | 否 | 事件级变量。 |
| addEventVariables | map&lt;string,object&gt; | 否 | 事件级变量集合。 |

代码示例：

```text
public class Demo {
private static GrowingAPI projectA = new GrowingAPI.Builder().setProjectKey("项目ID").setDataSourceId("数据源ID").build();
public static void main(String[] args) {
sendCdpCustomEvent();
}
public static void sendCdpCustomEvent() {
Map<String, Object> map = new HashMap<String, Object>();
GioCdpEventMessage msg = new GioCdpEventMessage.Builder()
.eventTime(System.currentTimeMillis())  // 默认为系统当前时间(选填)
.eventKey("test")  // 事件标识 (必填)
.loginUserId("test")  // 登录用户ID (必填)
.addEventVariable("product_name", "cdp苹果")  // 事件级变量 (选填)
.addEventVariables(map)  // 事件级变量集合 (选填)
.build();
projectA.send(msg);
}
```

### **用户变量API**

| 参数名称 | 参数类型 | 是否必填 | 说明 |
| :--- | :--- | :--- | :--- |
| loginUserId | string | 是 | 登录用户ID。 |
| time | long | 否 | 事件发生时间。 |
| addUserVariable | string, string\|double\|Int\) | 否 | 用户变量。 |
| addUserVariables | map&lt;string,object&gt; | 否 | 用户变量集合。 |

示例代码：

```text
public class Demo {
private static GrowingAPI projectA = new GrowingAPI.Builder().setProjectKey("项目ID").setDataSourceId("数据源ID").build();
public static void main(String[] args) {
sendCdpUser();
}
public static void sendCdpUser() {
Map<String, Object> map = new HashMap<String, Object>();
GioCdpEventMessage msg = new GioCdpEventMessage.Builder()
.time(System.currentTimeMillis())  // 默认为系统当前时间(选填)
.loginUserId("test")  // 登录用户ID (必填)
.addUserVariable("product_name", "cdp苹果")  // 用户变量 (选填)
.addUserVariables(map)  // 用户变量集合 (选填)
.build();
projectA.send(msg);
}
```

## **程序测试**

请按照如下步骤进行埋点数据的开发联调。

### **完成埋点事件的配置**

在GrowingIO【数据】&gt;【数据管理】中创建自定义事件及事件属性/登录用户属性，如图所示。

![](../../../.gitbook/assets/image%20%28105%29.png)

### **测试程序配置**

1. 在您的Java项目中的pom.xml中增加GrowingIO Java SDK的依赖（首次集成需要）
2. 在gio.properties配置文件将run.mode定义为test
3. 在您的Java项目中找到合适的埋点位置，调用自定义事件API/用户变量API上传数据
4. 在输出的日志中查找是否包含期望事件内容，如下：gio message is

\[{"cs1":"10324","t":"cstm","var":{"product\_name":"苹果"},"tm":1575895053509,"n":"order"}\]

![](../../../.gitbook/assets/image%20%2824%29.png)



完成以上测试步骤后： ‌

1. 修改gio.properties文件并将run.mode定义为production，并触发埋点事件 。
2. 在线查询GrowingIO数据库，确认数据上传成功。

\*\*\*\*

