# Official Address
+ [Tutorial: Create a Go module](https://golang.google.cn/doc/tutorial/create-module)
# **创建**模块[Tutorial: Create a Go module](https://golang.google.cn/doc/tutorial/create-module)
+ Go的代码通过**包（package）** 进行分组管理，包通过**模块（module）** 进行分组管理。
    + 模块名等价于一个本地路径或网络路径，路径下有和模块名最后一个单词**同名**的包，方便大家下载调用。
    + **import**和**module path**的**真正含义**
        + **模块名**（module name） 本质上是一个**路径**（module path），该**路径下包含包（package）**，如果填的github之类的，就是**远端路径**
        + import后面接的是一个**路径**，**不是包名**，通常路径的**最后一个单词**与**其包含的包**的包名**一致**，这样能方便他人调用
        + import的真正意思是：导入后边接着的**路径下**的**包**，你也可以设置与路径最后一个单词**不一致的包名**，这是允许的，但是不方便使用。
        + 一个要运行的包，必须声明为**main包**，不管其路径名最后一个单词是什么。这也从一方面**证明了包名与路径名无关**
+ **创建**模块步骤
1. 创建目录并进入目录
    + `mkdir greetings; cd greetings`
2. 执行`go mod init`命令，为模块赋予一个**路径（Path）**，如果该模块之后要发布到网上，这个路径就是**代码仓库所在位置**
    + `go mod init example/greeetings` 声明模块路径为xample/greeetings，默认模块名和**这个路径下的包名**都是greetings。
    + go.mod文件内容包括：
        + 自身模块名
        + Go版本信息
        + 依赖的模块及其版本（保证**编译可重现**）
3. 编写代码
    + 包名通常为**模块路径的结尾** 
      + `package greetings`
    + 在Golang中，函数名开头如果是**大写**，表明其实**可导出，即可被导入（import）**，可以在该函数所在包的**包外**进行调用，**类似public**
# **调用**模块[Call your code from another module](https://golang.google.cn/doc/tutorial/call-module-code)
1. 通常情况下，如果引用的是**公开发布的模块**，Go工具会找到它并**将它下载到本地**
2. main运行的包名必须声明为main包，哪怕它的模块名是example.com/hello， 两者关系是“**在example.com/hello 下有一个main包**”
3. 如果调用的是**未公开发布的模块**，或者是存放在**本地的模块**，则需要修改一些信息，让Go工具可以找到它（**只是找到，知道在哪**），需要用`go mod tidy`使得更改**生效**
    + `go mod edit -replace example.com/greetings = ../greetings`，go.mod文件中会多出一条**replace记录**
        + 将引入路径从 example.com/greetings 改成**本地路径`../greetings`**，**`../greetings`下面有greetings这个包** 
    + 执行 `go mod tidy` 使得更改生效，go.mod文件中会多出一条**require记录**，此时**依赖追踪才正式开始**
        + require记录后边会有模块的**版本号**，确保引入正确的版本
# 返回（Return）并处理错误（Handle error）[Return and handle an error](https://golang.google.cn/doc/tutorial/handle-errors)
1. `errors.New`函数返回一个error对象
    + `errors.New(info)`
2. `log.Prefix`设置打印信息的前缀
    + `log.Prefix("greetings:")`
3. `log.Fatal`打印错误信息并且结束程序
    + `log.Fatal(err)`
# 返回随机（random）问候[Return a random greeting](https://golang.google.cn/doc/tutorial/random-greeting)
1. slice的类似数组，但它的**大小是动态**的
    + 声明slice时，不需要写明大小 `[]string`
2. 调用`math/rand`包可以生成**随机数**，可以传入**随机种子seed** `rand.Seed(time.Now().UnixNano())`
3. **init方法**：主要负责**初始化**工作
    + 如果init方法和main方法在同一包中：**先于main方法**执行
    + 如果init方法在第三方包中：在**导入时会执行**，再让main方法使用，同样**先于main方法**执行
# 返回对多人的问候[Return greetings for multiple people](https://golang.google.cn/doc/tutorial/greetings-multiple-people)
1. 当需要变动函数参数时，会使得**函数签名（unction's signature）** 发生变化，如果是要公开发布的模块，最好建议重新起一个函数名，这样才能**向后兼容**（backward compatibility）。
2. 空标识符 "\_" Go blank identifier可以忽略**不需要的返回值**
# 添加测试[Add a test](https://golang.google.cn/doc/tutorial/add-a-test)
1. Golang内置了单元测试（unit test）
2. 测试工具
    + 使用命名规范（naming convention）
    + 使用`testing`包（testing package）
    + 使用`go test`命令
3. 测试步骤
    + 创建测试文件
        + 在需要测试的代码文件**相同路径**下创建测试文件
        + 测试文件必须以**_test.go**结尾
        + 该命名方式告诉`go test`命令这个文件包含**测试方法（test function）**
    + 编写测试方法（test function）
        + 测试方法/函数必须**以Test开头**，参数必须为***testing.T**指针类型（testing为包）
            + `func TestHelloName(t *testing.T){}` `func TestHelloEmpty(t *testing.T){}`
        + `t.Fatalf()`可以将错误信息打印至**控制台（console）**，并中断程序
    + `go test` 命令进行测试
        + 在该测试文件所在目录下执行
        + \-v 标识符可以获取更详细的信息 `go test -v`
# 编译和安装应用[Compile and install the application](https://golang.google.cn/doc/tutorial/compile-install)
1. `go build`：编译所有包（package）和依赖（dependencies），但**不执行安装**
2. `go install`：编译并且安装包
