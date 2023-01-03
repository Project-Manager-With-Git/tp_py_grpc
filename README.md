# tp_py_grpc

python的grpc组件及模板.

python构造服务在性能方面不占优势,唯一可以想到的原因有如下:

1. 希望使用其计算库,python是多数计算库的接口语言,比如pytorch,pandas等这是别的语言没有的优势.
2. 对并发性能要求不高,但要求快速开发快速迭代.这种需求一般用在工具型应用上,用啥不重要因为用户基本不会太多(最多万级),且对体验有一定容忍度.很少有像python这样可以半天弄出个能跑的服务的编程语言.

rpc的形式相比较起通常的http接口更加接近本地调用的模式,对于使用者来说学习门槛更低,因此在后端的计算密集型任务常用rpc.grpc是当今最流行的rpc协议,因此这个模版会比较常用.虽然grpc一般用在计算密集型任务中,但python天然锁进程核心数,所以一般来说我们的grpc服务还是单进程任务,如果要增加算力我们可以多开.

## 项目组织形式

本项目是sanic项目的模板,使用分支管理组件和模版的开发,tag固定版本,

+ dev分支:维护最新的的组件,组件tag全部从这里分出,统一使用cp-0.0.0作为前缀
+ master分支用于测试各种模版配置,模版tag全部从这里分出,统一使用api-0.0.0这样的形式,前缀分为:
    + `sync`,同步接口形式的grpc服务
    + `aio`,异步接口形式的grpc服务
    + `syncnogen`,同步接口形式的grpc服务,但直接解析pb定义文件
    + `aionogen`,异步接口形式的grpc服务,但直接解析pb定义文件

## 用法说明

使用模版构造项目后可以进行如下进一步操作:

+ 调试

    使用[grpcurl](https://github.com/fullstorydev/grpcurl)

+ 增加sdk

    + `ppm project add tp_py_grpc@cp-0.0.1//aiossecli --located-path=aiossecli.py` 异步sse客户端
    + `ppm project add tp_py_grpc@cp-0.0.1//ssecli --located-path=ssecli.py` 同步sse客户端
    + `ppm project add tp_py_grpc@cp-0.0.1//aiowscli --located-path=aiowscli.py` 异步websocket客户端
    + `ppm project add tp_py_grpc@cp-0.0.1//wscli --located-path=wscli.py` 同步websocket客户端

+ 添加拦截器功能组件
    + `ppm project add tp_py_grpc@cp-0.0.1//aio_serv_interceptor --located-path=testpygrpc/interceptor --kv=source::timer`增加异步服务端拦截器
    + `ppm project add tp_py_grpc@cp-0.0.1//sync_serv_interceptor --located-path=testpygrpc/interceptor --kv=source::timer`增加同步服务端拦截器
    + `ppm project add tp_py_grpc@cp-0.0.1//aio_serv_interceptor_source --located-path=testpygrpc/interceptor/timer.py --kv=source::timer`增加异步服务端拦截器的模板文件
    + `ppm project add tp_py_grpc@cp-0.0.1//sync_serv_interceptor_source --located-path=testpygrpc/interceptor/timer.py --kv=source::timer`增加同步服务端拦截器的模板文件

    + `ppm project add tp_py_grpc@cp-0.0.1//aio_sdk_interceptor --located-path=testpygrpc/sdk/interceptor --kv=source::timer`增加异步sdk拦截器
    + `ppm project add tp_py_grpc@cp-0.0.1//sync_sdk_interceptor --located-path=testpygrpc/sdk/interceptor --kv=source::timer`增加同步服务端拦截器
    + `ppm project add tp_py_grpc@cp-0.0.1//aio_sdk_interceptor_source --located-path=testpygrpc/sdk/interceptor/timer.py --kv=source::timer`增加异步sdk拦截器的模板文件
    + `ppm project add tp_py_grpc@cp-0.0.1//sync_sdk_interceptor_source --located-path=testpygrpc/sdk/interceptor/timer.py --kv=source::timer`增加同步服务端拦截器的模板文件

### 服务端使用拦截器

1. 在`serv.py`中`from interceptor.timer import Interceptor`
2. 在`self.xds_serv(...)`或`self.common_serv(...)`中最后添加`Interceptor()`作为参数