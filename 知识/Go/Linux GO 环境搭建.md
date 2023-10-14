

>使用二进制文件

有了gvm之后就不推荐使用了




>使用GVM进行搭建

下载

最好使用二进制安装，如果使用源码安装会遇到报错，导致失败
```
加上  -B选项
```

在使用vscode 建立环境的时候，除了需要修改代理之外，还需要重启一下电脑，之后的包才会自动安装，

```
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct

```


```
GVM下载
一条命令，随便搜索，就能找到
```

```
GVM  环境变量设置

打开.bashrc, 添加

export GO_BINARY_BASE_URL=https://golang.google.cn/dl/
[[ -s "$HOME/.gvm/scripts/gvm" ]] && source "$HOME/.gvm/scripts/gvm"
export GOROOT_BOOTSTRAP=$GOROOT

```



#go坑 在使用 go get 获取第三方依赖的时候， 会出现"zip: not a valid zip file" 的错误
方案：
```
首先 清楚缓存
go clean -modcache

设置代理
export GOPROXY=https://goproxy.cn  

再次  get
```