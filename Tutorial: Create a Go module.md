# Official Address
+ [Tutorial: Create a Go module](https://golang.google.cn/doc/tutorial/create-module)
# **创建**模块[Tutorial: Create a Go module](https://golang.google.cn/doc/tutorial/create-module)
+ Go的代码通过**包（package）** 进行分组管理，包通过**模块（module）** 进行分组管理。
+ 创建模块步骤
1. 创建目录并进入目录
    + `mkdir greetings; cd greetings`
2. 执行`go mod init`命令，为模块赋予一个**路径（Path）**，如果该模块之后要发布到网上，这个路径就是**代码仓库所在位置**
    + `go mod init example/greeetings`
    + **为模块赋予一个路径，相当于在这个路径下有存在包**
    + go.mod文件内容包括：
        + 自身模块名
        + Go版本信息
        + 依赖的模块及其版本（保证**编译可重现**）
3. 编写代码
    + 包名通常为**模块路径的结尾** 
      + `package greetings`
    + 在Golang中，函数名开头如果是**大写**，表明其实**可导出，即可被导入（import）**，可以在该函数所在包的**包外**进行调用，**类似public**
# **调用**模块[Call your code from another module](https://golang.google.cn/doc/tutorial/call-module-code)
