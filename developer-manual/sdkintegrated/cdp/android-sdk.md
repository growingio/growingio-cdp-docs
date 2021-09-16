# Android SDK

## **添加依赖**

在 module 级别的 build.gradle 文件中添加依赖

```text
dependencies {
    //埋点CDP SDK
    implementation 'com.growingio.android:vds-android-agent:cdp-1.2.4'
}
```

## **添加初始化代码**

请将GrowingIO.starWithConfiguration 加在您的 Application 的onCreate方法中。

SDK的初始化时机必须在 Application的onCreate方法中进行。

```text
public class MyApplication extends Application {
@Override
public void onCreate() {
    super.onCreate();
    // GrowingIO 初始化代码
    GrowingIO.startWithConfiguration(this, new Configuration()
        .setProjectId("获取您的项目ID")
        .setDataSourceId("填写您的数据源ID")
        .setURLScheme("填写UrlScheme")
        .setTestMode(BuildConfig.DEBUG)
        .setDebugMode(BuildConfig.DEBUG)
        .setTrackerHost("这里设置为您的 HOST ")
        .setChannel("XXX应用商店")
        );
    }
}
```

## **添加应用权限和**URL Scheme

将应用的 URLScheme 和应用权限添加到你的 AndroidManifest.xml 中。

```text
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
package="com.example.cdpdemo">
<!-- GIO 需要的权限  -->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW"/>
<application
        android:name=".MyApplication"
        <activity android:name=".MainActivity">
            <!--请添加这里的整个 intent-filter 区块，并确保其中只有一个 data 字段-->
            <intent-filter>
                <data android:scheme="growing.您的URL Scheme" />
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
            </intent-filter>
            <!--请添加这里的整个 intent-filter 区块，并确保其中只有一个 data 字段-->
        </activity>
    </application>
</manifest>
```

## **添加混淆文件**

如果您启用了混淆，请在您的 proguard-rules.pro 中加入如下代码。

```text
-keep class com.growingio.** {
*;
}
-dontwarn com.growingio.**
-keepnames class * extends android.view.View
-keepnames class * extends android.app.Fragment
-keepnames class * extends android.support.v4.app.Fragment
-keepnames class * extends androidx.fragment.app.Fragment
-keep class android.support.v4.view.ViewPager{
*;
}
-keep class android.support.v4.view.ViewPager$**{
*;
}
-keep class androidx.viewpager.widget.ViewPager{
*;
}
-keep class androidx.viewpager.widget.ViewPager$**{
*;
}
```

如果您使用的AndRestGuard ，请在白名单中添加GrowingIO。

```text
R.string.growingio*
```

## **API**

### **初始化配置API**

初始化配置API在Application中初始化SDK处使用。

