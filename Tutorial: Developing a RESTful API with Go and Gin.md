# Official Address
+ [Tutorial: Developing a RESTful API with Go and Gin](https://golang.google.cn/doc/tutorial/web-service-gin)

# 设计API（Design API endpoints）
+ `/albums`
1. `GET请求`：返回一个JSON字符串，内容是专辑列表
2. `POST请求`：接收一个JSON字符串，内容是要添加到数据库的新专辑信息
+ `/albums/:id`
1. `GET请求`：根据请求发送过来的id值，查询对应的专辑信息，并将结果用JSON字符串返回
# 创建工程（Create a folder for your code）
```
  mkdir web-service-gin
  cd web-service-gin
  go mod init example/web-service-gin
```
# 生产数据（Create the data）
+ 代码
```
package main

type album struct {
	// Golang中以大写开头有public的蕴意
	ID string `json:"id"` 
	Title string `json:"title"`
	Artist string `json:"artist"`
	Price float64 `json:"price"`
}

var albums = []album{
	{ID: "1", Title: "Blue Train", Artist: "John Coltrane", Price: 56.99},
	{ID: "2", Title: "Jeru", Artist: "Gerry Mulligan", Price: 17.99},
	{ID: "3", Title: "Sarah Vaughan and Clifford Brown", Artist: "Sarah Vaughan", Price: 39.99},
}
```
+ **结构体标签struct tags**可以使得结构体在**序列化**成JSON时，每个**属性**应该对应的**JSON字段**的名称，使**值**可以赋到**对应的字段**上
# 编写处理器，返回所有album类目（Write a handler to return all items）
1. `/albums`的`GET请求`处理器
2. 代码编写顺序
    + 响应的具体逻辑
    + 将请求路径**映射**到该逻辑上
3. 代码
```

```
