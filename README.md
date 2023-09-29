# XRay 全平台部署

## 1. 创建服务器

### 1.1. 注册账户

在下面网页正中间区域填写要注册的账号密码，点击 Create account
该网址为我的邀请网址，通过此链接跳转到 vultr 官网注册会有额外奖励

```bash
https://www.vultr.com/?ref=8907593
```

### 1.2. 添加防火墙组

```bash
Products-Firewall-Add Firewall Group:
Description:allow 22, 80, 443
Inbound IPv4 Rules:
accept SSH 22 Anywhere 0.0.0.0/0 +
accept HTTP 80 Anywhere 0.0.0.0/0 +
accept HTTPS 443 Anywhere 0.0.0.0/0 +
```

### 1.3. 添加 SSH 公钥

```bash
右上角your account name-Profile-SSH Keys-Add SSH Key
```

### 1.4. 申请服务器

服务器平台

```bash
vultr
```

服务器系统

```bash
Debian 12 x64
```

服务器地址

```bash
韩国(推荐)
新加坡(第二)
日本(第三,用户量过大)
```

并选择对应的 Firewall 和 SSH Key

## 2. 创建域名

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
wget -P /root -N --no-check-certificate "https://raw.githubusercontent.com/mack-a/v2ray-agent/master/install.sh" && chmod 700 /root/install.sh && /root/install.sh
```

选择安装、Tuic安装

```bash
1
and
vasma->6->1
```

## 获取订阅链接

```bash
vasma->7->2
```

## 安装客户端

### 下载客户端

```bash
Win & Mac & Linux:
https://github.com/zzzgydi/clash-verge/releases
and download Prerelease-Alpha from
https://github.com/MetaCubeX/Clash.Meta/releases
and rename as clash-meta to replace the source file in clash verge folder

Android:
https://github.com/MatsuriDayo/NekoBoxForAndroid/releases
```

### 配置客户端

Profiles 添加订阅链接，之后前往 Proxies 选择节点

#### Extra action only for Mac & Linux

更新 clash-meta 和 provider.yaml 权限

```bash
if [ "$(uname)" == "Darwin" ]; then
	sudo chown root /Applications/Clash\ Verge.app/Contents/MacOS/clash-meta
	sudo chmod +sx /Applications/Clash\ Verge.app/Contents/MacOS/clash-meta
fi

if [ "$(uname)" == "Linux" ]; then
	sudo chown root /usr/bin/clash-meta
	sudo chmod +sx /usr/bin/clash-meta
fi

sudo chmod 777 $HOME/.config/clash-verge/*_provider.yaml
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
(默认) SOCKS5 127.0.0.1 7890
http:// HTTP 127.0.0.1 7890
https:// HTTP 127.0.0.1 7890
ftp:// (同默认)
```
启用xray情景模式即可

## 尽情享用吧~