<table>
  <thead>
    <tr>
      <th style="text-align:left">API</th>
      <th style="text-align:left">&#x9ED8;&#x8BA4;&#x503C;</th>
      <th style="text-align:left">&#x662F;&#x5426;&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">setProjectId</td>
      <td style="text-align:left">&#x65E0;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x9879;&#x76EE;ID&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">setFlushInterval</td>
      <td style="text-align:left">15s</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x8BBE;&#x7F6E;&#x83B7;&#x53D6;&#x53D1;&#x9001;&#x6570;&#x636E;&#x7684;&#x4E8B;&#x4EF6;&#x95F4;&#x9694;&#xFF0C;&#x9ED8;&#x8BA4;15s</td>
    </tr>
    <tr>
      <td style="text-align:left">setCellularDataLimit</td>
      <td style="text-align:left">10MB</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x8BBE;&#x7F6E;&#x6BCF;&#x5929;&#x4F7F;&#x7528;&#x6570;&#x636E;&#x7F51;&#x7EDC;&#xFF08;2G&#x3001;3G&#x3001;4G&#xFF09;&#x4E0A;&#x4F20;&#x7684;&#x6570;&#x636E;&#x91CF;&#x7684;&#x4E0A;&#x9650;&#xFF0C;&#x9ED8;&#x8BA4;&#x503C;10485KB&#xFF08;10MB&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left">getCellularDataLimit</td>
      <td style="text-align:left">&#x65E0;</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x8BBE;&#x7F6E;&#x6BCF;&#x5929;&#x4F7F;&#x7528;&#x6570;&#x636E;&#x7F51;&#x7EDC;&#xFF08;2G&#x3001;3G&#x3001;4G&#xFF09;&#x4E0A;&#x4F20;&#x7684;&#x6570;&#x636E;&#x91CF;&#x7684;&#x4E0A;&#x9650;&#xFF0C;&#x9ED8;&#x8BA4;&#x503C;10485KB&#xFF08;10MB&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left">setDataSourceId</td>
      <td style="text-align:left">&#x65E0;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x6570;&#x636E;&#x6E90;ID&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">srtURLScheme</td>
      <td style="text-align:left">&#x65E0;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x8BBE;&#x7F6E;URLScheme&#xFF0C;&#x662F;&#x5E94;&#x7528;&#x552F;&#x4E00;&#x6807;&#x8BC6;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">setDebugMode</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x5728;local&#x4E2D;&#x8F93;&#x51FA;&#x91C7;&#x96C6;&#x65E5;&#x5FD7;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">setTestMode</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">
        <p>&#x5B9E;&#x65F6;&#x53D1;&#x9001;&#x6570;&#x636E;&#xFF0C;&#x5F00;&#x542F;&#x5219;&#x4E0D;&#x9075;&#x5FAA;&#x79FB;&#x52A8;&#x7F51;&#x7EDC;</p>
        <p>&#x72B6;&#x6001;&#x4E0B;&#x6570;&#x636E;&#x53D1;&#x9001;&#x5927;&#x5C0F;&#x9ED8;&#x8BA4;
          3M &#x9650;&#x5236;&#x4EE5;&#x53CA;</p>
        <p>&#x91C7;&#x96C6;&#x6570;&#x636E;&#x7F13;&#x5B58;30&#x79D2;&#x53D1;&#x9001;&#x7B56;&#x7565;&#x3002;</p>
        <p>&#x4E3A;&#x4E86;&#x65B9;&#x4FBF;&#x5F00;&#x53D1;&#x8005;&#x67E5;&#x770B;&#x65E5;&#x5FD7;&#xFF0C;&#x4E00;&#x822C;&#x548C;</p>
        <p>setDebugMode&#x4E00;&#x8D77;&#x4F7F;&#x7528;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">setChannel</td>
      <td style="text-align:left">&#x65E0;</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x8BBE;&#x7F6E;App&#x4E0B;&#x8F7D;&#x6E20;&#x9053;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">setImeiEnable</td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">
        <p>&#x4E3A;&#x4E86;&#x6D77;&#x5916;&#x5E94;&#x7528;&#x5E02;&#x573A;&#x4E0A;&#x67B6;&#x5E94;&#x7528;&#xFF0C;&#x8BBE;&#x7F6E;&#x4E3A;</p>
        <p>fasle&#x5219;SDK&#x4E0D;&#x91C7;&#x96C6;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">setAndroidIdEnable</td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">
        <p>&#x4E3A;&#x4E86;&#x6D77;&#x5916;&#x5E94;&#x7528;&#x5E02;&#x573A;&#x4E0A;&#x67B6;&#x5E94;&#x7528;&#xFF0C;&#x8BBE;&#x7F6E;&#x4E3A;</p>
        <p>false&#x5219;SDK&#x4E0D;&#x91C7;&#x96C6;Android ID&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">disableDataCollect</td>
      <td style="text-align:left">&#x65E0;</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x8BBE;&#x7F6E;GDPR&#x751F;&#x6548;</td>
    </tr>
  </tbody>
</table>

