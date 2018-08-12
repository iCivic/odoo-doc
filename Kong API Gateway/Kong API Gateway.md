### 学习 Kong API Gateway 的背景
- API的版本控制，如何做到后台应用服务器升级，而不会影响暂时没有来得及升级的App用户
- API的访问控制，如何做到一部分API是公开的，另一部分是私有的
- 最终的目的，要达到将API的管理与控制功能，与业务功能相隔离

### 搭建Kong API环境
1. 先了解Kong的一些相关资料
    - [在docker中运行kong和kong dashboard](https://www.cnblogs.com/ikodota/p/run_kong_and_kong_dashboard_in_docker.html)
    - 

2. 通过Docker安装Kong API Gateway
    - 先运行postgres数据库
    - 迁移数据
    - 运行Kong
    - 运行kong dashboard，且创建两个用户：admin/admin, kong/kong

```
docker run -d --name kong-database \
			  --restart=always \
              -p 5432:5432 \
              -e "POSTGRES_USER=kong" \
              -e "POSTGRES_DB=kong" \
              postgres:9.5
```
```
docker run --rm \
    --link kong-database:kong-database \
    -e "KONG_DATABASE=postgres" \
    -e "KONG_PG_HOST=kong-database" \
    -e "KONG_CASSANDRA_CONTACT_POINTS=kong-database" \
    kong:0.12.1-alpine kong migrations up
```

```
docker run -d --name kong \
	--restart=always \
    --link kong-database:kong-database \
    -e "KONG_PG_HOST=kong-database" \
    -e "KONG_PROXY_ACCESS_LOG=/dev/stdout" \
    -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout" \
    -e "KONG_PROXY_ERROR_LOG=/dev/stderr" \
    -e "KONG_ADMIN_ERROR_LOG=/dev/stderr" \
    -e "KONG_ADMIN_LISTEN=0.0.0.0:8001" \
    -e "KONG_ADMIN_LISTEN_SSL=0.0.0.0:8444" \
    -p 8000:8000 \
    -p 8443:8443 \
    -p 8001:8001 \
    -p 8444:8444 \
    kong:0.12.1-alpine
```

```
docker run --name kong-dashboard  \
           --restart=always  \
		   --link kong:kong  \
		   -p 8080:8080 pgbi/kong-dashboard:v2
```

在这个实验过程中，有两个问题：
1. 无法进入Kong容器

   解决办法：将kong:0.12.1-alpine 换成 kong:0.13.1-centos。
   
2. 虚拟机无法Ping通宿主机，因为我的开发环境部署在宿主机，方便我进行代码调试

   解决方法: [局域网内ping不通，防火墙规则更改（win7为例）](https://jingyan.baidu.com/article/a65957f4f557cb24e67f9ba6.html)


**收集资料**
1. Kong API 相关的资料
[[云框架]KONG API Gateway](https://github.com/cloudframeworks-apigateway)

2. WebSocket 转发
[随笔分类 - KONG](https://www.cnblogs.com/SummerinShire/category/861287.html) 

3. 小豹API网关

![image](http://www.xbgateway.com/resources/img/why_use_api.png)

4. 工作原理

![image](http://i2.51cto.com/images/blog/201801/08/1bb110f42c391c4ea631a7280e3d4fb8.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

5. 采用API Gteway 前后的区别
![image](https://getkong.org/assets/images/homepage/diagram-left.png)
![image](https://getkong.org/assets/images/homepage/diagram-right.png)

6. Kong API Gateway的技术架构
![image](https://images2015.cnblogs.com/blog/761566/201702/761566-20170210101320151-504870266.jpg)
