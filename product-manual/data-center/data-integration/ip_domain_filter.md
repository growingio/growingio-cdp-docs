---
id: ip_domain_filter
sidebar_position: 5
---

# IP及域名数据过滤

## 用途

IP 及域名数据过滤可以去除内部人员使用对数据造成的干扰，避免 tracking code 被拷贝所造成的数据污染。

## 功能介绍

使用路径：数据中心——数据集成——IP及域名数据过滤

![图 1](/img/pic_ipdomainfilter_ip_domain_filter.png)  

### 添加IP及域名

  点击 编辑 按钮， 添加IP黑名单和需要过滤的域名
  
  ![图 2](/img/pic_ipfilter_ip_domain_filter.png)  
  
  支持输入 IP（如128.0.0.0）或 IP 网段（如128.0.0.0/22），最多 100 条，回车分隔。

  ![图 3](/img/pic_domainfilter_ip_domain_filter.png)  

  支持输入顶级域名（如 baidu.com）、二级域名（如zhidao.baidu.com）等格式，最多输入100条，回车分隔.

### 开启IP及域名过滤

  ![图 5](/img/pic_openfilter_ip_domain_filter.png)  

  开启过滤后，数据过滤将立即生效，但不对历史数据做处理，请谨慎使用过滤功能。