### **运行时API**

> **注意：**GrowingIO 所有API 都需要在主线程调用。

|  |  |
| :--- | :--- |
| setGeoLocation | 设置经纬度，并在vst事件中发送，Android SDK暂时没办法自动获取GPS数据，如果您要采集GPS数据，需要在您的App每次获取完GPS数据之后，通过该API告知SDK。如果您不设置，我们默认使用用户IP的location。 |
| clearGeoLocation | 清空经纬度。 |
| setChannel | 保留原有设置渠道信息的方法，新增在运行时设置渠道信息。新增的接口无法保证所有数据都一定会带上渠道信息（虽然我们会通过重发机制进行保证，但是无法做到100%）。 |
| disableDataCollect | 遵守欧洲联盟出台的通用数据保护条例，用户不授权，不采集用户数据。 |
| enableDataCollect | 遵守欧洲联盟出台的通用数据保护条例，用户授权，采集用户数据。 |

示例代码：

```text
// 得到 GrowingIO 实例后可以调用其中 API
IGrowingIO gio = GrowingIO.getInstance();
gio.setUserId("xiaowang");
```

## **常用API**

### **设置登录用户ID**

当用户登录应用后调用setUserId，上传登录用户ID。

| 参数名称 | 类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| userId | string | 是 | 应用的登录用户ID。 |

代码示例：

```text
//setuserId API调用示例
GrowingIO.getInstance().setUserId("xiaowang")
```

> Tips：
>
> 如果您的App每次用户升级版本时无需重新登录的话，为防止用户本地缓存被清除导致的无法被识别为登录用户，建议在用户每次升级App版本后初次访问时重新调用上述setUserId方法。

### **清除登录用户ID**

当用户退出登录后，调用clearUserId，清除已经设置的登录用户ID。

```text
//clearUserId API原型和调用示例
GrowingIO.getInstance().clearUserId();
```

### **设置自定义事件和属性**

发送一个自定义事件，在添加所需发送的事件代码之前，需要在打点管理用户界面配置事件及事件属性。

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x662F;&#x5426;&#x5FC5;&#x987B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">eventId</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x6807;&#x8BC6;&#x7B26;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">eventLevelVariable</td>
      <td style="text-align:left">JSON Object</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">
        <p>&#x4E8B;&#x4EF6;&#x53D1;&#x751F;&#x65F6;&#x6240;&#x4F34;&#x968F;&#x7684;&#x7EF4;&#x5EA6;&#x4FE1;&#x606F;&#x3002;</p>
        <p>&#x9650;&#x5236;&#xFF1A;&#x975E;&#x7A7A;&#xFF0C;&#x952E;&#x503C;&#x5BF9;&#x4E2A;&#x6570;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;100&#xFF08;eventLevelVariable.length()&lt;=100&#xFF09;&#xFF1B;</p>
        <p>eventLevelVariable&#x5185;&#x90E8;&#x4E0D;&#x5141;&#x8BB8;&#x542B;&#x6709;</p>
        <p>JSONObject&#x6216;&#x8005;JSONArray&#xFF1B;</p>
        <p>key&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;50&#xFF0C;value&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;</p>
        <p>&#x4E8E;&#x7B49;&#x4E8E;200&#xFF0C;&#x503C;&#x4E0D;&#x80FD;&#x4E3A;&#x7A7A;&#x5B57;&#x7B26;&#x4E32;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x201C;&#x201D;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">itemId</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x7269;&#x54C1;&#x6A21;&#x578B;&#x552F;&#x4E00;&#x6807;&#x8BC6;&#x5C5E;&#x6027;&#xFF0C;&#x5982;&quot;order_id&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">itemKey</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x7269;&#x54C1;&#x6A21;&#x578B;&#x552F;&#x4E00;&#x6807;&#x8BC6;&#x5C5E;&#x6027;&#x7684;&#x503C;&#xFF0C;&#x5982;&quot;123456&quot;</td>
    </tr>
  </tbody>
