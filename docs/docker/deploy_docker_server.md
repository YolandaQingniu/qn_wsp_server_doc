# 部署服务器Docker

服务器SDK采用Docker镜像的方式进行分发, 需开发者理解并掌握Docker

## 读取镜像
`vim Dockerfile`
```Dockerfile
FROM registry.cn-shenzhen.aliyuncs.com/yolanda/wsp_open:v1.0.18
```

## 配置环境变量
WSP_DOMAIN为三方服务器访问地址, 注意不要有空格
SUPPORT_READ_MODEL_ID_FLAG为是否需要特殊支持read_model_id接口标识, 该环境变量配合read_model_id接口使用, 以保证多实例部署时服务器发送的model_id始终是正常, 若需则设为1, 否则可以不考虑

`vim main.env`
```
WSP_DOMAIN=https://abc.com
```

## 启动容器
```shell
docker build . -t wsp_server
docker run -p 3000:3000 --env-file main.env wsp_server
```
