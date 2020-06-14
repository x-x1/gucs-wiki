# GUCS 升级部署手册

[![Documentation chat](https://img.shields.io/badge/gitter-Docs%20chat-4AB495.svg)](#)

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [升级功能](#%E5%8D%87%E7%BA%A7%E5%8A%9F%E8%83%BD)
- [版本信息](#%E7%89%88%E6%9C%AC%E4%BF%A1%E6%81%AF)
- [环境信息](#%E7%8E%AF%E5%A2%83%E4%BF%A1%E6%81%AF)
- [升级步骤](#%E5%8D%87%E7%BA%A7%E6%AD%A5%E9%AA%A4)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## 升级概要

* 升级功能：解决回执中交易状态可见性问题；
* 升级块高: `410600`
* 升级时间估约：2020-6-14 22:00:00 


## 版本信息

| 版本 | md5摘要 |
|:---|:---|
| `release/gucs-v1.1.0` | `c704c658a0c6e5d828a66ff392c640c3` |


## 环境信息 

| 配置项 | 建议值 | 描述 |
|:---|:---|:---|
| 操作系统 | `Ubuntu 16.04` | 建议使用该系统作为节点的运行环境 |
| 内存 | `4G` | 建议内存值 |
| CPU | `2核` | 建议CPU核数 |
| 磁盘 | `500G` | 建议的磁盘容量，机械或SSD均可 |
| P2P端口 | `26781` | P2P端口设置为该值，同时注意防火墙已开放该端口 |


## 升级步骤

1. 关闭进程

请勿使用暴力的方式关闭进程，关闭进程建议使用 `kill PID` 关闭进程，请不要加上 `-9` 的参数；

2. 数据备份

将整个节点数据进行备份，假设节点目录为： `/root/node`， 节点数据目录为：`/root/node/data`，此时请备份整个目录：

```
cp -rp /root/node /root/nodeback
```

3. 获取安装包

[点击下载](https://github.com/x-x1/gucs-wiki/releases/download/v1.1.0/gucs)

4. 更换 `gucs` 程序

5. 启动节点

```
./gucs --gcmode archive --networkid 106 --identity "gucs" --datadir ./data --rpc --port 26781 --rpcport 7793 
--rpcaddr 0.0.0.0 --rpcapi "db,eth,net,web3,admin,personal,miner"
```

注意：此处的各参数信息请按照实际部署的节点情况设置。

命令参数说明：

* `--networkid`: 网络ID，所有节点网络ID必须一致，此处定义为 106；
* `--gcmode`: 可选参数，加入该参数在进行余额查询时不受区块总数限制；
* `--identity`: 该参数非必须，仅用来标记该节点在网络中的名称，可以自定义；
* `--datadir`: 该参数非必须，用来指定链的数据目录，如果不指定则默认在当前用户目录下；
* `--rpc`: 该命令用于开启节点的 `JSON-RPC` 接口；
* `--port`：指定当前节点的P2P网络端口，默认为30303；
* `--rpcport`：指定JSON-RPC的访问端口；
* `--rpcapi`：指定开启JSON-RPC的哪些模块；

6. 挖矿节点启动挖矿

```
./gucs attach http://127.0.0.1:7793
```

说明：此处的RCP端口请根据实际节点填写。

启动挖矿：

```
miner.start(1)
```

查看节点是否连接上网络

```
admin.peers
```

查看出块是否正常

```
eth.blockNumber
```

说明：启动挖矿后可能需要过一会才会正常出块，DAG 需要时间初始化。














