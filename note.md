## 小问题记录
### 1.关于加速器Watt Toolkit 的原理及其副作用
本地反向代理（基于YARP）+ 自动优选GitHub可用IP + 两种流量接管模式（Hosts / 系统代理），定向只加速GitHub相关域名，不是全局代理，也不是VPN
副作用就是IP库依赖作者更新，异常卡退可能会残留host记录，Git https模式容易证书报错，校园网有时候测速出来的IP仍然拥堵
>YARP(Yet Another Reverse Proxy):一个用来用来做HTTP/HTTPS请求转发的代码工具包

** 注意！**
1. 优先用hosts模式
2. Git推拉固定用SSH
3. 不要长期挂后台，不用就关了！！！！


### 2.Github为何会如此卡
1. 跨境出口带宽资源有限，高峰拥塞
2. DNS污染，域名解析返回无效IP
> DNS （域名系统）（Domain Name System）把 github.com 翻译成服务器IP
3. 跨境链路随机丢包，TCP重传放大卡顿
> TCP 传输控制协议（Transmission Control Protocol）传输层的协议，面向连接、可靠传输，有重传、确认机制
4. 静态资源独立域名  githubusercontent  污染更严重
5. 出口QoS流量限速
> QoS 服务质量（Quality of Service）流量整形、优先级管控。运营商/校园网会在出口给不用的流量分优先级

3.一些名词的解释记录
DNS（Domain Name System）域名系统
作用：域名 ↔ IP地址翻译。
> 比如把  github.com  翻译成服务器IP。
> DNS污染：解析的时候给你返回假IP。

 
TCP (Transmission Control Protocol) 传输控制协议
传输层协议，面向连接、可靠传输，有重传、确认机制。
< 网页、HTTPS、Git HTTPS底层都是TCP；丢包就要重传，所以跨境丢包会很卡。

 
UDP (User Datagram Protocol) 用户数据报协议
无连接，不保证送达，没有重传。
> DNS查询默认走UDP。

 
CDN (Content Delivery Network) 内容分发网络
就近缓存静态资源（图片、js、徽章）。
> GitHub的头像、README卡片图放在  githubusercontent.com ，就是它的CDN域名。

 
QoS (Quality of Service) 服务质量
流量整形、优先级管控,运营商/校园网在出口给不同流量分优先级。

 
HTTPS (HyperText Transfer Protocol Secure) 超文本传输安全协议
HTTP + TLS加密。网页浏览、https方式git clone用这个。
中间人代理需要证书才能解密。

 
TLS (Transport Layer Security) 传输层安全协议
前身SSL，HTTPS的加密层，负责加密、身份校验（证书）。
> SSL是旧版本，现在标准叫TLS。

 
SSH (Secure Shell) 安全外壳协议
加密远程连接协议，你现在  git@github.com  推拉代码用的就是SSH。
> SSH不走HTTPS代理、不需要中间人解密证书。

 
CA (Certificate Authority) 证书颁发机构
签发数字证书的组织。
> Watt Toolkit自己生成一个自签名CA根证书，用来做HTTPS中间人转发。

 
YARP (Yet Another Reverse Proxy) 又一个反向代理
微软.NET开源反向代理库
> Watt Toolkit用来做本地流量转发。

 
IP
Internet Protocol 网际协议
> 网络层协议，IP地址就是主机在互联网上的编号。

 
MTR (My Traceroute)
网络排查工具，组合 ping + traceroute，看整条链路每一跳的丢包、延迟。
> ping (Packet Internet Groper)
基于ICMP，测试连通性、延迟。

 
ICMP (Internet Control Message Protocol) 互联网控制报文协议
用来发连通检测、报错消息，ping命令底层协议。

 
Hosts
Windows本地静态域名映射表，优先级高于DNS。Watt可以往这里写入：域名→IP。

 
repo (repository) 仓库
> GitHub里的仓库，大家简写repo，就是存放代码、README的仓库。

 
commit
一次提交快照，保存版本。

 
SSH Key：非对称密钥，公钥放到GitHub，免密码推拉仓库
​

RSA：一种非对称加密算法，SSH密钥常用RSA

​
HTTPS Token：个人访问令牌，HTTPS方式git登录验证用

​
TOC：Table of Contents 目录（Markdown里的目录）
