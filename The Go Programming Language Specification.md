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
1. `0b`、`0B`开头： **二进制数**
2. `0`、`0o`、`0O`开头： **八进制数**
3. `0x`、`0X`开头： **十六进制数**
4. 整型字面量中出现**下划线_**，不影响字面量的值 
```
    0x_67_7a_2f_cc_40_c6
    170_141183_460469_231731_687303_715884_105727
    4__2        // 无效：一次只能有一个下划线
```
+ 浮点型字面量（Floating-point literals）
1. `e`或者`E`表示**10为底**的指数
2. `p`或者`P`表示**2为底**的指数，在**十六进制**浮点型字面量中使用
3. 十六进制的浮点型字面量以`0x`、`0X`开头
4. 浮点型字面量中出现**下划线_**，不影响字面量的值
```
    0.15e+0_2    // == 15.0
    0x2.p10      // == 2048.0
    0X.8p-0      // == 0.5
    0x1.5e-2     // 无效，e只能出现在十进制，十六进制要用p
```
+ 虚数型字面量（Imaginary literals）
1. 使用方法和计算规则同数学上的虚数一样
```
    0123i         // == 123i for backward-compatibility
    0o123i        // == 0o123 * 1i == 83i
    0xabci        // == 0xabc * 1i == 2748i
    0x1p-2i       // == 0x1p-2 * 1i == 0.25i
```
+ 字符型字面量（Rune literals）
1. 单引号引起来 `'x'` `'\n'`
2. Go源码文本是用UTF-8编码的
    + `\`  后跟3位八进制数  `'\377'`
    + `\x` 后跟2位十六进制数 `'\xff'`
    + `\u` 后跟4位十六进制数 `'\u12e4'`
    + `\U` 后跟8位十六进制数 `'\U00101234'`
3. 字符型字面量不是以**编码字节**衡量，而以能够编码成具体含义的**多个编码字节**作为整体来衡量
    + `'ä'` 编码为（`0xc3``0xa4`）2个字节，但是视为1个rune型字符
+ 字符串字面量（String literals）
1. **原生字符串Raw string** 使用**反引号**引起来的，转义字符在其中**失效**，被视为**普通字符**，原生字符串若输出则为**原样输出**
2. **可译字符串Interpreted string** 使用**双引号**引起来的，转义字符在其中**生效**，被视为**特殊字符**
    + **\nnn** 表示八进制编码
    + **\xnn** 表示十六进制编码
    + 
```
    `中国话\n`  // 换行符不生效，原样输出
    "中国话\n" //换行符生效，会换行
```
