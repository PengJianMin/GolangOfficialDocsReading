# Official Address
+ [Tutorial: Get started with Go](https://golang.google.cn/doc/tutorial/getting-started)

# 依赖追踪（Dependency Tracking）
+ 代码所依赖的第三方包的信息会被记录在自己的模块中，一个**模块通过go.mod文件来定义**，这个文件会追踪提供了**第三方包**的那些**模块**
+ go.mod文件和**源码**保存在一起，包括**源码仓库**也会有该文件。

# 创建模块（module）
+ `go mod init ${module_name}` module_name是模块路径（module path）
+ 实际开发中，模块路径常常设置成源码存放的位置，例如 github.com/mymodule

# 包（package）
+ 包是对函数的分组，它是由**一个目录下的所有文件组成**，即一个目录下**只能表示一个包**。

## 模块和包*并不冲突*，模块下可以有多个目录，一个包只能对应一个目录，一个目录只能对应一个包，所以模块下可以有多个包。

# 调用外部包（external package）
+ [pkg.go.dev](pkg.go.dev) 上可以找到许多公开的模块，**模块中的包**可以被调用。
+ `go mod tidy`：更新依赖追踪的信息。
1. 一旦调用了外部包，便有了**依赖关系**，这个命令可以用来**记录依赖关系**，它将**更新go.mod文件**的内容，并在**go.sum文件**中记录该模块的**校验信息**。
