---
layout:     post                    
title:      HTTP                  # 标题 
subtitle:   HTTP HTTPS               #副标题
date:       2020-04-12              # 时间
author:     FireWork2020                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - 技术
---

##HTTP
###工作原理
HTTP协议工作于C/S架构下，通过客户端发送请求，服务端发送响应达到通信的目的
###无状态协议
HTTP是一种不保存状态的协议，即无状态协议，HTTP自身不对请求和响应之间的通信状态进行保存。
###持久连接
HTTP/1.0之前的版本中，每进行一次HTTP通信就要断开一次TCP连接,1.0中显示指定Connection:keep-alive实现长连接。
HTTP/1.1默认支持长连接。
###管线化
持久连接使得多数请求以管线化方式放松成为可能。可以在一次连接中不用等待响应，直接发送多个请求。
###Cookie
HTTP的无状态使得无法根据之前的状态进行本次的请求处理。
##HTTPS
由于HTTP在传输过程中采用明文传输，因此造成HTTP的三大缺陷：内容可能被窃听、无法验证双方身份、无法验证报文的完整性。HTTPS的出现就是为了解决这三大问题。
###HTTPS握手过程
                客户端                         服务器
        1.Client Hello   ---------------->
                         <----------------   2.Server Hello 
                         <----------------   3.Server Certification
                         <----------------   4.Server Hello Done
                         -----------------
        5.Client evaluate certification  -                      
                         <----------------
        6.Secret Key     ---------------->
        7.Test message   ---------------->
                         <----------------   8.Test message
        

1.Client向Server发送请求到服务器，连接到Server的443端口，发送的信息内容是Random key1和客户端所支持的加密算法
2.Server收到消息后响应Client，响应内容是Random key2和匹配好的加密算法
3.Server向Client发送数字证书，内容是证书的颁发机构、过期时间、服务端的公钥、第三方认证机构(CA)的签名、服务端的域名信息
4.客户端接收证书并验证证书真实性，通过后进行下一步
5.通过Random key1、key2和预主密钥生成对称密钥，服务端同样生成对称密钥
6.客户端用对称密钥发送一条测试信息
7.服务端用对称密钥发送一条测试信息