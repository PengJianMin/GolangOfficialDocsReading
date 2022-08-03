# Official Address
+ [Tutorial: Get started with Go](https://golang.google.cn/doc/tutorial/getting-started)

# 依赖追踪（Dependency Tracking）
+ 代码所依赖的第三方包的信息会被记录在自己的模块中，一个**模块通过go.mod文件来定义**，这个文件会追踪提供了**第三方包**的那些**模块**
+ go.mod文件和**源码**保存在一起，包括**源码仓库**也会有该文件。

# 创建模块（module）
+ `go mod init ${module_name}` module_name是模块路径（module path）
+ 实际开发中，模块路径常常设置成源码存放的位置，例如 github.com/mymodule
