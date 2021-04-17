---
title: golang环境配置
mathjax: true
date: 2021-04-14 13:31:30
tags: 
	- 编程
	- golang
categories: golang
cover: https://cdn.jsdelivr.net/gh/303snowing/303snowing.github.io@hexo-img/footer-gopher.jpg
---

# 官方网站

* 中文文档：<http://docscn.studygolang.com/>
* go语言中文网：<https://studygolang.com/>

<!--more-->

# 安装golang环境（使用zip方式安装，Windows10操作系统）

1. 下载二进制包

    下载地址：<https://studygolang.com/dl> ，下载`gox.x.x.windows-amd64.zip`文件到电脑上

    ![image-20210414134833354](https://cdn.jsdelivr.net/gh/303snowing/303snowing.github.io@hexo-img/image-20210414134833354.png)

2. 解压到指定目录，如`D:/go`，解压后如图所示

    ![image-20210414135008377](https://cdn.jsdelivr.net/gh/303snowing/303snowing.github.io@hexo-img/image-20210414135008377.png)

3. 配置环境变量

    * 创建`D:\go\env`文件，存放go的环境变量

        打开cmd，执行`go env`命令，将打印的结果复制到`D:\go\env`文件中，删除所有的`set`命令，只保留`KEY=VALUE`格式的变量，如下内容，根据自己的go解压路径自行调整

        ```bash
        GO111MODULE=
        GOARCH=amd64
        GOBIN=
        GOCACHE=D:\go-build
        GOENV=D:\go\env
        GOEXE=.exe
        GOFLAGS=
        GOHOSTARCH=amd64
        GOHOSTOS=windows
        GOINSECURE=
        GOMODCACHE=D:\go\pkg\mod
        GONOPROXY=
        GONOSUMDB=
        GOOS=windows
        GOPATH=D:\go
        GOPRIVATE=
        GOPROXY=https://goproxy.cn
        GOROOT=D:\go
        GOSUMDB=sum.golang.org
        GOTMPDIR=
        GOTOOLDIR=D:\go\pkg\tool\windows_amd64
        GOVCS=
        GOVERSION=go1.16.3
        GCCGO=gccgo
        AR=ar
        CC=gcc
        CXX=g++
        CGO_ENABLED=1
        GOMOD=NUL
        CGO_CFLAGS=-g -O2
        CGO_CPPFLAGS=
        CGO_CXXFLAGS=-g -O2
        CGO_FFLAGS=-g -O2
        CGO_LDFLAGS=-g -O2
        PKG_CONFIG=pkg-config
        ```

    * 需要配置的环境变量：
        * PATH：添加D:\go\bin

            ![image-20210414135654765](https://cdn.jsdelivr.net/gh/303snowing/303snowing.github.io@hexo-img/image-20210414135654765.png)

        * GOENV=D:\go\env

            ![image-20210414135828882](https://cdn.jsdelivr.net/gh/303snowing/303snowing.github.io@hexo-img/image-20210414135828882.png)

4. **查看环境变量应该如下打印**

    ```bash
    C:\Users\xxx>go env
    set GO111MODULE=
    set GOARCH=amd64
    set GOBIN=
    set GOCACHE=D:\go-build
    set GOENV=D:\go\env
    set GOEXE=.exe
    set GOFLAGS=
    set GOHOSTARCH=amd64
    set GOHOSTOS=windows
    set GOINSECURE=
    set GOMODCACHE=D:\go\pkg\mod
    set GONOPROXY=
    set GONOSUMDB=
    set GOOS=windows
    set GOPATH=D:\go
    set GOPRIVATE=
    set GOPROXY=https://goproxy.cn
    set GOROOT=D:\go
    set GOSUMDB=sum.golang.org
    set GOTMPDIR=
    set GOTOOLDIR=D:\go\pkg\tool\windows_amd64
    set GOVCS=
    set GOVERSION=go1.16.3
    set GCCGO=gccgo
    set AR=ar
    set CC=gcc
    set CXX=g++
    set CGO_ENABLED=1
    set GOMOD=NUL
    set CGO_CFLAGS=-g -O2
    set CGO_CPPFLAGS=
    set CGO_CXXFLAGS=-g -O2
    set CGO_FFLAGS=-g -O2
    set CGO_LDFLAGS=-g -O2
    set PKG_CONFIG=pkg-config
    set GOGCCFLAGS=-m64 -mthreads -fno-caret-diagnostics -Qunused-arguments -fmessage-length=0 -fdebug-prefix-map=C:\Users\303sn\AppData\Local\Temp\go-build3612435218=/tmp/go-build -gno-record-gcc-switches
    ```

    

# 配置goland

* goland自行下载：<https://www.jetbrains.com/go/>

    1. 使用`go module`方式新建项目，路径名字自行定义

    2. 创建完成后如图

        ![image-20210414141427103](https://cdn.jsdelivr.net/gh/303snowing/303snowing.github.io@hexo-img/image-20210414141427103.png)

    3. 编写测试代码

        ```golang
        package main
        
        import (
        	"fmt"
        	"github.com/gogf/gf"
        )
        
        func main() {
        	fmt.Println("hello GF", gf.VERSION)
        }
        ```

    4. 同步依赖，鼠标右击`go.mod`文件，点击`Sync Go Module`同步按钮同步依赖

        ![image-20210414143048002](https://cdn.jsdelivr.net/gh/303snowing/303snowing.github.io@hexo-img/image-20210414143048002.png)

    5. 运行

        ![image-20210414143318911](https://cdn.jsdelivr.net/gh/303snowing/303snowing.github.io@hexo-img/image-20210414143318911.png)