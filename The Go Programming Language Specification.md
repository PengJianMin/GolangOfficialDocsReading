# Official Address
[The Go Programming Language Specification](https://golang.google.cn/ref/spec)

# 源码的语法元素（Lexical elements）
+ 注释（comments）
1. 行注释：`//`开头至该**行结尾**
2. 块注释：`/*`开头 ，`*/`结尾
+ 代号（tockens）
1. 代号指源码中的各种词汇，一共有5大类：
    + 标识符（identifiers）
    + 关键字（keywords）
    + 操作符（operators）
    + 标点符号（punctuation）
    + 字面量（literals）
2. 分号自动插入原则（;）
    + an identifier
    + an integer, floating-point, imaginary, rune, or string literal
    + one of the keywords break, continue, fallthrough, or return
    + one of the operators and punctuation ++, --, ), ], or }
+ 标识符（identifiers）
1. 标识符必须以**字母开头**
2. 有些标识符被**事先声明给占用了**
+ 关键字（keywords），已被占用，不可作为标识符：
1. ```break        default      func         interface    select
      case         defer        go           map          struct
      chan         else         goto         package      switch
      const        fallthrough  if           range        type
      continue     for          import       return       var
+ 操作符（operators）和标点（punctuation）
1. ```+    &     +=    &=     &&    ==    !=    (    )
      -    |     -=    |=     ||    <     <=    [    ]
      *    ^     *=    ^=     <-    >     >=    {    }
      /    <<    /=    <<=    ++    =     :=    ,    ;
      %    >>    %=    >>=    --    !     ...   .    :
           &^          &^=          ~
+ 整型字面量（Integer literals）
1. 
