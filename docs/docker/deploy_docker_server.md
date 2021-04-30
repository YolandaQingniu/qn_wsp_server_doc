# 部署服务器Docker

服务器SDK采用Docker镜像的方式进行分发, 需开发者理解并掌握Docker

## 读取镜像
`vim Dockerfile`
```Dockerfile
FROM registry.cn-shenzhen.aliyuncs.com/yolanda/wsp_open:v1.0.11
```

## 配置环境变量
WSP_DOMAIN为三方服务器访问地址, 注意不要有空格

`vim main.env`
```
WSP_DOMAIN=https://abc.com
```

## 启动容器
```shell
docker build . -t wsp_server
docker run -p 3000:3000 --env-file main.env wsp_server
```
