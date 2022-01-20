---
title: Kubernetes基本概念
tags:
  - K8S
categories: K8S
mathjax: true
cover: >-
  https://cdn.jsdelivr.net/gh/303snowing/303snowing.github.io@hexo-img/202201201613432.png
date: 2022-01-20 16:36:23
---


# Kubernetes是什么

Kubernetes是容器集群管理系统，是一个开源的平台，可以实现容器集群的自动化部署、自动扩缩容、维护等功能。

<!-- more -->

通过Kubernetes你可以：

- 快速部署应用
- 快速扩展应用
- 无缝对接新的应用功能
- 节省资源，优化硬件资源的使用

# Kubernetes 特点

- **可移植**: 支持公有云，私有云，混合云，多重云（multi-cloud）
- **可扩展**: 模块化, 插件化, 可挂载, 可组合
- **自动化**: 自动部署，自动重启，自动复制，自动伸缩/扩展



容器优势总结：

- **快速创建/部署应用：**与VM虚拟机相比，容器镜像的创建更加容易。
- **持续开发、集成和部署：**提供可靠且频繁的容器镜像构建/部署，并使用快速和简单的回滚(由于镜像不可变性)。
- **开发和运行相分离：**在build或者release阶段创建容器镜像，使得应用和基础设施解耦。
- **开发，测试和生产环境一致性：**在本地或外网（生产环境）运行的一致性。
- **云平台或其他操作系统：**可以在 Ubuntu、RHEL、 CoreOS、on-prem、Google Container Engine或其它任何环境中运行。
- **Loosely coupled，分布式，弹性，微服务化：**应用程序分为更小的、独立的部件，可以动态部署和管理。
- **资源隔离**
- **资源利用：**更高效

# 使用Kubernetes能做什么？

可以在物理或虚拟机的Kubernetes集群上运行容器化应用，Kubernetes能提供一个以“**容器为中心的基础架构**”，满足在生产环境中运行应用的一些常见需求，如：

- [多个进程（作为容器运行）协同工作。](http://docs.kubernetes.org.cn/312.html)（Pod）
- 存储系统挂载
- Distributing secrets
- 应用健康检测
- [应用实例的复制](http://docs.kubernetes.org.cn/314.html)
- Pod自动伸缩/扩展
- Naming and discovering
- 负载均衡
- 滚动更新
- 资源监控
- 日志访问
- 调试应用程序
- [提供认证和授权](http://docs.kubernetes.org.cn/51.html)

# Kubernetes不是什么？

Kubernetes并不是传统的PaaS（平台即服务）系统。

- Kubernetes不限制支持应用的类型，不限制应用框架。不限制受支持的语言runtimes (例如, Java, Python, Ruby)，满足[12-factor applications](https://12factor.net/) 。不区分 “apps” 或者“services”。 Kubernetes支持不同负载应用，包括有状态、无状态、数据处理类型的应用。只要这个应用可以在容器里运行，那么就能很好的运行在Kubernetes上。
- Kubernetes不提供中间件（如message buses）、数据处理框架（如Spark）、数据库(如Mysql)或者集群存储系统(如Ceph)作为内置服务。但这些应用都可以运行在Kubernetes上面。
- Kubernetes不部署源码不编译应用。持续集成的 (CI)工作流方面，不同的用户有不同的需求和偏好的区域，因此，我们提供分层的 CI工作流，但并不定义它应该如何工作。
- Kubernetes允许用户选择自己的日志、监控和报警系统。
- Kubernetes不提供或授权一个全面的应用程序配置 语言/系统（例如，[jsonnet](https://github.com/google/jsonnet)）。
- Kubernetes不提供任何机器配置、维护、管理或者自修复系统。

另一方面，大量的Paas系统都可以运行在Kubernetes上，比如Openshift、Deis、Gondor。可以构建自己的Paas平台，与自己选择的CI系统集成。

由于Kubernetes运行在应用级别而不是硬件级，因此提供了普通的Paas平台提供的一些通用功能，比如部署，扩展，负载均衡，日志，监控等。这些默认功能是可选的。

另外，Kubernetes不仅仅是一个“编排系统”；它消除了编排的需要。“编排”的定义是指执行一个预定的工作流：先执行A，之B，然C。相反，Kubernetes由一组独立的可组合控制进程组成。怎么样从A到C并不重要，达到目的就好。当然集中控制也是必不可少，方法更像排舞的过程。这使得系统更加易用、强大、弹性和可扩展。
