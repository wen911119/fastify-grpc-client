> #### 在fastapi内使用
fastapi框架已经内置该插件，所以只要写好配置就可以了。
```javascript
// src/conifg/index.default.js
// ...
module.exports = {
  // ...
  grpc: {
    pbPathsRegExp:
      process.cwd() +
      "/node_modules/@quancheng/**/src/main/proto/**/*_service.proto", // pb文件位置
    pemPath: process.cwd() + "/grpc.pem", // grpc证书路径
    retry: 5, // 重试次数
    services: { // services包名映射
      UserService: "com.quancheng.zeus.service.UserService:zeus-service:1.0.0",
      CompanyService:
        "com.quancheng.zeus.service.CompanyService:zeus-service:1.0.0",
      AccountService:
        "com.quancheng.zeus.service.AccountService:zeus-service:1.0.0"
    },
    options: { // 其它grpc配置
      "grpc.ssl_target_name_override": "grpc",
      "grpc.default_authority": "grpc"
    }
  }
  // ...
}

```
之后就可以在api或者servcie内通过this.grpc.UserService取到的UserService实例。