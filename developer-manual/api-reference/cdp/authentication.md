# 接口认证

系统部署后，会给每个系统生成一个 API 密钥，此密钥默认不支持修改和替换，请妥善保存，请勿泄露。如需更换请联系部署工程师。

使用内部接口前需要使用 API 密钥生成临时认证 Token，命令行示例如下：

```text
curl --location --request POST 'http://www.gio.com/accounts/oauth/access_token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=api' \
--data-urlencode 'client_secret=API密钥' \
--data-urlencode 'scope=system'
```

使用返回内容里的 access\_token 作为后续接口认证的 Token，请求时在 header 中增加 “Authorization: Token 临时token”。Token失效后（接口返回 401\)，请再次调用生成接口。

