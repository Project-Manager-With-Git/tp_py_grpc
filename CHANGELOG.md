# v0.0.1

+ 新增对xds的支持(aio接口暂不支持)
+ 将grpc版本提升到1.51.1

## 新增组件模板

| 组件名                  | 说明                         |
| ----------------------- | ---------------------------- |
| `aio_serv_interceptor`  | grpc异步服务端模块拦截器模板 |
| `aio_sdk_interceptor`   | grpc异步sdk模块拦截器模板    |
| `sync_serv_interceptor` | grpc同步服务端模块拦截器模板 |
| `sync_sdk_interceptor`  | grpc同步sdk模块拦截器模板    |
| `aio_sdk`               | grpc异步sdk模块模板          |
| `aio_nogen_sdk`         | grpc异步sdk模块模板          |
| `sync_sdk`              | grpc同步sdk模块模板          |
| `sync_nogen_sdk`        | grpc同步sdk模块模板          |
| `main`                  | 定义项目的入口函数           |
| `servinit`              | serv作为模块时的模块入口文件 |

## 新增组件资源模版

| 组件资源名                     | 说明                             |
| ------------------------------ | -------------------------------- |
| `aio_serv_interceptor_source`  | grpc异步服务端模块拦截器文件模板 |
| `aio_sdk_interceptor_source`   | grpc异步sdk模块拦截器文件模板    |
| `sync_serv_interceptor_source` | grpc同步服务端模块拦截器文件模板 |
| `sync_sdk_interceptor_source`  | grpc同步sdk模块拦截器文件模板    |

## 新增基础组件

| 组件名           | 说明                       |
| ---------------- | -------------------------- |
| `service_schema` | 项目定义service的proto文件 |
| `aio_serv`        | grpc异步服务端模块模板     |
| `aio_nogen_serv`  | grpc异步服务端模块模板     |
| `sync_serv`       | grpc同步服务端模块模板     |
| `sync_nogen_serv` | grpc同步服务端模块模板     |
