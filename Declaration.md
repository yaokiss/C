1. 声名语法
1. 声明说明符：

  * 储存类型： auto、 static、 extern、 register。在声明中最多可以出现一种储存类型，如果表示储存类型，则必须把它放置在声明中的首要位置。
  * 类型限定符： 只有两种类型限定符： const、 volatile。生命可以指定一个限定符、两个都有或者一个也没有。
  * 类型说明符： 关键字void、 char、 short、 int、 long、 float、 double、 signed、 unsigned。全部都是类型说明符。
  
  ```
  带有存储类型和三个声明符的声明。
  
  存储类型        声明符
     ↓          ↙ ↓ ↘
  static float x, y, *p; 
            ↑
         类型说明符
 ```
 ```
 有类型限定符但是没有存储类型，还有初始化式。
 
 类型限定符    声明符
    ↓          ↓
 const char month[] = "January";
        ↑                 ↑
     类型说明符          初始化式
```
```
既有存储类型也有类型限定符，还有三种类型说明符，顺序并不重要。

  存储类型           类型说明符
    ↓              ↙   ↓  ↘
extern const unsigned long int a[10];
         ↑                       ↑
      类型限定符                 声明符
```
```
和变量声明一样，函数声明也有存储类型、类型限定符和类型说明符。
    存储类型       声明符
       ↓           ↓
   extern int square(int);
           ↑
        类型说明符
```
