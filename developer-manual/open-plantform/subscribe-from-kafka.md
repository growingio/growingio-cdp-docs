---
id: subscribe-from-kafka
sidebar_position: 1
---

# Kafka 实时数据订阅

## 简介

GrowingIO 为开放架构，实时采集的用户行为数据支持订阅以满足更多的使用场景，如基于用户事件触发的商品推荐、消息推送等。

## 能力边界和约束

- 通过jar依赖的形式，获取Kafka里的原始数据，不包含后续数据流中GrowingIO添加的字段
- 订阅的机器需要与GrowingIO私有化部署的机器在同一个内网，且可以解析GrowingIO服务器的host

## 能力说明

### Topic 范围

1. 用户行为数据

    Topic: cdp-event-collect 行为事件,包含 访问，埋点，页面，点击事件

2. 用户属性数据

    Topic: cdp-user-props-collect 用户属性

3. 维度表数据

    Topic: cdp-item-collect 维度表

### 安装依赖

GrowingIO提供了集成 kafka 里面的protobuf二进制数据转换成数据模型字段的数据工具类，所在的jar包已提交到Maven中央仓库中，需要通过 Maven 给项目引入依赖的jar包。
项目引入依赖的jar包需要在pom.xml中添加如下配置信息：

``` xml
<dependency>
    <groupId>io.growing.data.utils.connector</groupId>
    <artifactId>gio-data-connector</artifactId>
    <version>1.0.1</version>
</dependency>
```

pom中引入依赖后，刷新Maven拉取jar包到本地

::: warn
刷新Maven获取jar包时，若报错：
Failed to read artifact descriptor for io.growing.data.utils.connector:gio-data-connector:jar:standalone:1.0.1

解决方案：在Maven缺省的本地仓库路径.m2下修改settings.xml文件，增加中央仓库地址的配置，内容参加如下：
:::

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
  <offline>false</offline>
  <servers>
  </servers>
  <mirrors>
    <mirror>
      <id>huaweicloud</id>
      <mirrorOf>central</mirrorOf>
      <url>https://repo.huaweicloud.com/repository/maven/</url>
    </mirror>
  </mirrors>
  <profiles>
    <profile>
      <id>defaultProfile</id>
      <repositories>
         <repository>
          <id>gio</id>
          <name>local private nexus</name>
          <url>https://nexus.growingio.cn/repository/maven-public</url>
          <releases>
            <enabled>true</enabled>
            <checksumPolicy>warn</checksumPolicy>
          </releases>
          <snapshots>
            <enabled>true</enabled>
          </snapshots>
              </repository>
        <repository>
          <id>huawei</id>
          <name>huawei</name>
          <url>https://repo.huaweicloud.com/repository/maven/</url>
        </repository>
                          <repository>
          <id>flink snapshot</id>
          <name>flink snapshot</name>
          <url>https://repository.apache.org/content/repositories/snapshots</url>
        </repository>
        <repository>
          <id>oss.sonatype.org-snapshot</id>
          <url>https://oss.sonatype.org/content/repositories/snapshots</url>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>true</enabled>
          </snapshots>
        </repository>
      </repositories>
      <pluginRepositories>
        <pluginRepository>
          <id>alimaven</id>
          <name>aliyun maven plugin repo</name>
          <url>https://maven.aliyun.com/nexus/content/groups/public/</url>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
          </snapshots>
        </pluginRepository>
      </pluginRepositories>
    </profile>
  </profiles>
  <activeProfiles>
    <activeProfile>defaultProfile</activeProfile>
  </activeProfiles>
