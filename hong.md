## c语言的宏定义

```c
#include <stdio.h>

#define N 100

int main(){
int sum = 20 + N;
printf("%d\n",sum);
return 0;
}
```

该示例中的语句int sim = 20 + N;,N被100代替了.

#define N 100 就是宏定义, N为宏名, 100是宏的内容, 对程序中所有出现的'宏名',都用宏定义中的字符串取代换,这称为"宏代换"或"宏展开".
