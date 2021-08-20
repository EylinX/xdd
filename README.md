教程
第一步，去 官网（https://golang.google.cn/dl/） 找到现成的 go 安装包 链接（https://golang.google.cn/dl/go1.16.7.linux-amd64.tar.gz） ，以 linux amd64 位为例。
第二步， cd /usr/local && wget https://golang.google.cn/dl/go1.16.7.linux-amd64.tar.gz -O go1.16.7.linux-amd64.tar.gz
第三步，解压 tar -xvzf go1.16.7.linux-amd64.tar.gz
第四步，设置环境变量 vi /etc/profile ,将红框内文本复制到最后一行。 

export GO111MODULE=on
export GOPROXY=https://goproxy.cn
export GOROOT=/usr/local/go
export GOPATH=/usr/local/go/path
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin

esc :wq 保存文件后 source /etc/profile

输入 go env ,输出如此代表go安装好了。

第六步，编译 cd jd_study/xdd && go build

第七步，运行 ./xdd
