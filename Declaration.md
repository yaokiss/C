1. 声名语法
1. 声明说明符：

  * 储存类型： auto、 static、 extern、 register。在声明中最多可以出现一种储存类型，如果表示储存类型，则必须把它放置在声明中的首要位置。
  * 类型限定符： 只有两种类型限定符： const、 volatile。生命可以指定一个限定符、两个都有或者一个也没有。
  * 类型说明符： 关键字void、 char、 short、 int、 long、 float、 double、 signed、 unsigned。全部都是类型说明符。
  
  ```
  带有
  存储类型        声明符
     ↓          ↙ ↓ ↘
  static float x, y, *p 
            ↑
         类型说明符
 ```
