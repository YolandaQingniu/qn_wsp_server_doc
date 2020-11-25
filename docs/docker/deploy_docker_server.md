# 部署服务器Docker

服务器SDK采用Docker镜像的方式进行分发, 需开发者理解并掌握Docker

## 读取镜像
`vim Dockerfile`
```Dockerfile
FROM registry.cn-shenzhen.aliyuncs.com/yolanda/wsp_open:v1.0.9
```

## 配置环境变量
`vim main.env`
```
WSP_DOMAIN=http://wsp-demo.yolanda.hk         # [必填项] 第三方服务器地址
AUTHORIZATION="Basic ZHVtbXk6MTIzNDU2Nzg="    # [选填项] 验签头部, 默认为空
CUSTOM_OTA_SERVER=http://wsp-demo.yolanda.hk  # [选填项] 自定义OTA服务器, 默认Yolanda自带的OTA升级
CUSTOM_ALGORITHM=01                           # [选填项] 自定义算法, 默认01
PORT=3000                                     # [选填项] 服务器监听端口, 默认3000
TZ=Asia/Shanghai                              # [选填项] 服务器时区, 默认Asia/Shanghai
```

## 启动容器
```shell
docker build . -t wsp_server
docker run --env-file main.env wsp_server
# docker run --env-file main.env wsp_server -d # 后台启动
```
