## 声明本程序是搬运[cdle](https://github.com/cdle/xdd)大佬，源码归原作者所有

## 菜鸟教程

## 第一步
去 [官网](https://golang.google.cn/dl/) 找到现成的 go 安装包 [链接](https://golang.google.cn/dl/go1.16.7.linux-amd64.tar.gz) ，以 linux amd64 位为例。
![telegram-cloud-photo-size-5-6105087589842267495-y](https://user-images.githubusercontent.com/85423779/130250420-26915bed-c705-4113-8a24-431656f07191.jpg)

## 第二步
拉取golang压缩包
```bash
cd /usr/local && wget https://golang.google.cn/dl/go1.16.7.linux-amd64.tar.gz -O go1.16.7.linux-amd64.tar.gz
```
![telegram-cloud-photo-size-5-6105087589842267497-y](https://user-images.githubusercontent.com/85423779/130250401-2668e075-31bd-4581-81c7-1c4d150f6e9f.jpg)

解压 (如果解压命令提示无效命令，安装 tar 即可）
```bash
tar -xvzf go1.16.7.linux-amd64.tar.gz
```
![telegram-cloud-photo-size-5-6105087589842267498-y](https://user-images.githubusercontent.com/85423779/130250361-2d3a56de-6769-47cf-b25e-a41038cf7794.jpg)

## 第三步
设置环境变量 
```bash
vi /etc/profile
```
将红框内文本复制到最后一行
```bash
export GO111MODULE=on
export GOPROXY=https://goproxy.cn
export GOROOT=/usr/local/go
export GOPATH=/usr/local/go/path
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```
![telegram-cloud-photo-size-5-6105087589842267499-y](https://user-images.githubusercontent.com/85423779/130249981-57cc9867-acc1-433d-945c-31481416e77c.jpg)

esc :wq 保存文件后输入：
```bash
source /etc/profile
```

再输入： 
```bash
go env 
```
![telegram-cloud-photo-size-5-6105087589842267501-y](https://user-images.githubusercontent.com/85423779/130249887-5a471d01-a73f-46e8-aead-8e4a02ed2877.jpg)

输出如此代表go安装好了。

## 第四步
安装gcc
```bash
## ubuntu 命令
apt-get install gcc -y
## centos/debian 命令
yum install gcc -y
```
安装git
```bash
## ubuntu 命令
apt-get install git -y
## centos/debian 命令
yum install git -y
```

## 第五步
拉取源码（cd到想安装的目录再运行命令）

```bash
cd /etc && git clone https://github.com/EylinX/xdd.git
```
编译 xdd
```bash
cd xdd && go build
```

## 第六步
先[配置文件](https://github.com/EylinX/xdd/blob/main/README.md#配置教程) 后输入：
```bash
./xdd
```
扫码成功后 Ctrl+c 退出，再输入： 
```bash
./xdd -d
```
或
```bash
nohup ./xdd >/dev/null 2>&1 &
```
或
通过systemd添加[开机自启](https://github.com/EylinX/xdd/blob/main/README.md#开机自启)


# 配置教程

修改端口
```bash
vim /etc/xdd/conf/app.conf
```
修改config配置文件【重要】
```bash
vim /etc/xdd/conf/config.yaml
```
输入 i 进入编辑模式 将下面代码文本复制进去 按需修改
```bash
mode: parallel #模式 balance(均衡模式)、parallel(平行模式)
containers: #容器，可配置多个
  - address: http://192.168.2.6:5700 #青龙2.2、青龙2.8、v1v2v3v4v5访问地址
    username: admin #用户名
    password: admin123 #密码
#    weigth:  #权重 balance模式下权重越高分得的ck越多，默认1 单容器禁用
#    mode: parallel #单独对容器进行模式设置 单容器禁用
#    limit: 1 #限制容器ck数目 单容器禁用
  - address: http://192.168.2.5:5700 #第二个青龙2.2、青龙2.8、v1v2v3v4v5访问地址
    username: admin
    password: admin123
theme:  #自定义主题，支持本地、网络路径
static: ./static #静态文件 便于自定义二维码页面时，引入css、js等文件
master:  #管理员账户pin，有多个用'&'拼接
database:  #数据库位置，默认./.xdd.db
qywx_key:  #企业微信推送key
daily_push: #定时任务
resident: #均衡模式下所有容器共同的账号pin，有多个用'&'拼接。不建议填写，后续实现指定账号助力功能。
#自定义ua
user_agent:
telegram_bot_token:  #telegram bot token
telegram_user_id:  #telegrame user id
qquid: 283371717 #接收通知的qq号
qqgid: 727438347 #监听的群
default_priority:  #新用户默认优先级，默认：1
no_ghproxy: true #更新资源是否不使用代理 默认false
qbot_public_mode: true  #qq机器人群聊模式，默认私聊模式
daily_asset_push_cron: 0 9 * * * #日常资产推送时间
repos:
  - git: https://github.com/EylinX/faker2.git #脚本库
```
自定义回复配置编辑
```bash   
vim /etc/xdd/conf/reply.php
```

# 开机自启
增加systemd服务
```bash
vim /lib/systemd/system/xdd.service
```
输入 i 进入编辑模式 将下面代码文本复制进去
```bash
[Unit]
Description=xdd
After=network.target

[Service]
#Type=forking
WorkingDirectory=/etc/xdd
ExecStart=/usr/bin/nohup /etc/xdd/xdd >/dev/null 2>&1 &
ExecStop=/usr/bin/kill -9 $MAINPID
Environment=HOME=/etc/xdd PWD=/etc/xdd
StandardOutput=null

[Install]
WantedBy=multi-user.target
```
esc :wq 保存文件后输入：
```bash
systemctl daemon-reload
```
启动该服务，在系统 boot 时激活
```bash
systemctl enable xdd
```
启动服务
```bash
systemctl start xdd
```
停止服务
```bash
systemctl stop xdd
````
重启服务
```bash
systemctl restart xdd
```
使用该命令查看服务的 log 信息
```bash
journalctl -u xdd
```
查看是否后台运行,显示有运行脚本到 PID 即代表成功后台运行
```bash
ps -def | grep xdd
```
如需停止运行，找到 PID 后，就可以使用 kill PID 来停止运行
```bash
kill -9 进程号PID
```
##################好好学习#############天天向上####################
