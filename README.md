## 教程

## 第一步
去 [官网](https://golang.google.cn/dl/) 找到现成的 go 安装包 [链接](https://golang.google.cn/dl/go1.16.7.linux-amd64.tar.gz) ，以 linux amd64 位为例。
![telegram-cloud-photo-size-5-6105087589842267495-y](https://user-images.githubusercontent.com/85423779/130250420-26915bed-c705-4113-8a24-431656f07191.jpg)


第二步
```bash
cd /usr/local && wget https://golang.google.cn/dl/go1.16.7.linux-amd64.tar.gz -O go1.16.7.linux-amd64.tar.gz
```
![telegram-cloud-photo-size-5-6105087589842267497-y](https://user-images.githubusercontent.com/85423779/130250401-2668e075-31bd-4581-81c7-1c4d150f6e9f.jpg)


## 第三步
解压
```bash
tar -xvzf go1.16.7.linux-amd64.tar.gz
```
![telegram-cloud-photo-size-5-6105087589842267498-y](https://user-images.githubusercontent.com/85423779/130250361-2d3a56de-6769-47cf-b25e-a41038cf7794.jpg)


## 第四步
设置环境变量 vi /etc/profile ,将红框内文本复制到最后一行。 

```bash
export GO111MODULE=on
export GOPROXY=https://goproxy.cn
export GOROOT=/usr/local/go
export GOPATH=/usr/local/go/path
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```
![telegram-cloud-photo-size-5-6105087589842267499-y](https://user-images.githubusercontent.com/85423779/130249981-57cc9867-acc1-433d-945c-31481416e77c.jpg)

esc :wq 保存文件后 source /etc/profile

输入 
```bash
go env 
```
![telegram-cloud-photo-size-5-6105087589842267501-y](https://user-images.githubusercontent.com/85423779/130249887-5a471d01-a73f-46e8-aead-8e4a02ed2877.jpg)

输出如此代表go安装好了。

## 第六步
编译 xdd
```bash
cd jd_study/xdd && go build
```

## 第七步
配置好config。yaml 运行xdd
```bash
./xdd
```
