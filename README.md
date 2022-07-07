# XRay 全平台部署

<!-- TOC -->

- [XRay 全平台部署](#xray-%E5%85%A8%E5%B9%B3%E5%8F%B0%E9%83%A8%E7%BD%B2)
    - [创建服务器](#%E5%88%9B%E5%BB%BA%E6%9C%8D%E5%8A%A1%E5%99%A8)
        - [注册账户](#%E6%B3%A8%E5%86%8C%E8%B4%A6%E6%88%B7)
        - [添加防火墙组](#%E6%B7%BB%E5%8A%A0%E9%98%B2%E7%81%AB%E5%A2%99%E7%BB%84)
        - [添加 SSH 公钥](#%E6%B7%BB%E5%8A%A0-ssh-%E5%85%AC%E9%92%A5)
        - [申请服务器](#%E7%94%B3%E8%AF%B7%E6%9C%8D%E5%8A%A1%E5%99%A8)
    - [创建域名](#%E5%88%9B%E5%BB%BA%E5%9F%9F%E5%90%8D)
        - [创建 A 记录](#%E5%88%9B%E5%BB%BA-a-%E8%AE%B0%E5%BD%95)
    - [部署 XRay](#%E9%83%A8%E7%BD%B2-xray)
    - [保存 XRay 安装信息](#%E4%BF%9D%E5%AD%98-xray-%E5%AE%89%E8%A3%85%E4%BF%A1%E6%81%AF)
    - [安装客户端](#%E5%AE%89%E8%A3%85%E5%AE%A2%E6%88%B7%E7%AB%AF)
        - [下载 XRay 内核](#%E4%B8%8B%E8%BD%BD-xray-%E5%86%85%E6%A0%B8)
        - [下载客户端](#%E4%B8%8B%E8%BD%BD%E5%AE%A2%E6%88%B7%E7%AB%AF)
        - [配置客户端](#%E9%85%8D%E7%BD%AE%E5%AE%A2%E6%88%B7%E7%AB%AF)
            - [Qv2ray 配置](#qv2ray-%E9%85%8D%E7%BD%AE)
            - [v2rayNG 配置](#v2rayng-%E9%85%8D%E7%BD%AE)
    - [浏览器使用](#%E6%B5%8F%E8%A7%88%E5%99%A8%E4%BD%BF%E7%94%A8)
    - [重新部署](#%E9%87%8D%E6%96%B0%E9%83%A8%E7%BD%B2)
    - [尽情享用吧~](#%E5%B0%BD%E6%83%85%E4%BA%AB%E7%94%A8%E5%90%A7)

<!-- /TOC -->

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
Debian 11 x64
```
服务器地址
```bash
韩国(推荐)
新加坡(第二)
日本(第三,用户量过大)
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
or
wget -N --no-check-certificate -q -O install.sh "https://raw.githubusercontent.com/wulabing/Xray_onekey/main/install.sh" && chmod +x install.sh && bash install.sh
```
选择并存模式

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
