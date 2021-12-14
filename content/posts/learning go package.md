---
title: Golang 官方标准库学习
date:  2019-12-07 23:49:49
draft: false
description: Go源码中带有的所有官方标准库，基于 1.10 版本的 Go 源码。
---

本文主要介绍Go源码中带有的所有官方标准库，很基本
内容还比较少，有机会会继续更新

#### 什么是golang官方标准库

1. 这些包一般储存在GOROOT路径下的src文件夹中，并且是以.go为后缀名的（有可能你会在pkg/中找到一些.a后缀的文件 [拓展.a](https://www.solvusoft.com/zh-cn/file-extensions/file-extension-a)
例如用apt-get安装后在ubuntu下的路径：

    > /usr/lib/go-1.10/src

2. 如何简便的学习/观察这些库
    [Go语言中文网](https://studygolang.com/pkgdoc)
[官方英文](https://golang.google.cn/pkg/)
（当然本地观看的办法也很多）

#### 进入本体
1. **net** 

从我们比较熟悉的网络包入手
这个包主要是与网络相关，算是Go标准库中比较大型（也比较常用的）包
主要包含了一些底层的协议实现
net包提供的函数和类型可用于使用Unix域以及网络socket通信、TCP/IP和UDP编程。
**[net/http](https://studygolang.com/static/pkgdoc/pkg/net_http.htm)**
http主要包提供了HTTP客户端和服务端的实现。
包括创建服务器，路由
http目录下其他的子库：
**[net/http/cgi](https://studygolang.com/static/pkgdoc/pkg/net_http_cgi.htm)
[net/http/cookiejar](https://studygolang.com/static/pkgdoc/pkg/net_http_cookiejar.htm)
[net/http/fcgi](https://studygolang.com/static/pkgdoc/pkg/net_http_fcgi.htm)
[net/http/httptest](https://studygolang.com/static/pkgdoc/pkg/net_http_httptest.htm)
[net/http/httptrace](https://studygolang.com/static/pkgdoc/pkg/net_http_httptrace.htm)
[net/http/httputil](https://studygolang.com/static/pkgdoc/pkg/net_http_httputil.htm)
[net/http/pprof](https://studygolang.com/static/pkgdoc/pkg/net_http_pprof.htm)**

**[net/url](https://studygolang.com/static/pkgdoc/pkg/net_url.htm)**
主要与解析/处理URL有关，比如url字符串解析、编码
net目录下其他子库：
**[net/mail](https://studygolang.com/static/pkgdoc/pkg/net_mail.htm)
[net/rpc](https://studygolang.com/static/pkgdoc/pkg/net_rpc.htm)
[net/rpc/jsonrpc](https://studygolang.com/static/pkgdoc/pkg/net_rpc_jsonrpc.htm)
[net/smtp](https://studygolang.com/static/pkgdoc/pkg/net_smtp.htm)
[net/textproto](https://studygolang.com/static/pkgdoc/pkg/net_textproto.htm)**


2. **[fmt](https://studygolang.com/static/pkgdoc/pkg/fmt.htm)**

从入门到弃坑，都会使用的fmt库
fmt库主要涉及go的格式化操作，并且主要是字符串的格式化
包含最常见的格式化输入输出到控制台，当作目标函数的参数等等（debug也比较建议用log
fmt并没有再延伸的标准库

3. **[log](https://studygolang.com/static/pkgdoc/pkg/log.htm)**

实现简易/简单的日志服务，是并发安全的
（最主要的是还带时间哈哈哈哈
调用会打印每条日志信息的日期、时间，默认输出到标准错误。
Print系列函数包括控制台的打印（使用参考fmt包
Fatal系列函数会在写入日志信息后调用os.Exit(1)
Panic系列函数会在写入日志信息后panic
适合一般情况下日志的记录，适合一般情况下对错误的处理，适合一般情况下的debug
log目录下的子库：
**[log/syslog](https://studygolang.com/static/pkgdoc/pkg/log_syslog.htm)**

4. **[sort](https://studygolang.com/static/pkgdoc/pkg/sort.htm)**

方便的排序函数，主要是排序各式各样切片类型
主流的排序算法：插入排序，堆排序，快排，归并排序都有实现
并且一次排序不一定只调用一种函数，只要实现了 sort.Interface 定义的三个方法：获取数据集合长度的 Len() 方法、比较两个元素大小的 Less() 方法和交换两个元素位置的 Swap() 方法，就可以顺利对数据集合进行排序。sort 包会根据实际数据自动选择高效的排序算法。 
当然，不做更多的要求的调用也很方便
还有search功能，可以同时支持更神奇的操作
PS1：sort包对不同类型的实现好像略有不同
PS2：sort包好像普通的排序不是稳定的，为此有特别提供稳定的stable函数
个人觉得是可以深入了解的库
没有子库

5. **[strings](https://studygolang.com/static/pkgdoc/pkg/strings.htm)**

实现用于操作字符的简单函数，即主要包含针对字符串操作的函数
为某些较复杂（麻烦）日常还会经常用到的一些需求提供方便的实现
比如：字符串分割，字符串匹配系列，字符串读取以及字符串替换/修剪等等
PS1：**Go 中字符串是不可变的**
这个包里还声明了两个跟io包关系密切的类型:Reader和Replacer
strings包没有字库

6. **[io](https://studygolang.com/static/pkgdoc/pkg/io.htm)**

~~自然~~的过渡到io包
这个包经常会根其他的包联动
~~谈到io，自然要谈到I/O~~

>同时，这里补充以下对Go中I/O的一点简述：
>*  io 为 IO 原语（I/O primitives）提供基本的接口
>*  io/ioutil 封装一些实用的 I/O 函数
>*  fmt 实现格式化 I/O，类似 C 语言中的 printf 和 scanf
>*  bufio 实现带缓冲I/O

io包中声明了两个很强大，很厉害的类型(接口）：Reader和Writer
（其实这个包声明了很多类型，都很强的
io包中提供了供日常使用的很多读写功能，对常用资源（内存，文件等等）的读写的接口实现，使得很多操作变得简便，灵活性高（包括但不限函数间）
PS1: 由于这些被接口包装的I/O原语是由不同的低级操作实现，因此，在另有声明之前不该假定它们的并行执行是安全的。
**[io/ioutil](https://studygolang.com/static/pkgdoc/pkg/io_ioutil.htm)**
这个包很实用，很实用，很方便，很方便
常用函数：

    func ReadAll(r io.Reader)([]byte,error）
    func ReadFile(filename string)([]byte,error)
    func WriteFile(filename string,data []byte,perm os.FileMode) error

7. **[bytes](https://studygolang.com/static/pkgdoc/pkg/bytes.htm)**
这个包主要是和Go中的[]byte类型的处理有关
string,bytes 联系蛮紧密的
因此，bytes包中有很多和strings相仿的函数，一定程度上可以参考string包学习（但其实大概没这个必要
还有两个类型Reader和**Buffer**
Buffer本身是一个缓存，没有底层数据，缓存的容量会根据需要自动调整

8. **[errors](https://studygolang.com/static/pkgdoc/pkg/errors.htm)**
非常短
包含了实现创建错误值的函数（不过常见的error类型并不是在这里声明的！
只是包含了对错误的简单处理，相对的，个性化处理变得简单
很短，目录下没有子库

9. **[encoding](https://studygolang.com/static/pkgdoc/pkg/encoding.htm)**
>encoding包定义了供其它包使用的可以将数据在字节水平和文本表示之间转换的接口。encoding/gob、encoding/json、encoding/xml三个包都会检查使用这些接口。因此，只要实现了这些接口一次，就可以在多个包里使用。标准包内建类型time.Time和net.IP都实现了这些接口。接口是成对的，分别产生和还原编码后的数据。

以上是引用的官网的解释
encoding包主要是关于常用的各种数据格式的转化操作，子库包括了json,xml,csv,binary等等的转化操作
（解析和转化功能还是很强的
涉及一些和数据类型相关的知识
当然不同的类型实现方法/接收类型也很不一样
encoding目录下的子库：
[encoding/ascii85](https://studygolang.com/static/pkgdoc/pkg/encoding_ascii85.htm)
[encoding/asn1](https://studygolang.com/static/pkgdoc/pkg/encoding_asn1.htm)
[encoding/base32](https://studygolang.com/static/pkgdoc/pkg/encoding_base32.htm)
[encoding/base64](https://studygolang.com/static/pkgdoc/pkg/encoding_base64.htm)
[encoding/binary](https://studygolang.com/static/pkgdoc/pkg/encoding_binary.htm)
[encoding/csv](https://studygolang.com/static/pkgdoc/pkg/encoding_csv.htm)
[encoding/gob](https://studygolang.com/static/pkgdoc/pkg/encoding_gob.htm)
[encoding/hex](https://studygolang.com/static/pkgdoc/pkg/encoding_hex.htm)
**[encoding/json](https://studygolang.com/static/pkgdoc/pkg/encoding_json.htm)**
[encoding/pem](https://studygolang.com/static/pkgdoc/pkg/encoding_pem.htm)
[encoding/xml](https://studygolang.com/static/pkgdoc/pkg/encoding_xml.htm)

10. **[time](https://studygolang.com/static/pkgdoc/pkg/time.htm)**

time包是关于日期时间的包，提供了时间的现实和计量等等的功能，是个强大的时间接口
PS：Go中采用公历，unix timestamp 是int64
time包目录下没有子库

11. **[runtime](https://studygolang.com/static/pkgdoc/pkg/runtime.htm)**

与Go运行时相关的实现，可以通过他的某些函数来控制goroutine
涉及计算机底层的堆栈
Go的并发很强有一部分原因与runtime的强大有关
runtime目录下的子库：
[runtime/cgo](https://studygolang.com/static/pkgdoc/pkg/runtime_cgo.htm)
[runtime/debug](https://studygolang.com/static/pkgdoc/pkg/runtime_debug.htm)
[runtime/pprof](https://studygolang.com/static/pkgdoc/pkg/runtime_pprof.htm)
[runtime/race](https://studygolang.com/static/pkgdoc/pkg/runtime_race.htm)
[runtime/trace](https://studygolang.com/static/pkgdoc/pkg/runtime_trace.htm)

12. **[sync](https://studygolang.com/static/pkgdoc/pkg/sync.htm)**

谈起并发，sync包也很常用
sync包提供了基本的同步基元，但Go更推荐以channel的方式实现并发控制
常用的互斥锁：Mutex
线程控制：WaitGroup
还包含了一个Pool临时对象池
sync的原子操作包含在**[sync/atomic](https://studygolang.com/static/pkgdoc/pkg/sync_atomic.htm)**下

13. **[strconv](https://studygolang.com/static/pkgdoc/pkg/strconv.htm)(string convert)**

字符串转化
strconv提供了关于字符串与其他类型转化的功能实现方法
整型：Itoa，Atio
浮点型：ParseFloat,FormatFloat
布尔型：ParseBool,FormatBool
有append系列
有Unicode和ASCII的操作
strconv目录下没有子库

14. **[unicode](https://studygolang.com/static/pkgdoc/pkg/unicode.htm)**

与unicode编码有关的基本函数
子库可以实现unicode（rune）与utf8（byte），utf16（int16）之间的转化
**[unicode/utf16](https://studygolang.com/static/pkgdoc/pkg/unicode_utf16.htm)
[unicode/utf8](https://studygolang.com/static/pkgdoc/pkg/unicode_utf8.htm)**

15. **[regexp](https://studygolang.com/static/pkgdoc/pkg/regexp.htm)**
正则表达式可能会迟到，但绝不会缺席！
regexp实现了正则表达式搜索
编译，匹配，搜索，替换
>本包的正则表达式保证搜索复杂度为O(n)
>**很强**
>Regexp类型提供了多达16个方法，用于匹配正则表达式并获取匹配的结果。

就正则吧，没啥可介绍的，基本每个语言都会提供的包，而且还就很麻烦qwq
还没翻译的子包：**[regexp/syntax](https://studygolang.com/static/pkgdoc/pkg/regexp_syntax.htm)**

16. **[database/sql](https://studygolang.com/static/pkgdoc/pkg/database_sql.htm)**
实现了对SQL的大量操作
并且官网指出了
>使用sql包时必须注入（至少）一个数据库驱动。

例如

    _"github.com/go-sql-driver/mysql"

这条语句将提供MySQL驱动。
具体的查询执行都是通过调用驱动实现的db接口中的方法
database/sql 提供的是抽象概念，和具体数据库无关，具体的数据库实现，有驱动来做，这样可以很方便的更换数据库。
子包**[database/sql/driver](https://studygolang.com/static/pkgdoc/pkg/database_sql_driver.htm)**定义了一些接口供数据库驱动实现

17. **[os](https://studygolang.com/static/pkgdoc/pkg/os.htm)**
os包提供了操作系统函数的不依赖平台的接口。设计为Unix风格的，虽然错误处理是go风格的；失败的调用会返回错误值而非错误码。通常错误值里包含更多信息。
os包主要实现与操作系统相关的函数，并且是与平台无关的。
在 Go 中，文件描述符封装在 os.File 结构中，通过 File.Fd() 可以获得底层的文件描述符：fd。
例如：文件打开关闭，新建等等
子包：
**[os/user](https://studygolang.com/static/pkgdoc/pkg/os_user.htm)**
与系统用户相关的库，可用于获取登陆用户、所在祖等信息
**[os/signal](https://studygolang.com/static/pkgdoc/pkg/os_signal.htm)**
Unix-Like 的系统信号处理相关函数，Linux支持64中系统信号
**[os/exec](https://studygolang.com/static/pkgdoc/pkg/os_exec.htm)**
帮助我们实现了方便执行命令的能力

18. **[hash](https://studygolang.com/static/pkgdoc/pkg/hash.htm)**
hash包主要是提供了不同的hash算法
PS：md5 hash算法包含在crypto/hash中
子库主要提供了不同的循环冗余校验算法
日后加密时候会用到
一些子库：
**[hash/adler32](https://studygolang.com/static/pkgdoc/pkg/hash_adler32.htm)
[hash/crc32](https://studygolang.com/static/pkgdoc/pkg/hash_crc32.htm)
[hash/crc64](https://studygolang.com/static/pkgdoc/pkg/hash_crc64.htm)
[hash/fnv](https://studygolang.com/static/pkgdoc/pkg/hash_fnv.htm)**

19. **[html](https://studygolang.com/static/pkgdoc/pkg/html.htm)**
html包提供了用于转义和解转义HTML文本的函数
主要是提供对html文本的处理
子包template提供了对html的模板渲染
**[html/template](https://studygolang.com/static/pkgdoc/pkg/html_template.htm)**

20. **[math](https://studygolang.com/static/pkgdoc/pkg/math.htm)**
math包提供了基本的数学处理
包括数学计算，数学常量
具体实现好像是通过大量的汇编代码实现
基本有需求的时候就可以直接用
子库
**[math/cmplx](https://studygolang.com/static/pkgdoc/pkg/math_cmplx.htm)**
支持复数操作
**[math/big](https://studygolang.com/static/pkgdoc/pkg/math_big.htm)**
支持高/多精度运算
**[math/rand](https://studygolang.com/static/pkgdoc/pkg/math_rand.htm)**
**随机生成数包**这个还是很常用的（支持生成多种类型

>如果需要每次运行产生不同的序列，应使用Seed函数进行初始化。默认资源可以安全的用于多go程并发。

这里引用一条官方的提示，并作一下解释：同一个程序多次调用rand函数只会生成同一个随机数，这个点需要注意一下

21. **[crypto](https://studygolang.com/static/pkgdoc/pkg/crypto.htm)**
crypto包提供了常用的加密算法
包含了常用的加密算法实现，比如最常见的公私钥加密，散列算法，各种签名算法等等
涉及算法层面很复杂，基本都是直接拿来用
基本都是提供与加密相关的函数，实际情况下，经常会于其他字符/数字处理包联动
大量的子库对应大量的加密算法
**[crypto/aes](https://studygolang.com/static/pkgdoc/pkg/crypto_aes.htm)
[crypto/cipher](https://studygolang.com/static/pkgdoc/pkg/crypto_cipher.htm)
[crypto/des](https://studygolang.com/static/pkgdoc/pkg/crypto_des.htm)
[crypto/dsa](https://studygolang.com/static/pkgdoc/pkg/crypto_dsa.htm)
[crypto/ecdsa](https://studygolang.com/static/pkgdoc/pkg/crypto_ecdsa.htm)
[crypto/elliptic](https://studygolang.com/static/pkgdoc/pkg/crypto_elliptic.htm)
[crypto/hmac](https://studygolang.com/static/pkgdoc/pkg/crypto_hmac.htm)
[crypto/md5](https://studygolang.com/static/pkgdoc/pkg/crypto_md5.htm)
[crypto/rand](https://studygolang.com/static/pkgdoc/pkg/crypto_rand.htm)
[crypto/rc4](https://studygolang.com/static/pkgdoc/pkg/crypto_rc4.htm)
[crypto/rsa](https://studygolang.com/static/pkgdoc/pkg/crypto_rsa.htm)
[crypto/sha1](https://studygolang.com/static/pkgdoc/pkg/crypto_sha1.htm)
[crypto/sha256](https://studygolang.com/static/pkgdoc/pkg/crypto_sha256.htm)
[crypto/sha512](https://studygolang.com/static/pkgdoc/pkg/crypto_sha512.htm)
[crypto/subtle](https://studygolang.com/static/pkgdoc/pkg/crypto_subtle.htm)
[crypto/tls](https://studygolang.com/static/pkgdoc/pkg/crypto_tls.htm)
[crypto/x509](https://studygolang.com/static/pkgdoc/pkg/crypto_x509.htm)
[crypto/x509/pkix](https://studygolang.com/static/pkgdoc/pkg/crypto_x509_pkix.htm)**

22. **[syscall](https://studygolang.com/static/pkgdoc/pkg/syscall.htm)**
硬核系统层面调用
很复杂
实现应用层和操作底层的接口**不同系统之间也存在着差异**
涉及架构、汇编
没有子库

23. **[bufio](https://studygolang.com/static/pkgdoc/pkg/bufio.htm)**
>bufio包实现了有缓冲的I/O。它包装一个io.Reader或io.Writer接口对象，创建另一个也实现了该接口，且同时还提供了缓冲和一些文本I/O的帮助函数的对象。

通过io.Reader或io.Writer创建新的Reader或Writer实例
没有子库

24. **[builtin](https://studygolang.com/static/pkgdoc/pkg/builtin.htm)**
内部声明/定义了Go的内置类型、内置函数、内置变量
>builtin 包为Go的预声明标识符提供了文档。此处列出的条目其实并不在builtin包中，对它们的描述只是为了让 godoc 给该语言的特殊标识符提供文档。

 通过官网的声明来看，builtin只是个类似包含了说明文档的包，具体和Go的内部实现有关
builtin没有子包

25. **[expvar](https://studygolang.com/static/pkgdoc/pkg/expvar.htm)**
expvar提供了可以查询Go运行时的指标记录的接口
通过HTTP在/debug/vars位置以JSON格式导出了这些变量（很多）
个人认为使用范围可以比较广的一个包，但是**这个包用的人很少.......**非常少
运行时会自动注册`http://localhost:9090/debug/vars
`
(路由接口因程序而定，可以自定义
源码相对较少，没有子库

26. **[context](https://studygolang.com/static/pkgdoc/pkg/context.htm)**
Go上下文包
和Golang的并发有很大联系，可以帮助程序更好的控制并发，在不同的goroutine间实现安全的传递数据以及超时管理等
声明了重要的Context接口
主要应用在：控制goroutine的生命周期、使不同的Goroutine携带各自的value变量等
因为和并发关系很大，所以使用时要考虑的并发的知识要很全面
没有子库

27. **[flag](https://studygolang.com/static/pkgdoc/pkg/flag.htm)**
flag包用于命令行解析参数
可以很酷的帮助你实现命令行操作
例如`git commit -m`
哈哈哈
>一般可以通过这个库来实现一些基本的操作，如果需要更复杂的命令行解析方式，可以用[https://github.com/urfave/cli](https://github.com/urfave/cli) 或者 [https://github.com/spf13/cobra](https://github.com/spf13/cobra)这两个非官方标准库

flag包没有子库

28. go
go包是Go语言核心工具使用的包。
有兴趣可以直接看源码....这里就直接跳过啦
**[go/ast](https://studygolang.com/static/pkgdoc/pkg/go_ast.htm)
[go/build](https://studygolang.com/static/pkgdoc/pkg/go_build.htm)
[go/constant](https://studygolang.com/static/pkgdoc/pkg/go_constant.htm)
[go/doc](https://studygolang.com/static/pkgdoc/pkg/go_doc.htm)
[go/format](https://studygolang.com/static/pkgdoc/pkg/go_format.htm)
[go/importer](https://studygolang.com/static/pkgdoc/pkg/go_importer.htm)
[go/parser](https://studygolang.com/static/pkgdoc/pkg/go_parser.htm)
[go/printer](https://studygolang.com/static/pkgdoc/pkg/go_printer.htm)
[go/scanner](https://studygolang.com/static/pkgdoc/pkg/go_scanner.htm)
[go/token](https://studygolang.com/static/pkgdoc/pkg/go_token.htm)
[go/types](https://studygolang.com/static/pkgdoc/pkg/go_types.htm)**

29. debug
debug包是Go语言中和调试有关的包
其中dwarf子包好像是主要与UNIX有关，包含很硬核的底层操作/信息，官网有pdf，有兴趣的可以下载下来看，很神奇哈哈哈，这里也是直接跳过
**[debug/dwarf](https://studygolang.com/static/pkgdoc/pkg/debug_dwarf.htm)
[debug/elf](https://studygolang.com/static/pkgdoc/pkg/debug_elf.htm)
[debug/gosym](https://studygolang.com/static/pkgdoc/pkg/debug_gosym.htm)
[debug/macho](https://studygolang.com/static/pkgdoc/pkg/debug_macho.htm)
[debug/pe](https://studygolang.com/static/pkgdoc/pkg/debug_pe.htm)
[debug/plan9obj](https://studygolang.com/static/pkgdoc/pkg/debug_plan9obj.htm)**

30. **[path](https://studygolang.com/static/pkgdoc/pkg/path.htm)**
回归正常的Go标准库，path包实现了对路径处理（这里就是官网指的斜杠分隔的路径，即通过*/*分隔）常用与对文件路径、URL的处理
本身篇幅较短，大概是除了error包最简单易懂的了
主要就是方便的实现一系列与路径有关的操作
这个包似乎不适合Windows的磁盘路径处理（因为不同系统，路径表示方式有所不同
而他的子包**[path/filepath](https://studygolang.com/static/pkgdoc/pkg/path_filepath.htm)**实现了兼容的问题

31. **[plugin](https://studygolang.com/static/pkgdoc/pkg/plugin.htm)**
首先指出有的人有可能没有这个包...
因为这个包是Go1.8才被官方添加的包（可以通过`go version`查看当前版本然后去官网更新），目的是增加Go本身的动态库加载能力
目前只支持Linux和MacOS
>似乎使用不是那么方便，生成和使用库文件的环境有一定的要求

plugin包没有子包

32. **[reflect](https://studygolang.com/static/pkgdoc/pkg/reflect.htm)**
（这个包其实位置应该放在前面一点的
主要包含与反射相关的函数，通过反射可以实现运行时的动态创建、修改变量、进行函数方法的调用等操作
有可能常用的两个方法：reflect.ValueOf,reflect.TypeOf
reflect包没有子库

33. **[testing](https://studygolang.com/static/pkgdoc/pkg/testing.htm)**
testing包提供了Go中自动化测试的相关实现
与`go test`命令配合使用
>常用的测试方法：单元测试，基准测试，子测试
>Go推荐采用表格驱动的测试方式

子包：**[testing/iotest](https://studygolang.com/static/pkgdoc/pkg/testing_iotest.htm)
[testing/quick](https://studygolang.com/static/pkgdoc/pkg/testing_quick.htm)**

34. text
text包主要是关于文本（**不同于字符串**）分析
词法分析：**[text/scanner](https://studygolang.com/static/pkgdoc/pkg/text_scanner.htm)**
tab处理：**[text/tabwriter](https://studygolang.com/static/pkgdoc/pkg/text_tabwriter.htm)**
模板引擎：**[text/template](https://studygolang.com/static/pkgdoc/pkg/text_template.htm)
[text/template/parse](https://studygolang.com/static/pkgdoc/pkg/text_template_parse.htm)**

35. **[unsafe](https://studygolang.com/static/pkgdoc/pkg/unsafe.htm)**
unsafe包提供了一些跳过go语言类型安全限制的操作。
平时Go会限制一些可能导致程序运行出错的用法，通过unsafe可以突破Go的限制，包含不安全的操作
涉及底层编程
unsafe没有子包

36. **[image](https://studygolang.com/static/pkgdoc/pkg/image.htm)**
image实现了基本的2D图片库。
**[image/color](https://studygolang.com/static/pkgdoc/pkg/image_color.htm)
[image/color/palette](https://studygolang.com/static/pkgdoc/pkg/image_color_palette.htm)
[image/draw](https://studygolang.com/static/pkgdoc/pkg/image_draw.htm)
[image/gif](https://studygolang.com/static/pkgdoc/pkg/image_gif.htm)
[image/jpeg](https://studygolang.com/static/pkgdoc/pkg/image_jpeg.htm)
[image/png](https://studygolang.com/static/pkgdoc/pkg/image_png.htm)

37. archive
包含文件的归档
**[archive/tar](https://studygolang.com/static/pkgdoc/pkg/archive_tar.htm)**
压缩**[archive/zip](https://studygolang.com/static/pkgdoc/pkg/archive_zip.htm)**

38. compress
主要是与压缩有关的操作，包含常见的几种压缩格式bzip2、flate、gzip、lzw、zlib
有些操作要与tar联动使用
**[compress/bzip2](https://studygolang.com/static/pkgdoc/pkg/compress_bzip2.htm)
[compress/flate](https://studygolang.com/static/pkgdoc/pkg/compress_flate.htm)
[compress/gzip](https://studygolang.com/static/pkgdoc/pkg/compress_gzip.htm)
[compress/lzw](https://studygolang.com/static/pkgdoc/pkg/compress_lzw.htm)
[compress/zlib](https://studygolang.com/static/pkgdoc/pkg/compress_zlib.htm)**

39. **[mime](https://studygolang.com/static/pkgdoc/pkg/mime.htm)**
[MIME]([https://baike.baidu.com/item/MIME/2900607?fr=aladdin](https://baike.baidu.com/item/MIME/2900607?fr=aladdin)
)(Multipurpose Internet Mail Extensions)多用途互联网邮箱扩展类型
本包实现了一些和MIME有关的功能
**[mime/multipart](https://studygolang.com/static/pkgdoc/pkg/mime_multipart.htm)
[mime/quotedprintable](https://studygolang.com/static/pkgdoc/pkg/mime_quotedprintable.htm)**

40. index
index下只有一个子包，后缀数组
>suffixarrayb包通过使用内存中的后缀树实现了对数级时间消耗的子字符串搜索。

即将子字符串的查询时间复杂度下降到了logn
算是个算法包
**[index/suffixarray](https://studygolang.com/static/pkgdoc/pkg/index_suffixarray.htm)**

41. container
（这个涉及数据结构，放在最后来写！！！
数组、切片、映射-->内置数据结构
container中还包含了很多数据结构
堆**[container/heap](https://studygolang.com/static/pkgdoc/pkg/container_heap.htm)**
双向链表**[container/list](https://studygolang.com/static/pkgdoc/pkg/container_list.htm)**
环链**[container/ring](https://studygolang.com/static/pkgdoc/pkg/container_ring.htm)**
具体的使用看源码就可以啦，平时使用也没有特别多的操作

顺便一提，以上的标准库有一部分是依赖第三方包vender的，这个也是官方所开发

除了源码中带有的这些标准库，官方还在[Github]([https://github.com/golang](https://github.com/golang)
)上提供了很多包
