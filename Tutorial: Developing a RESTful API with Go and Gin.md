# Official Address
+ [Tutorial: Developing a RESTful API with Go and Gin](https://golang.google.cn/doc/tutorial/web-service-gin)

# 设计API（Design API endpoints）
+ /albums
1. `GET请求`：返回一个JSON字符串，内容是专辑列表
2. `POST请求`：接收一个JSON字符串，内容是要添加到数据库的新专辑信息
+ /albums/:id
1. `GET请求`：根据请求发送过来的id值，查询对应的专辑信息，并将结果用JSON字符串返回
# 创建工程
```
  mkdir web-service-gin
  cd web-service-gin
  go mod init example/web-service-gin
```
