---
title: docker-compose容器通信
mathjax: true
date: 2021-12-05 08:57:53
tags:
    - docker
    - docker-compose
categories: docker
cover: https://cdn.jsdelivr.net/gh/303snowing/303snowing.github.io@hexo-img/202112050900995.png
---

# docker-compose容器通信常见配置方式

<!--more-->

* ## 直接通过IP进行通信

* ## 映射hosts记录到容器hosts文件中

* ## 使用环境变量配置目标主机地址

* ## 使用`links`标签通过容器名称访问

# docker-compose内的service互相通信

此类方式适用于一个docker-compose.yml文件编排了一个系统的多个service，一个docker-compose.yml默认是用的是一个network网关，不需要往宿主机暴露端口，可直接使用service名称访问对应的容器。

使用service名称进行通信，见如下文件37行：

```yaml
version: '3'

services:
  db:
    image: mysql/mysql-server:5.6
    restart: always
    container_name: "mysql-webstack-laravel"
    environment:
      MYSQL_ROOT_PASSWORD: xxx
      MYSQL_DATABASE: webstack
      MYSQL_USER: webstack
      MYSQL_PASSWORD: xxx
    volumes:
      - ./data:/var/lib/mysql
    command: --default-authentication-plugin=mysql_native_password --explicit_defaults_for_timestamp
    networks:
      - "webstacknet"
  redis:
    image: redis:3
    container_name: "redis-webstack-laravel"
    restart: always
    networks:
      - "webstacknet"
  webstack:
    image: arvon2014/webstack-laravel:v1.2.1
    container_name: "webstack-laravel"
    restart: always
    ports:
      - 8000:8000
    volumes: 
      - ./app:/opt/navi
    depends_on:
      - "db"
      - "redis"
    environment:
      LOGIN_COPTCHA: "false"
      DB_HOST: db	# 这里使用的db就是第4行的db，名称保持一致即可通信
      DB_PORT: 3306
      DB_DATABASE: webstack
      DB_USERNAME: webstack
      DB_PASSWORD: xxx
    # command: ['/entrypoint.sh','new-server']
    command: ['/entrypoint.sh','serve']
    networks:
      - "webstacknet"
networks:
  webstacknet:
    driver: bridge

```



---

# docker-compose内的service与宿主机进行通信

首先需要在docker-compose.yml文件中的`service`下面声明：

```yaml
extra_hosts:
      - "host.docker.internal:host-gateway"
```

不通平台内容有区别：

> * MAC: `docker.for.mac.host.internal`
> * Windows/Linux: `host.docker.internal`

完整示例docker-compose.yml如下：

```yaml
version: "3.2"

services:
  hertzbeat:
    #使用的镜像
    image: tancloud/hertzbeat:1.0-beta.7
    #定义主机名
    container_name: hertzbeat
    #容器的映射端口
    ports:
      - 1157:1157
    extra_hosts:
      - "host.docker.internal:host-gateway"
    network_mode: bridge
    #定义挂载点         
    volumes:
      - /etc/timezone:/etc/timezone
      - /etc/localtime:/etc/localtime
      - ./application.yml:/opt/hertzbeat/config/application.yml
      - ./sureness.yml:/opt/hertzbeat/config/sureness.yml
    #docker 重启后，容器自启动
    restart: always
```

在应用内有配置文件如下（见第6行）：

```yaml
warehouse:
  store:
    td-engine:
      enabled: true
      driver-class-name: com.taosdata.jdbc.rs.RestfulDriver
      url: jdbc:TAOS-RS://host.docker.internal:6041/hertzbeat	# 此处的host.docker.internal:6041就是宿主机的6041端口
      username: root
      password: xxx
```





---

# docker-compose内的service与其他已有容器进行通信

