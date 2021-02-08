<!--
 * @Author: Jason_Ma
 * @Date: 2021-01-18 22:21:48
 * @LastEditors: Jason_Ma
 * @LastEditTime: 2021-01-23 22:09:28
 * @FilePath: /gitbook/Chapter2/README.md
-->
 [mongoDB 安装使用]
============================
 1. 关于mongoDB 数据库
============================
MongoDB 官网https://www.mongodb.com
1. MongoDB 是由C++语言编写的，是一个基于分布式文件存储的开源数据库系统。
2. MongoDB 可在高负载的情况下，添加更多的节点，可以保证服务器性能。
3. MongoDB 可为Web应用提供可扩展的高性能数据存储解决方案。
4. MongoDB 将数据存储在灵活的json文档中，这意味着可以直接得到从文档到文档的数据、结构等。
5. MongoDB 是免费使用的（MongoDB分 社区版[在所有环境下都免费] 和 企业版[在开发环境免费，生产环境收费]两个版本）。
6. MongoDB 数据库具有可伸缩性和灵活性，可帮助你快速查询和索引你需要数据。   


2. mongoDB 安装
============================
2. 官网下载https://www.mongodb.com/try/download/community?jmp=nav 并解压 usr/local/mongodb 
3. 运行  brew tap mongodb/brew ，可能需要等待几分钟
4. 运行  brew install mongodb-community@4.2  安装社区版@4.2
5. 添加路径 vim .bash_profile   

```
# mongodb
export PATH="$PATH:/usr/local/mongodb/bin"
``` 

这一步除了安装二进制文件，还会添加下面文件
> * 配置文件 (/usr/local/etc/mongod.conf)
> * 日志目录路径 (/usr/local/var/log/mongodb)
>* 数据目录路径 (/usr/local/var/mongodb) 数据库文件都存在这里

此时运行  mongod -version  会打印出安装版本证明安装成功。  
```
lhhdembp:~ lhm$ mongod -version 
db version v4.4.3
Build Info: {
    "version": "4.4.3",
    "gitVersion": "913d6b62acfbb344dde1b116f4161360acd8fd13",
    "modules": [],
    "allocator": "system",
    "environment": {
        "distarch": "x86_64",
        "target_arch": "x86_64"
    }
}
```


1. 启动mongoDB 服务
============================

使用 brew 将 MongoDB 作为 macOS 服务运行
```
# 启动
brew services start mongodb-community
# 停止
brew services stop mongodb-community
```
可以通过下面命令查看正在运行的 MongoDB 服务 
```
ps aux | grep -v grep | grep mongod
```  
4. 连接并使用 MongoDB
==========================

首先要启动 MongoDB 服务。

运行  mongo  连接服务，可以看到成功连接 mongo 服务。

