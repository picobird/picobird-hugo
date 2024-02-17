+++
date = "2016-02-22T21:04:55+08:00"
title = "install go tools (Golang 1.6)"
tags = ["golang"]

+++

### 免翻墙安装Go tools (Golang 1.6)  

`branch="release-branch.go1.6"`  
`mkdir -p $GOPATH/src/golang.org/x`  

`git clone -b $branch https://github.com/golang/tools.git $GOPATH/src/golang.org/x/tools`  
`git clone https://github.com/golang/net.git $GOPATH/src/golang.org/x/net`  

`cd $GOPATH`  
`go install golang.org/x/tools/cmd/goimports`  
`go install golang.org/x/tools/cmd/vet`  
`go install golang.org/x/tools/cmd/oracle`  
`go install golang.org/x/tools/cmd/godoc`  
 
[参考内容crazygit@github](https://gist.github.com/crazygit/79641e92e474ec151d07)
