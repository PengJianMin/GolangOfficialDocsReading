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
+ 编写代码（Write the code）
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
+ `/albums`的`GET请求`处理器
+ 代码编写顺序
1. 处理请求的**具体逻辑**
2. 将请求路径**映射**到该逻辑上
+ 编写代码（Write the code）
```
func getAlbums(c *gin.Context) {
    c.IndentedJSON(http.StatusOK, albums)
}
```
1. `gin.Context`是`Gin`框架**最重要**的部分，它携带了请求的细节，可以完成合理化JSON，序列化Json等等工作，它**不同于**Golang内置的**同名包`context`**
2. ` Context.IndentedJSON`会把struct**序列化**为JSON，并将它添加到响应中
```
func main() {
    router := gin.Default()
    router.GET("/albums", getAlbums)

    router.Run("localhost:8080")
}
```
3. `gin.Default()` 初始化Gin路由（router）
4. `router.GET`将`/albums` **GET请求**和`getAlbums`进行绑定
```
package main

import (
    "net/http"

    "github.com/gin-gonic/gin"
)
```
+ 运行代码（Run the code）
```
go get .
go run . 
curl http://localhost:8080/albums
```
# 编写处理器，增加新album类目（Write a handler to add a new item）
+ 编写代码
```
func postAlbums(c *gin.Context){
	var newAlbum album
	if err:= c.BindJSON(&newAlbum);err!= nil{
		return
	}
	albums = append(albums,newAlbum)
	c.IndentedJSON(http.StatusCreated,newAlbum)
}
```
1. ` Context.BindJSON`将**请求体**绑定到`newAlbum`变量
2. `http.StatusCreated` 为状态码`201`
```
router.POST("/albums", postAlbums)
```
3. `router.POST`将`/albums` **POST请求**和`postAlbums`进行绑定
+ 运行代码
```
go run .
curl http://localhost:8080/albums --include --header "Content-Type: application/json" --request "POST" --data '{"id": "4","title": "The Modern Sound of Betty Carter","artist": "Betty Carter","price": 49.99}'

curl http://localhost:8080/albums --header "Content-Type: application/json" --request "GET"
```