</table>

示例代码：

```text
// track API调用示例一
IGrowingIO gio = GrowingIO.getInstance();
gio.track("registerSuccess");

// track API调用示例二 - 事件属性
IGrowingIO gio = GrowingIO.getInstance();
JSONObject jsonObject = new JSONObject();
jsonObject.put("gender", "male");
jsonObject.put("age", "21");
gio.track("registerSuccess", jsonObject);

// track API调用示例三 - 物品模型
IGrowingIO gio = GrowingIO.getInstance();
JSONObject jsonObject = new JSONObject();
String eventName = "payOrder";
eventVar.put("k1","v1");
eventVar.put("k2","v2");
String itemKey = "order_id";
String itemId = '123456';
gio.track(eventName, eventVar, itemId, itemKey);
```

### **设置用户属性**

自定义用户属性，用于用户属性相关的分析，比如年龄、性别、会员等级等。

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x662F;&#x5426;&#x5FC5;&#x4F20;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">key</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x7528;&#x6237;&#x53D8;&#x91CF;&#x7684;&#x6807;&#x8BC6;&#x7B26;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x7528;&#x6237;&#x53D8;&#x91CF;&#x7684;&#x503C;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">peopleVariables</td>
      <td style="text-align:left">JSON Object</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">
        <p>&#x9650;&#x5236;&#xFF1A;&#x975E;&#x7A7A;&#xFF0C;&#x952E;&#x503C;&#x5BF9;&#x4E2A;&#x6570;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;</p>
        <p>100&#xFF08;jsonObject.length()&lt;=100&#xFF09;&#xFF1B;</p>
        <p>&#x5185;&#x90E8;&#x4E0D;&#x5141;&#x8BB8;&#x5D4C;&#x5957;&#x542B;&#x6709;JSONObject&#x6216;&#x8005;</p>
        <p>JSONArray&#xFF1B;</p>
        <p>key&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;50&#xFF0C;value&#x957F;&#x5EA6;&#x9650;&#x5236;</p>
        <p>&#x5C0F;&#x7B49;&#x4E8E;200&#xFF0C;&#x503C;&#x4E0D;&#x80FD;&#x4E3A;&#x7A7A;&#x4E32;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&quot;&quot;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>

代码示例：

```text
//代码示例一
try {
    GrowingIO.getInstance().setUserAttributes(new JSONObject().put("age", 54).put("gender", "male"));
} catch (JSONException e) {
    e.printStackTrace();
}
//代码示例二
HashMap<String,Object> userAttr = new HashMap<>();
userAttr.put("age",54);
userAttr.put("gender","female");
GrowingIO.getInstance().setUserAttributes(userAttr);
```

### **发送自定义Page 事件 （数据采集SDK &gt;=1.2.0）** <a id="page"></a>

| 参数名称 | 类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| pageName | string | 是 | **page**事件标识符。 |

```objectivec
  /**
 发送自定义Page事件

 @param pageName : 页面名称, pageName为正常中英文数字组合的字符串, 长度<=1000, 请不要含有 "'|\*&$@/', 等特殊字符
 */
IGrowingIO trackPage(String pageName);

//代码示例
GrowingIO.getInstance().trackPage("TrackTestPage");
```

### 加载了H5内嵌页SDK gio\_hybrid\_cdp.js的页面。自动采集H5**（数据采集SDK &gt;=1.2.0）** <a id="bridgeforwebview"></a>

| 参数名称 | 类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| webView | WebView | 是 | WebView实例化后立刻调用 |

```objectivec
//代码示例
private void initWebView() {
        mWebView = findViewById(R.id.web_view);
        GrowingIO.getInstance().bridgeForWebView(mWebView);
        mWebView.loadUrl("https://www.growingio.com");
    }
```

{% hint style="info" %}
需要在 webview 初始化后调用
{% endhint %}

