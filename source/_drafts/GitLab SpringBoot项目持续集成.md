---
title: GitLab SpringBoot项目持续集成
mathjax: true
date: 2021-04-17 14:47:32
tags:
	- CI/CD
	- GitLab
	- SpringBoot
categories: JAVA
cover: https://cdn.jsdelivr.net/gh/303snowing/303snowing.github.io@hexo-img/20210417151947.png
---

**所有的环境都是基于docker的**，本文会给出涉及到的docker-compose.yml编排文件，使用docker-compose工具可以方便的拉起容器

<!--more-->

# 服务器安装Docker环境

1. 直接看官方文档就行：<https://docs.docker.com/engine/install/>

2. 需要安装`docker-compose编排工具`：<https://docs.docker.com/compose/install/>

3. 以上完成后，服务器应该能执行下面两条命令：

    1. `docker`命令

    ```bash
    snowing@303snowing:~$ docker version
    Client: Docker Engine - Community
     Cloud integration: 1.0.12
     Version:           20.10.5
     API version:       1.41
     Go version:        go1.13.15
     Git commit:        55c4c88
     Built:             Tue Mar  2 20:17:50 2021
     OS/Arch:           linux/amd64
     Context:           default
     Experimental:      true
    
    Server: Docker Engine - Community
     Engine:
      Version:          20.10.5
      API version:      1.41 (minimum version 1.12)
      Go version:       go1.13.15
      Git commit:       363e9a8
      Built:            Tue Mar  2 20:15:47 2021
      OS/Arch:          linux/amd64
      Experimental:     false
     containerd:
      Version:          1.4.4
      GitCommit:        05f951a3781f4f2c1911b05e61c160e9c30eaa8e
     runc:
      Version:          1.0.0-rc93
      GitCommit:        12644e614e25b05da6fd08a38ffa0cfe1903fdec
     docker-init:
      Version:          0.19.0
      GitCommit:        de40ad0
    ```

    2. `docker-compose`命令

    ```bash
    snowing@303snowing:~$ docker-compose version
    docker-compose version 1.29.0, build 07737305
    docker-py version: 5.0.0
    CPython version: 3.7.10
    OpenSSL version: OpenSSL 1.1.0l  10 Sep 2019
    ```

# 准备