</settings>
```

### 参数配置

Jar 内部提供通过 KafkaSource 自动消费kafka 中的数据，需先配置 gio-kafka.properties 放到 classpath 中。

``` conf
# kafka server 地址和端口。多个地址用英文逗号分隔
bootstrap.servers={kafka地址1}:9092,{kafka地址2}:9092,{kafka地址3}:9092 ...
# 消费者组
group.id=sdk-demo
```

### 数据格式及转换工具

#### 转换工具类

通过3个数据转换工具类，将 kafka 中的 protobuf 二进制数据转换成数据模型字段。

  1. 获取行为事件数据

``` java
EventViewDto eventView = new EventDtoTransformer().transform(protobufBytes)
```

  2. 获取用户属性数据

``` java
UserViewDto eventView = new UserDtoTransformer().transform(protobufBytes)
```

  3. 获取维度表数据

``` java
ItemViewDto itemView = new ItemDtoTransformer().transform(protobufBytes)
```

#### 消费 kafka 数据示例

使用 KafkaSource 消费行为数据的示例，更多例子参考 io.growing.data.utils.connector.examples.ConsumeKafkaSource

``` java
import io.growing.data.utils.connector.dto.EventViewDto;
import io.growing.data.utils.connector.dto.ItemViewDto;
import io.growing.data.utils.connector.dto.UserViewDto;
import io.growing.data.utils.connector.source.DataSource;
import io.growing.data.utils.connector.source.KafkaSource;
import io.growing.data.utils.connector.transformer.Transformer;
import io.growing.data.utils.connector.transformer.EventDtoTransformer;
import io.growing.data.utils.connector.transformer.ItemDtoTransformer;
import io.growing.data.utils.connector.transformer.UserDtoTransformer;

public class Demo {

    static DataSource source = new KafkaSource();

    public static void main( String[] args ) {
       consumeEventView();
    }

    public static void consumeEventView() {
        Transformer<EventViewDto> event = new EventDtoTransformer(); //数据转换类
        source.open(event.messageTypes()); //数据类型
        source.consume(event, new OutputEventView());
    }
}


public class OutputEventView implements OutputMessage<EventViewDto>{
    @Override
    public EventViewDto output(EventViewDto input) {
        System.out.println("event_key: " + input.getEventKey());
        
        return null;
    }
}
```

## 数据字典

用户行为数据字典

| Kafka字段 | 事件表字段（2.0版） | 含义 |
| --- | --- | --- |
| String eventKey; | event_key | 事件标识符 |
| long eventTime; | event_time | 事件接收时间（毫秒时间戳） |
| long clientTime; | client_time | 事件发生时间（毫秒时间戳） |
| String anonymousUser; | anonymous_user | 访问用户ID |
| String userId; | user | 登录用户ID |
| String userKey; | user_key | 用户身份类型 |
| String session; | session | 会话标识，标记一个访问 |
| Map<String, String> attributes; | attributes | 事件属性 |
| String packageName; | package | APP包名/Web域名/小程序APPID |
| String platform; | $platform | 平台标识，示例：Web |
| String referrerDomain; | $referrer_domain | 来源域名或包名 |
| String path; | $path | 页面路径 |
| String query; | $query | 页面query参数 |
| String keyWord; | $key_word | 访问来源广告关键字 |
| String accountId; | account_id | 系统账户ID，由SDK集成时设置 |
| String domain; | $domain | 域名或包名 |
| String ip; | $ip | 客户端ID地址 |
| String userAgent; | $user_agent | 浏览器 agent 详细信息 |
| String sdkVersion; | $sdk_version | SDK版本号 |
| String dataSourceId; | $data_source_id | 数据源信息 |

用户属性数据字典

| Kafka字段 | 含义 |
| --- | --- |
| String accountId; | 系统账户ID，由SDK集成时设置 |
| String propKey; | 属性标识符 |
| String propValue; | 属性值 |
| long sendTime; | 属性接收时间 |
| String userKey; | 用户身份 |
| String userId; | 登录用户ID |
| String anonymousId; | 匿名用户ID |

维度表数据字典

| Kafka字段 | 含义 |
| --- | --- |
| String accountId; | 系统账户ID，由SDK集成时设置 |
| String propKey; | 维度表字段标识符 |
| String propValue; | 维度表字段值 |
| String itemKey; | 维度表标识符 |
| String itemValue; | 维度表记录ID |

## 常见问题

- Q：支持订阅历史数据吗？

  A：可以。gio-kafka.properties 配置文件中加入 auto.offset.reset=earliest，可以订阅 Kafka 中保存的历史数据。

- Q：能指定数据源 ID 订阅 Kafka 数据吗？

  A：不能指定数据源 ID 订阅，但可以在消费代码中按照数据源 ID 过滤，提取需要的数据。

- Q：能按组订阅 Kafka 数据吗？

  A：可以。gio-kafka.properties 配置文件中定义 group.id，区分不同的消费组。

- Q：Kafka 订阅不到数据可能的原因

  A：多半跟网络不通有关系，请确认通过 telnet hostname 9092 能访问 GrowingIO 部署的服务器。