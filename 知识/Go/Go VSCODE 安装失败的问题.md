vscode 安装go插件

用vscode新建一个go文件
使用go mod 代理来安装


从https://studygolang.com/dl下载go1.14.6.windows-amd64.msi安装即可，安装路径选择默认，安装完成后会自动帮你配置环境变量不用自己配置了
打开cmd，查看是否安装完成

这样就代表已经成功安装了
用vscode新建一个go文件

vscode会提示你安装go插件
点击install all
这时候会安装失败
Installing github.com/mdempsky/gocode FAILED
Installing github.com/uudashr/gopkgs/v2/cmd/gopkgs FAILED
Installing github.com/ramya-rao-a/go-outline FAILED
Installing github.com/acroca/go-symbols FAILED
Installing golang.org/x/tools/cmd/guru FAILED
Installing golang.org/x/tools/cmd/gorename FAILED
Installing github.com/cweill/gotests/… FAILED
Installing github.com/fatih/gomodifytags FAILED
Installing github.com/josharian/impl FAILED
Installing github.com/davidrjenni/reftools/cmd/fillstruct FAILED
Installing github.com/haya14busa/goplay/cmd/goplay FAILED
Installing github.com/godoctor/godoctor FAILED
Installing github.com/go-delve/delve/cmd/dlv FAILED
Installing github.com/stamblerre/gocode FAILED
Installing github.com/rogpeppe/godef FAILED
Installing github.com/sqs/goreturns FAILED
Installing golang.org/x/lint/golint FAILED
原因你懂的

使用go mod 代理来安装
https://goproxy.io是一个国内的代理
执行
```
# 旧版，已废弃 go env -w GO111MODULE=on 
go env -w GOPROXY=https://goproxy.io,direct


# 新版改成如下链接 
go env -w GO111MODULE=on 
go env -w GOPROXY=https://proxy.golang.com.cn,direct
```


开启go mod 代理后也可以手动安装

go get -u -v github.com/mdempsky/gocode
go get -u -v github.com/uudashr/gopkgs/v2/cmd/gopkgs
go get -u -v github.com/ramya-rao-a/go-outline
go get -u -v github.com/acroca/go-symbols
go get -u -v golang.org/x/tools/cmd/guru
go get -u -v golang.org/x/tools/cmd/gorename
go get -u -v github.com/cweill/gotests/...
go get -u -v github.com/fatih/gomodifytags
go get -u -v github.com/josharian/impl
go get -u -v github.com/davidrjenni/reftools/cmd/fillstruct
go get -u -v github.com/haya14busa/goplay/cmd/goplay
go get -u -v github.com/godoctor/godoctor
go get -u -v github.com/go-delve/delve/cmd/dlv
go get -u -v github.com/stamblerre/gocode
go get -u -v github.com/rogpeppe/godef
go get -u -v github.com/sqs/goreturns
go get -u -v golang.org/x/lint/golint

