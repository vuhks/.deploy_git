---
title: 'Hexo部署到ipv6only vps '
tags: [vps,ipv6,linux,hexo]
comments: false
date: 2020-07-21 13:34:41
abbrlink: hexo_vps
categories: hexo
description:  折腾了好几天的成果
---

# 1. DNS64

参考自[【DNS64/代理】IPv6 ONLY VPS访问IPv4资源](https://luotianyi.vc/2701.html)

由于vps没有ipv4地址，获取资源，安装软件的时候可能会导致解析不到的问题，临时修改dns地址，访问ipv4资源，这作为临时手段。也是ipv6only的vps能用的第一步操作。

```
vim /etc/resolv.conf
```

```
namesever2001:67c:2b0::4
```



# 2. 域名解析到cloudflare

使用cdn服务使ipv4地址可以通过cf的代理访问到该ipv6所在的web服务器上。

ps：AAAA 加ipv6地址，并打开proxy，即小黄云

# 3. frp内网穿透

在这一步之前，hexo d是无法操作的，因为hexo-deployer-git配置的repo只能是ipv4地址，且端口必须是22,所以通过内网穿透到带有ipv4、ipv6双栈的vps上获得ipv4的22端口的ssh服务

前，在内网穿透之前，ssh服务连接的两种途径，一种是本地支持ipv6地址，可直连，没有的话可以添加一个ipv6地址，二是通过带有ipv6地址的vps，进行千层饼操作（ssh到带有ipv6的vps上再ssh）。

## 3.1 安装并配置服务端

#### 安装frps

在有双栈ip地址的vps上安装frps，如果只有ipv4没有ipv6的vps上可以在[**Tunnel broker** ](https://www.tunnelbroker.net/)申请并添加ipv6隧道。具体可参考[为没有IPV6的VPS添加IPV6隧道](https://www.cmsky.com/tunnelbroker/)

```
cd /tmp
wget https://github.com/fatedier/frp/releases/download/v0.33.0/frp_0.33.0_linux_amd64.tar.gz
tar zxvf frp_0.33.0_linux_amd64.tar.gz
mv frp_0.33.0_linux_amd64 /etc/frps
rm -rf /etc/frp/frpc*
```

#### 配置

修改frpc.ini文件

```
[common]
bind_addr = [::]
bind_port = 5443
log_file = ./frps.log
# debug, info, warn, error
log_level = warn
log_max_days = 3
token = vuhks.top
max_pool_count = 50
tcp_mux = true
[http_proxy]
type = tcp
remote_port=10801
plugin=http_proxy          
```

启动frps服务

```
cd /etc/frps
./frps -c ./frps.ini
```



#### 也可使用一键脚本进行安装配置

[详情见github](https://github.com/MvsCode/frps-onekey)

```
wget https://raw.githubusercontent.com/MvsCode/frps-onekey/master/install-frps.sh -O ./install-frps.sh
chmod 700 ./install-frps.sh
./install-frps.sh install
```

## 3.2 安装并配置客户端

安装同上一步，在修改了dns64地址后是能够wget下载下来的

配置文件，增添ssh服务和http proxy，http proxy应该是没什么作用的，后续可能会删除。

#### 配置

```
cd /frpc
vim /frpc/frpc.ini
```

```
[common]
server_addr = [服务端的ipv6地址]
server_port = 5443
token = vuhks.top
[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 22
```

启动frpc服务

```
cd /etc/frpc
./frpc -c ./frpc.ini
```

## 3.3frpc加入系统服务并开机自启动

```
vim /etc/systemd/system/frpc.service 
```

```
[Unit]
Description=Frp Client
After=network.target syslog.target
Wants=network.target
[Service]
Type=simple
User=root
ExecStart=/etc/frpc/frpc -c /etc/frpc/frpc.ini
Restart=on-failure
RestartSec=42s

[Install]
WantedBy=multi-user.target

```

```
#刷新服务列表：
systemctl daemon-reload

#设置开机自启
systemctl enable frp
#关闭开机自启
systemctl disable frp

#启动服务
systemctl start frp
#停止服务
systemctl stop frp
```

 ps: 在这一步是折腾时间最长的，刚开始不知道./frpc -c ./frcp.ini不能后台运行，一直用./frpc -c ./frcp.ini &代替，结果ssh死活登不上去，后来知道了，又继续折腾加入服务这事，每个教程都看了，也都试了，不知道哪个教程最后成功了，最后的frpc.service就长这样了。有时间还得研究一下每行代表的嘛意思。这第一步，用到的linux命令可太多了，端口查看lsos -i，进程查看ps-aux，主要是frpc服务的错误可太多了。也是免费小鸡的性能太低，让我好等啊。

# 4. nginx安装与配置

主要是配置nginx.conf文件，其中有两个坑：

1.配置文件修改后，打开ip地址显示的还是welcome to nginx，看吐了，后来终于找到原因了，需要注释掉http中include所在的行，不让其他配置文件生效。

```
#include /etc/nginx/conf.d/*.conf;
#include /etc/nginx/sites-enabled/*;

```

主要是这两个文件

2.终于不是welcome to tianjin了，直接不能访问了，到处google，终于找到原因，还是因为没有ipv4地址，需要让nginx监听ipv6

```
listen      [::]:80;
```



# 5. Travis CI 自动部署

## 5.1 配置travis

使用github登录travis，travis分两个网站[](travis.org)，可免费部署github上的开源repo]，[](travis.com)，收费，可也免费部署，单但有次数限制。

选择源码仓库

## 5.2 加密ssh密钥

### 本地安装travis

安装ruby，这里选择的是编译安装，其他安装方式参考(http://www.ruby-lang.org/en/documentation/installation/)

```shell
cd /tmp
wget https://cache.ruby-china.com/pub/ruby/2.7/ruby-2.7.0.tar.gz
tar zxvf ruby-2.7.0.tar.gz
cd ruby-2.7.0
./configure 
make
sudo make install
ruby -v
```

安装ruby gems，参考(https://rubygems.org/pages/download)

```shell
cd /tmp
wget https://rubygems.org/rubygems/rubygems-3.1.4.zip
unzip rubygems-3.1.4.zip
cd rubygems-3.1.4
ruby setup.rb
gem -v
```

安装travis

```shell
sudo gem install travis
```

如果由于网络原因无发现下载的话，可以更换国内的源，具体可以 [参考这里](https://gems.ruby-china.com/)

```shell
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
```

### 登录

```shell
#登录travis.org
travis login --org
#登录travis.com		
travis login --pro
```

### 生成并加密密钥

```shell
# 在当前目录生成密钥
ssh-keygen -t rsa -b 4096 -C 'build@travis-ci.org' -f ./deploy_rsa
# 使用Travis加密
travis encrypt-file deploy_rsa --add
# 添加信任关系
ssh-copy-id -i deploy_rsa.pub <ssh-user>@<deploy-host>
# 删除敏感文件
rm -f deploy_rsa deploy_rsa.pub
# 将修改添加到git中
git add deploy_rsa.enc .travis.yml
```

## 5.3 配置.travis.yml

解密密钥部分

```json
before_deploy:
- openssl aes-256-cbc -K $encrypted_137f45644142_key -iv $encrypted_137f45644142_iv
  -in deploy_rsa.enc -out /tmp/deploy_rsa -d
- eval "$(ssh-agent -s)"
- chmod 600 /tmp/deploy_rsa
- ssh-add /tmp/deploy_rsa
```

需要添加我们部署机器的host信息，以让Travis可以正常访问服务器

```json
addons:
  ssh_known_hosts: ip地址
```

### 配置_config.yml

```
deploy:
- type: git
  #repository: https://github.com/vuhks/vuhks.github.io.git
  repo: 
    github: git@github.com:vuhks/vuhks.github.io.git 
    git: hexo@主机名:/home/hexo/blog.git
  branch: master 
```

## 最后配置文件

```json
language: node_js
node_js: stable
addons:
  ssh_known_hosts: ip地址
cache:
  directories:
  - node_modules
before_install:
- openssl aes-256-cbc -K $encrypted_db2095f63ba3_key -iv $encrypted_db2095f63ba3_iv
  -in deploy_rsa.enc -out /tmp/deploy_rsa -d
- eval "$(ssh-agent -s)"
- chmod 600 /tmp/deploy_rsa
- ssh-add /tmp/deploy_rsa
install:
  - yarn add global hexo
  - yarn add global hexo-cli
  - yarn add global hexo-deployer-git

script:
- hexo cl
- hexo g
after_success:
- hexo deploy
branches:
  only:
  - master

```

ps：遇到的几个错误，主要是travis encrypt-file deploy_rsa --add这一步错误，显示加入--r命令，travis encrypt-file ---r vuhks/vuhks_source.git deploy_rsa --add，还是报错，然后到travis官网看这一步的介绍，发现是git repo的问题，问题是本地没有git项目，于是git clone了vuhks_source.git ,然后配置git账户，再登录，加密，结果就没错了。

如果卡在加密那无法生成，关闭终端试一下。

# 结语

部署hexo到vps ipv6only的过程中，虽然每一步都有好多的教程，但还是遇到了无数的错误，还有一些独一无二的错误，有些错误是前置步骤的没有一致执行的错误，有些错误是没有ipv4的原因导致的，最后一一解决后发现，只要根据教程一步一步来，最终是会成功的。致谢网上所有的教程。

参考文献（不全，有教程不知道参考的哪些了）

[【DNS64/代理】IPv6 ONLY VPS访问IPv4资源](https://luotianyi.vc/2701.html)

[使用Travis-ci自动SSH部署代码](https://www.zhuwenlong.com/blog/article/5c24b6f2895e3a0fb4072a5c)