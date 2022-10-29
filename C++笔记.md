# C++笔记



## 1.程序框架

```c++
#include <bits/stdc++.h>
using namespace std;

int main()
{
    //程序主体内容
    return 0;
}
```



## 2.变量类型与变量定义

`int`整数	`short`短整型	`long`长整型	`long long`长长整型

`float`单精度浮点数	`double`双精度浮点数

`char`字符型	`string`字符串	`bool`布尔型	`void`空类型



定义：`(const) 变量类型 变量名( = 初始值);`

`const`修饰为常量，后面不可重新赋值更改



## 3.输入输出

输出：e.g.`printf("Hello World!");`  `printf("a=%d, b=%d",a,b);` (`%d`为格式符)

​					`cout<<"Hello World!"<<endl;` `cout<<"a="<<a<<", b="<<b<<endl;`

格式符：`%d`十进制整数 `%u`无符号整数 `%o`八进制 `%x`十六进制 `%c`字符 `%s`字符串 `%f`浮点数 `%lf`长浮点数(双精度浮点数)

​				`%5d`5位宽整数，以空格补足 `%02d`2位宽整数，以0补足 `%.2lf`两位双精度浮点小数



输入：e.g. `scanf("%d %d",&a,&b);`(scanf直接访问地址索引至变量，故用取址符&)

​					`cin>>a>>b;`



## 4.逻辑运算符 位运算

逻辑运算：`a&&b`与 `a||b`或 `!a`非

位运算：`&`与 `|`或 `~`非 `^`异或 `<<`左移(不足补零) `>>`右移(低位舍弃)



## 5.if条件句

```C++
if(condition 1)
{
    //条件1符合时运行
}
else if(condition 2)
{
    //条件2符合时运行
}
else if(condition 3)
{
    //条件3符合时运行
}
else
{
    //以上条件均不符合是运行
}
```



## 6.三目运算符

`(syntax 1)?(syntax a):(syntax b)`

语句1为真时，返回语句a的值，否则返回b的值



## 7.switch条件句

```C++
switch(var_name)//变量为整型变量或字符型
{
    case value1:
        //当值为此时运行
        break;//若无此句会执行下一分支直至下一个break
    case value2:
        
        break;
    default:
        //以上条件均不符合时运行
        break;
}
```

