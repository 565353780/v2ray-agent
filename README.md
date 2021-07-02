# XRay 全平台部署

@[TOC]

## 创建服务器
### 注册账户
在下面网页正中间区域填写要注册的账号密码，点击 Create account
该网址为我的邀请网址，通过此链接跳转到 vultr 官网注册会有额外奖励
```bash
https://www.vultr.com/?ref=8907594-6G
```
### 添加防火墙组
```bash
Products-Firewall-Add Firewall Group:
Description:allow 22, 80, 443
Inbound IPv4 Rules:
accept SSH 22 Anywhere 0.0.0.0/0 +
accept HTTP 80 Anywhere 0.0.0.0/0 +
accept HTTPS 443 Anywhere 0.0.0.0/0 +
```
### 添加 SSH 公钥
```bash
右上角your account name-Profile-SSH Keys-Add SSH Key
```
### 申请服务器
服务器平台
```bash
vultr
```
服务器系统
```bash
Debian 10 x64
```
并选择对应的 Firewall 和 SSH Key
## 创建域名
域名申请平台
```bash
阿里云万网域名:
https://wanwang.aliyun.com/domain/
```
需要完成
```bash
实名认证
```
### 创建 A 记录
在域名解析中创建 A 记录，指向创建的服务器IP
## 部署 XRay
在服务器上运行
```bash
bash <(curl -sL https://s.hijk.art/xray.sh)
```
选择
```bash
VLESS+TCP+XTLS
```
## 保存 XRay 安装信息
保存 XRay 安装输出的uuid，用于客户端的安装
## 安装客户端
### 下载 XRay 内核
```bash
Win & Mac & Linux:
https://github.com/XTLS/Xray-core/releases
```
### 下载客户端
```bash
Win & Mac & Linux:
https://github.com/Qv2ray/Qv2ray/releases

Android:
https://github.com/2dust/v2rayNG/releases
arm64
```
### 配置客户端
按照 XRay 安装输出的详细信息填写客户端配置
#### Qv2ray 配置
```bash
首选项-内核设置-V2Ray核心可执行文件路径:
<path-to-xray-core-folder>/xray(or xray.exe)

首选项-内核设置-V2Ray资源目录:
<path-to-xray-core-folder>/

首选项-入站设置-SOCKS设置-端口:
1080

首选项-入站设置-HTTP设置-端口:
8123

首选项-DNS设置-DNS服务器顺序:
8.8.8.8
8.8.4.4
1.1.1.1

新建：
标签:xray
主机:<服务器的IP>
端口:443
类型:VLESS
出站设置-UUID:<XRay 详细信息中的uuid>
出站设置-流控:xtls-rprx-direct
流设置-TLS设置-安全类型:XTLS
流设置-TLS设置-服务器地址(SNI):<A 记录域名全称>
```
#### v2rayNG 配置
```bash
新建-手动输入[VLESS]:
别名:xray
地址:<服务器的IP>
端口:443
用户ID:<XRay 详细信息中的uuid>
流控:xtls-rprx-direct
伪装域名:<A 记录域名全称>
底层传输安全:xtls
```
## 浏览器使用
安装插件
```bash
SwitchyOmega
```
删除所有情景模式并新建情景模式
```bash
情景模式名称:xray
请选择情景模式的类型:代理服务器
(默认) SOCKS5 127.0.0.1 1080
http:// HTTP 127.0.0.1 8123
https:// HTTP 127.0.0.1 8123
ftp:// (同默认)
```
启用xray情景模式即可
## 重新部署
仅需重新申请服务器，部署 XRay，修改客户端的uuid即可
## 尽情享用吧~
