# Official Address
+ [Tutorial: Create a Go module](https://golang.google.cn/doc/tutorial/create-module)
# **创建**模块[Tutorial: Create a Go module](https://golang.google.cn/doc/tutorial/create-module)
+ Go的代码通过**包（package）** 进行分组管理，包通过**模块（module）** 进行分组管理。
+ 创建模块步骤
1. 创建目录并进入目录
    + `mkdir greetings; cd greetings`
2. 执行`go mod init`命令，为模块赋予一个**路径（Path）**，如果该模块之后要发布到网上，这个路径就是**代码仓库所在位置**
    + `go mod init example/greeetings`
    + **为模块赋予一个路径，相当于在这个路径下有存在包**，因为在导入包的时候，也是写的**完整的模块名**，默认包名是最后一个单词。即**import后面接的是一个路径，不是包名**。import的真正意思是 导入后边接着的**路径下的包**，只不过我们通常把包名设置成和最后一个单词一样，这样方便他人直接使用。
    + go.mod文件内容包括：
        + 自身模块名
        + Go版本信息
        + 依赖的模块及其版本（保证**编译可重现**）
3. 编写代码
    + 包名通常为**模块路径的结尾** 
      + `package greetings`
    + 在Golang中，函数名开头如果是**大写**，表明其实**可导出，即可被导入（import）**，可以在该函数所在包的**包外**进行调用，**类似public**
# **调用**模块[Call your code from another module](https://golang.google.cn/doc/tutorial/call-module-code)
1. **import**和**module path**的**真正含义**
    + **模块名**（module name） 本质上是一个**路径**（module path），该**路径下包含包（package）**，如果填的github之类的，就是**远端路径**
    + import后面接的是一个**路径**，**不是包名**，通常路径的**最后一个单词**与**其包含的包**的包名**一致**，这样能方便他人调用
    + import的真正意思是：导入后边接着的**路径下**的**包**，你也可以设置与路径最后一个单词**不一致的包名**，这是允许的，但是不方便使用
2. 通常情况下，如果引用的是**公开发布的模块**，Go工具会找到它并**将它下载到本地**
3. 如果调用的是**未公开发布的模块**，或者是存放在**本地的模块**，则需要修改一些信息，让**Go工具可以找到它**进行**编译工作**。
    + `go mod edit -replace example.com/greetings = ../greetings`
    + 将引入路径从 example.com/greetings 改成**本地路径`../greetings`**，**`../greetings`下面有greetings这个包** 
