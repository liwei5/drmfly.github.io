---

layout: post

title: 自动化API测试服务[Titer]设计

categories: [automation,test,titer]

description: 自动化API测试服务设计

keywords: titer,automation,test,API

---

> 基于golang开发RESTful API自动化测试服务，支持分布式测试runner，runner运行在docker容器上，容器在创建时自动加入集群，支持大规模压力测试。

### 概念
- master 测试主控节点 负责调度runner server执行测试任务。
- node/runner 测试从节点 负责执行测试用例，输出测试报告
- tester 测试人员
- case 测试任务(用例) 配置包含名称、描述
- pipeline 任务流水线
- peer 管道节点对应某API测试任务 parent 父节点  
- branch pipeline 中的分支
- junction pipe branch junction 管道分支聚合点 拥有2个父节点
- report 测试报告 包含测试接口名称，响应时间，请求头信息，请求参数，请求报文。

### 技术选型
- 使用golang语言开发
- master 与 node 之间使用 golang rpc（http)库通信
- 选用redis支持控制台登录令牌管理。etcd存储测试配置信息。

### 设计概述
基于golang开发RESTful API自动化测试服务，支持分布式测试runner，runner运行在容器上，docker run容器时自动加入集群。支持大规模压力测试。

master与node/runner之间通过REST golang RPC 通信

runner 以job为单位执行任务

测试节点加入集群时，从master获取etcd等配置信息。

### 模块设计
- Master 负责测试任务调度分派、同时提供api-server 供web console、客户端工具调用 后续提供基于golang编译的不同平台（Win、Mac、Linux）的ctl(客户端工具) 方便测试用例管理、任务流水线配置、获取测试报告等
- Runner  执行具体测试任务（流水线工作），接受的任务以整个用例为单位。
- Console 控制台，前端控制台，为用户提供可视化的用例管理、测试流水线作业配置

起名为:titer

待续。。。

github(https://github.com/changhongio/titer)

转载请注明出处，本文采用 [CC4.0](http://creativecommons.org/licenses/by-nc-nd/4.0/) 协议授权










