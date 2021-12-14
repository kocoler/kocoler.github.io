---
title: Go入门须知
date: 2020-11-15 12:37:00
---


> GOLANG, GOPATH, GOROOT ......

### 预备知识

后面可能会用到，用到的时候再回来看

- [环境变量](https://en.wikipedia.org/wiki/Environment_variable)（Environment Variable）

  环境变量相当于给系统或用户应用程序设置的一些参数

  作用于这个系统层面的，不拘束于某些应用程序等等

  就比如我开机什么都不干Go就知道自己是装好的，知道哪里是GOPATH，大家都可以读取

  如何写入？

  ```bash
  vim ~/.bashrc
  // export xxx=xxx ...
  // export 的意思就是将局部变量设置为环境变量
  source ~/.bashrc
  
  // 检查是否成功
  echo $xxx
  // echo 打印
  ```

  在别的教程看到的不同的文件（~/.profile, /etc/profile ......）有什么区别？

  [如何选择放哪里](https://superuser.com/questions/789448/choosing-between-bashrc-profile-bash-profile-etc)

  [区别](https://superuser.com/questions/183870/difference-between-bashrc-and-bash-profile)

- PATH

  `PATH`: a list of directory paths. When the user types a command without providing the full path, this list is checked to see whether it contains a path that leads to the command.

  简单来说，就是命令行去哪里找的问题

  就像Go package要去GOPATH里找一样

- [绝对路径/相对路径](https://www.linuxnix.com/abslute-path-vs-relative-path-in-linuxunix/)

  绝对路径即/目录开始的一条完整路径。（绝对路径是唯一的）

  相对路径即当前目录开始的

- 一些命令行

  ```bash
  $ ls // 当前目录下的所有文件
  $ go
  $ gofmt xxx // Go 的小工具，用来格式化代码风格、规范
  $ go env
  $ go run
  $ go build
  $ which // 定位命令行文件位置
  
  // 带参数的
  $ go env -w // 设置Go环境变量
  $ go run -n // 打印编译期间所用到的其它命令，但是并不真正执行它们
  ```

  

----------



## Go 官网

[Golang官网](https://golang.org/) 是个需要翻墙才可以look的地方，不过问题不大

内含：

- Go 各版本的[**安装**](https://golang.org/doc/install)

- [Go Blog](https://blog.golang.org/)

   可以获得一些官方的建议，最新的发展......

- [**Go 官方文档**](https://golang.org/doc/)

  东西蛮多的，从Go的安装~~到卸载~~到各个阶段的教程都有了

  最主要的是官方的

  比较推荐其中的**[Effective go](https://golang.org/doc/effective_go.html)**，算是书写Go语言的规范，建议熟练运用Go之后学习
  
- [在线playground](https://play.golang.org/)

- [更多关于go](https://golang.org/project/)

### Geting started

![image-20201113163139849](https://s3.ax1x.com/2020/11/15/DP7kNj.png)

```bash
$ vim 1.go // vim 1.c

// coding......

$ go build 1.go // gcc 1.c
$ ./1 // ./a.out

// 或者

$ go run 1.go // 目前推荐这种方式
$ go install 1.go // 这个好玩

// end
```

## Golang

> 无论看哪本入门书籍，他们都会告诉你，Go很棒（当然所有语言的入门书籍都会这么说2333

- Something about Go

  **Less is more.**

  C++功能太多了，Go作者也是C++程序员

  讲个小故事

  ```
  谷歌大佬从事c++开发（分布式），某一天听说c++又要加新功能，内心疯狂吐槽后找了另外几个大佬，并表明觉得简化c++更棒
  大佬们一拍即合，他们决定开发一门新语言
  经过漫长岁月的发展，Go诞生了
  ```

  **基本的核心特性**

  - 简洁，开发效率高
  - 内存管理

  - **并发编程**，适合高并发
  - 静态编译、强类型......
  - 混合编程（cgo......）

- Golang is like C

  看哪本书估计也都会提起Go是类C语言

  在学习的时候可能会看到很多和C相似

  这种（类C）语言通常是为某种具体的应用而仿照C语言（语法类似）开发的，所以学过C之后学Go会很快，~~学过Cpp之后学Go会更快2333~~。

- A list of significant simplifications（重要的简化）

  没有头文件

  没有指针运算（no pointer arithmetic）

  自建类型字符串，切片，哈希表（builtin string, slice, map）

  内存0值初始化（memory is always zeroed）

  多返回值

  无循环依赖

  数组越界检查

  ......

- [more](https://commandcenter.blogspot.com/2012/06/less-is-exponentially-more.html)

#### GOENV

![image-20201113143044644](https://s3.ax1x.com/2020/11/15/DP7aDO.png)

都是`绝对路径`。

GO111MODULE：go mod，1.11版本后支持

GOARCH：环境架构

**GOBIN**

GOCACHE：缓存（go build）

GOHOSTOS：目标操作系统

GOPROXY：go代理

**GOPATH**

**GOROOT**

GOENV：Go环境配置，vim进去就可以看，一般通过 `go env -w xxx=xxx` 命令行设置的变量都存在里面，不用每次都切环境变量，不过优先度应该是在环境变量下~~虽然我这台电脑就出现了奇奇怪怪的问题~~。

```bash
$ go version
go version go1.14.10 darwin/amd64
```

[more](https://golang.org/cmd/go/#hdr-Environment_variables)

### GOROOT

#### 概念：GOROOT就是GO的安装目录

大家写这么久C，但是C都有什么应该还很模糊，但我们可以简单的看看Go都有什么

GOROOT里有什么：

![image-20201113100054532](https://s3.ax1x.com/2020/11/15/DP7tv6.png)

- api

  罗列了个版本Go api特性啥的，无所谓无所谓

- **bin**

  由go官方提供的一些工具的可执行文件

  一般来说：自带的有go, gofmt

  ```bash
  $ which go
  /usr/local/go/bin/go
  ```

- doc

  文档

  示例程序，代码工具，本地文档等

- version

  版本号（顺便一提自己改是没有用的233）

- pkg

  存放编译后的包文件

- **src**

  标准库函数

- favicon.ico

  地鼠！

### GOBIN

#### 概念：可执行文件目录

主要和 go install 相关，放各种go工具的地方

```bash
$ go install goexample

$ goexample
```

### GOPATH

GOPATH为 Go 语言的工作区的**集合（意味着可以有很多个）**。工作区类似于工作目录。每个不同的目录之间用`：`分隔。

Go 1.11 版本之后引入 Go module，削弱GOPATH的约束

引自宋汝阳的良好的GOPATH结构（为了避免争议，暂且划分在启用go mod以前）：

![image-20201113144030923](https://s3.ax1x.com/2020/11/15/DP7Ygx.png)

> 这个是不是和GOROOT里很像？每个目录代表意思都差不多
>
> 那为什么我们要这么安排？

GO Package 的引入规则

一般都是找两个地方：

`$GOPATH/src/...` (from $GOPATH)

`$GOROOT/src/...`  (from $GOROOT)

### Go Package

我们之前在C语言中可能用到过的，`string.h`, `stdlib.h` 这些叫做库函数，在官方库函数之外还有各种各样的 包。

Go 程序是通过 package 来组织的。

例如：package 这一行告诉我们当前文件属于哪个包，而包名 main 则告诉我们它是一个可独立运行的包，它在编译后会产生可执行文件。

> 任何包系统设计的目的都是为了简化大型程序的设计和维护工作，通过将一组相关的特性放进一个独立的单元以便于理解和更新，在每个单元更新的同时保持和程序中其它单元的相对**独立性**。这种**模块化**的特性允许每个包可以被其它的不同项目共享和重用，在项目范围内、甚至全球范围统一的分发和复用。
>
> 每个包一般都定义了一个**不同的名字空间**用于它内部的每个标识符的访问。每个名字空间关联到一个特定的包，让我们给类型、函数等选择简短明了的名字，这样可以避免在我们使用它们的时候减少和其它部分名字的冲突。
>
> 每个包还通过控制包内名字的可见性和是否导出来实现封装特性。通过限制包成员的可见性并隐藏包API的具体实现，将允许包的维护者在不影响外部包用户的前提下调整包的内部实现。通过限制包内变量的可见性，还可以强制用户通过某些特定函数来访问和更新内部变量，这样可以保证内部变量的一致性和并发时的互斥约束。
>
> ......

#### GO 官方包（标准库函数）

> $GOROOT/src

学习他：[在线的，镜像的，官方的，被翻译过的](https://studygolang.com/pkgdoc)

#### GO 文件

GO 语言的源码文件主要分为几类：

- **命令源码文件**

  命令源码文件总是作为可执行的程序的入口。

  声明自己属于 main 代码包、 main 函数。

  多个命令源码文件虽然可以分开单独 go run 运行起来，但是无法通过 go build 和 go install。

  **main.go**

- **库源码文件**

  库源码文件一般用于集中放置各种待被使用的程序实体（全局常量、全局变量、接口、结构体、函数等等）。

- **测试源码文件**

  测试源码文件主要用于对前两种源码文件中的程序实体的功能和性能进行测试。

#### 一个包是如何组成、使用的

> 包是函数和数据的集合。
>
> 我们将会大量的用到各种包，各种途径的。

- 含有Go文件的目录......有可见性的东西（type, function）基本就能当作一个包使用了

- 用 package 关键字定义一个包。文件名不需要与包名一致，但是你的文件夹必须要与包名字一致，这个很重要，所以为了简单起见，名字都是一样的。

  如果你定义好了这个包，那么就可以在外部引用他了

- 食用方法：

  ```go
  /*                                                    */
  /*    $GOPATH/src/github.com/kocoler/share/main.go    */
  /*                                                    */
  
  package main
  
  import (
    "fmt"
    . "log" // 不推荐
    
  	_ "github.com/jinzhu/gorm/dialects/mysql"
    
    "github.com/kocoler/share/example"
  )
  
  func main() {
    fmt.Println("Muxi") // fmt.Println()
    Println("Log Println") // log.Println()
  }
  
  ------
  
  /*                                                               */
  /*    $GOPATH/src/github.com/kocoler/share/example/example.go    */
  /*                                                               */
  
  package example
  
  import "fmt"
  
  int A = 0；
  
  func init() {
    fmt.Println("I'm initialzing")
  }
  
  func PrintA() {
    fmt.Println("example.PrintA() executed")  
  }
  ```

- 如何找到你想用的包

  1. 谷歌
  2. Github
  3. [Go dev](https://pkg.go.dev/) 最近Go官方也很推这个

- 放到GOPATH中

  ```bash
  // 比较笨拙的方法...
  $ cd $GOPATH/src/github.com
  $ mkdir go-gorm
  $ cd go-gorm
  $ git clone github.com/go-gorm/gorm
  
  // 或者
  $ go get -t https://github.com/go-gorm/gorm
  
  // 或者 go module, 交给后面的人讲了
  // 各有各的好处，不用纠结，直接auto，项目go mod，学习就off
  ```

- 如何快速的上手/学会用一个包

  1. 谷歌

  2. Readme, go dev ......

     Readme 重点关注quickly start
  
- 不知道包引入路径？

  ```bash
  $ go list
  github.com/kocoler/share/example
  
  $ go list log
  log
  ```

---------

### 执行 Example 经历的一小小部分

> 如果有时间就小小说一下.....
>
> 无复杂东西
>
> 挺神奇的
>
> 加深理解233

如果你记忆力好一点的话，可能知道C语言的编译过程，当然这无所谓

// 括号里是生成的

C/C++：预处理(.i)、编译(.s)、汇编(.o)、链接(.out)

Go：编译(.a)、链接(.out)

> .a文件是什么？
>
> 在Go中我们称.a文件为归档文件（也就是静态文件），简单来说就是放在pkg文件夹里编译好的包

```bash
$  go run -n main.go
#
# command-line-arguments
#

mkdir -p $WORK/b001/  # 创建临时目录

cat >$WORK/b001/importcfg << 'EOF' # internal 查找依赖信息
# import config
packagefile fmt=/usr/local/go/pkg/darwin_amd64/fmt.a
packagefile github.com/jinzhu/gorm/dialects/mysql=/Users/mac/go/pkg/darwin_amd64/github.com/jinzhu/gorm/dialects/mysql.a
packagefile github.com/kocoler/share/example=/Users/mac/Library/Caches/go-build/fc/fc6b2deb1c0f91857e094ad17bbcd48cf4b2b84bf405710663a83dde72aeb6ad-d
packagefile log=/usr/local/go/pkg/darwin_amd64/log.a
packagefile runtime=/usr/local/go/pkg/darwin_amd64/runtime.a
EOF

cd /Users/mac/go/src/github.com/kocoler/share # 执行源代码编译
/usr/local/go/pkg/tool/darwin_amd64/compile -o $WORK/b001/_pkg_.a -trimpath "$WORK/b001=>" -p main -complete -buildid YWEJgSlrVcwt0-zEHmU8/YWEJgSlrVcwt0-zEHmU8 -dwarf=false -goversion go1.14.10 -D _/Users/mac/go/src/github.com/kocoler/share -importcfg $WORK/b001/importcfg -pack -c=4 ./main.go
/usr/local/go/pkg/tool/darwin_amd64/buildid -w $WORK/b001/_pkg_.a # internal

cat >$WORK/b001/importcfg.link << 'EOF' # internal 收集链接库文件
packagefile command-line-arguments=$WORK/b001/_pkg_.a
packagefile fmt=/usr/local/go/pkg/darwin_amd64/fmt.a
packagefile github.com/jinzhu/gorm/dialects/mysql=/Users/mac/go/pkg/darwin_amd64/github.com/jinzhu/gorm/dialects/mysql.a
packagefile github.com/kocoler/share/example=/Users/mac/Library/Caches/go-build/fc/fc6b2deb1c0f91857e094ad17bbcd48cf4b2b84bf405710663a83dde72aeb6ad-d
packagefile log=/usr/local/go/pkg/darwin_amd64/log.a
......
packagefile vendor/golang.org/x/sys/cpu=/usr/local/go/pkg/darwin_amd64/vendor/golang.org/x/sys/cpu.a
EOF

mkdir -p $WORK/b001/exe/
cd .
# 链接生成可执行文件
/usr/local/go/pkg/tool/darwin_amd64/link -o $WORK/b001/exe/main -importcfg $WORK/b001/importcfg.link -s -w -buildmode=exe -buildid=2g1FvKbI5O8czokn17YO/YWEJgSlrVcwt0-zEHmU8/YWEJgSlrVcwt0-zEHmU8/2g1FvKbI5O8czokn17YO -extld=clang $WORK/b001/_pkg_.a
$WORK/b001/exe/main
```



​	......





---------

一些讨论

>https://github.com/golang/go/issues/23439
>
>https://stackoverflow.com/questions/25216765/gobin-not-set-cannot-run-go-install
>
>......
