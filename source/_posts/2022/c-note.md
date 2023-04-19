---
title: C语言学习笔记
excerpt: 学校教材内容的摘要
index_img: /img/c语言.webp
date: 2022-04-02 09:33:04
categories: 
- 学习
tags:
- C语言
- 笔记
---

# 3.第三章:数据类型运算符与表达式
## 3.1常量和变量
### 3.1.1常量
常量有以下几类：整型常量，实型常量，字符常量，字符串常量，符号常量。
其中符号常量的定义:
```c
#define 标识符 常量
#define PI 3.1415926
```
### 3.1.2变量
```c
//变量的定义:
int c1, c2, c3;
//变量的赋值
c1 = 10
```
## 3.2数据类型
基本数据类型:

| 类型  | 说明  | 	空间 (字节)  |
| :------------: | :------------: | :------------: |
| char  | 字符型  | 1  |
|  int |  整型 | 4  |
| short/long  | 短整形 / 长整形  | 2/4  |
| float  | 单精度实型  |  4 |
| double  | 双精度实型  |  8 |

修饰符:[添加在char或int前面]

| 修饰符  | 说明  |
| :------------: | :------------: |
| signed  | 有符号  |
| unsigned |  无符号 |

## 3.3整型
### 3.3.1整型常量
1.十进制:由0-9组成:100 , -200
2.八进制:由0开头,数字0-7组成,如0111 (=73), 010007 (=4103)
3.十六进制:由0X或0x开头,由0-9, a-f (或A-F)组成,如0x16 (=22), 0xA3 (=163)
### 3.3.2整型变量
见3.1.2
## 3.4实型数据
### 3.4.1实型常量
1.小数形式: 数字0-9和小数点组成,小数点必须有: 0.3   .23   23.  都合法
2.指数形式:  3.14E-2 (=0.0314)
## 3.5字符常量
### 3.5.1字符常量
由单引号括起作为定界符
1.普通字符常量:值由ASCII码确定
2.转义字符常量:
转义字符表:

| 字符  | 功能  |  ASCII码 |
| :------------: | :------------: | :------------: |
| \0 | 表示字符串结束 | 0 |
| \n | 换行到下一行行首 | 10 |
| \t | 横向跳格到下一个输出区 | 9 |
| \v | 竖向跳格 | 11 |
| \b | 退格 | 8 |
| \r | 回车 | 13 |
| \f | 换页到下页开头 | 12 |
| \' | 单引号字符 | 39 |
| \" | 双引号字符 | 34 |
| \\\\ | 反斜杠字符 | 92 |
| \ddd | 1~3位8进制数表示的字符	| 0-255 |
| \xhh | 1~2位16进制数表示的字符 | 0-255 |

例子:
```c
printf("This\tisn\b\ta\t\'book\'\n")
//输出:
This_ _ _ _is_ _ _ _ _ _a_ _ _ _ _ _ _'book'
```
### 3.5.2字符变量
|字符变量|ASCII码|
| :------------ | :------------ |
|'A'|65|
|'a'|97|
|'1'|49|
|' '|32|
|'%'|37|
|'\n'|10|

### 3.5.3字符串常量
由双引号括起的字符序列,自动以\0作为结束标志
china:

|存储格式|C|h|i|n|a|\0|
| :------------: | :------------: | :------------: | :------------: | :------------: | :------------: | :------------: |
| 实际以ASCII存储  |  67 |  104 | 105  | 110  | 97  | 0  |

## 3.6运算符
### 3.6.1运算符
#### 1.1算术运算符:
\+ \- \* \/ \%

#### 1.2自增减运算符
结合方向由右到左
注:在只需对变量本身进行加减的情况下前后缀运算效果相同，但表达式的结果可能不同

```c
//后缀运算：先把I的值赋给X然后I的值加1
x=i++
//前置运算：先把I的值加1再将I的值赋给Y
y=++i
```

```c
int a=3,b=5,c,d;
c=(++a)*b;
//结果为a=4,c=20
int a=3,b=5,c,d;
c=(a++)*b;
//结果为a=4,c=15
```

#### 2.赋值运算符

如:
a+=b 等价于 a=a+b
a%=b 等价于 a=a%b
...

#### 3.逻辑运算符
|!|非|
| :-----------: | :------------: |
|&&|与|
| ll  |或|

(1) !的结合方向由右到左且优先级高于算术运算符, &&,|| 的结合方向由左到右,优先级低于算术运算符和关系运算符但高于赋值运算符
(2) 优先级:! > && > ||
(3) !15 = 0 , !1 = 0, !0 = 1
(4)&&前表达式不为0才会执行后侧, ||前表达式为0才会执行后侧

#### 4.条件运算符

由?和:组成,连接三个对象,唯一的三目运算符
优先级高于赋值运算符和逗号运算符但低于其他运算符结合性方向为自R至L
表达式1 ? 表达式2  : 表达式 3
先计算表达式1,若为非零值则整个表达式的值为表达式2,若为0则整个表达式的值表达式三

注:false的值为0,true的值为1

#### 5.逗号运算符

用于连接若干个表达式
依次计算被逗号分隔的表达式,并将最后一个表达式的值作为整个逗号表达式的值

#### 6.圆括号运算符

优先级最高. 将某些运算符和运算对象括起来后,他们应被优先运算

### 3.6.3表达式数据类型转换
#### 1.自动转换

char,short→int→unsighed→long→double←float

#### 2.强制转换

(类型标识符)表达式

```c
(float)10/4
//10转换后计算除法
(float)(10/4)
//先计算除法,将结果转换
//无小数的除法运算直接删除小数点后数位
int 10/ int 4 = 2
```

强制转换时,得到一个转换后的中间变量,原变量类型未改变

# 4.第四章:基本输入输出
## 4.2数据输出
### 4.2.1字符输出函数putchar(c)
在屏幕上输出一个字符
使光标移至下一行:
```c
putchar('\n')
```
### 4.2.2格式输出函数printf(格式控制,参数2,参数3,...,参数n)
格式说明符:
整型数据:

|格式说明符|说明|
| :------------: | :------------: |
|%d 或 %i|有符号10进制输出整数|
|%o|无符号八进制输出整型数(无0)|
|%x 或 %X|无符号16进制输出整型数(无0x)|
|%u|无符号十进制输出整型数|

实型数据:

|格式说明符|说明|
| :------------: | :------------: |
|%f|以小数形式输出的实型数|
|%e 或 %E|以指数形式输出的实型数|
|%g 或 %G|以数值宽度最小的形式输出的实型数|

字符型数据:

|格式说明符|说明|
| :------------: | :------------: |
|%c|输出一个字符|
|%s|输出一个字符串(不包含结尾标识 \0 )|

其他:

|格式说明符|说明|
| :------------: | :------------: |
|%%|输出%本身|

附加格式说明符:

|符号|说明|
| :------------: | :------------: |
|l|输出长整型数(只可与d,o,x,u结合使用)|
|m|指定数据输出的宽度m,不足则空格补齐,超出则按实际宽度输出|
|.n|对于%f或%e输出的实型数据,输出n位小数,若小数位超出则四舍五入.对于%s输出的字符串则表示从字符串左端截取n个字符|
|+|	使输出的数值数据无论正负都带符号输出|
|-|使数据按左对齐方式输出(没有则右对齐)|

## 4.3数据输入
### 4.3.1字符输入函数getchar()
只能接收一个字符

### 4.3.2格式输入函数scanf(格式控制,地址参数1,地址参数2,...,地址参数n)
格式控制的以下数据与上文4.0.2的printf()相同:整型,实型,字符型,
此外,还有附加格式说明符:

|符号|说明|
| :------------: | :------------: |
|m|用于指定输入数据的域宽|
|*|忽略读入的数据|

```c
//例如:
scanf("%2d%*2d%3d",&a,&b)
//若输入的内容为 1234567 时,结果为:
a=12,b=567
```

注:使用该函数输入字符串时,字符串中不能含有空格,否则将以空格作为字符串的结束符.

# 5.第五章:选择结构程序设计
## 5.2逻辑运算符和逻辑表达式

到目前为止的运算符优先级:
!(逻辑非) > 算术运算符 > 关系运算符 >  && 与 ||   >  |  >  赋值运算符

## 5.3:C99的布尔值

```c
//声明一个布尔型变量
_boll b;
//b的值只能为0/1,若大于1则赋值为1,如下执行后b=1
b=10;
//如果使用以下头文件可以使用true和false代表1和0,如下使用
#include<stdbool.h>
bool b;
b=true;
```

## 5.4:if结构

```c
if (<表达式>)<语句>
//当<语句>有多行时,需要整个用{}括起
if (<表达式>)<语句1>
else if (<表达式>) <语句2>
else <语句3>
```

## 5.5条件运算符与条件表达式
上文3.6.1.4已经叙述.

## 5.6:switch语句结构

```c
switch (<表达式>){
    case <常量表达式1>: 
        <语句1>
        break;
    ...
 
    case <常量表达式n>:
        <语句n>
        break;
    default : <语句n+1>
//如果每个case都不满足,则执行default的内容
```

注:
1.<常量表达式n>不能包含变量和函数调用
2.<表达式>不能用浮点数和字符串
3.每个分支后面的语句不需要{}括起
4.如果没有break,则不会退出switch,即无论如何都会执行default

# 6.第六章:循环结构程序设计
## 6.1:循环结构控制语句
### 6.1.1:while循环
```c
while (表达式) 循环体
```
注:循环体如果有多行语句则需要{}括起

### 6.1.2:do-while循环

```c
do 循环体
while (表达式);
```

与while区别是先执行循环体再判断,若满足则再次执行循环体

### 6.1.3:for循环

```c
for (初始条件;循环条件判断;循环调整) 循环体
```

注:
1.可以将初始条件省略,在for循环之前给循环变量赋值
2.可以将循环条件判断省略,将会成为死循环
3.可以将循环调整省略,如果后续不能保证循环结束,将成为死循环
4.C99允许for语句在初始条件中定义变量并赋值

### 6.1.4:三种循环语句的比较
三个循环都可以用break;语句跳出循环,用continue;语句结束本次循环
其中break的作用是结束并跳出整个循环, continue的作用是结束本次循环并进行下一次循环

## 6.2:循环中的转移语句:6.1.4已说明不再赘述
## 6.3,6.4两节不再赘述
# 7.第七章:数组
## 7.1一维数组
### 7.1.1一维数组的定义与引用
#### 1.定义:
类型说明符 数组名 [元素个数]

类型说明符是任意一种基本数据类型或构造数据类型,定义了全体数组元素的数据类型
定义数组时需要指定数组元素的个数,也就是数组的长度.
数组是一个整体,是由连续的内存位置组成的.

#### 2.引用:
数组名[下标]

注:数组的长度可以是常量或变量等任意有效的整型表达式,大于0就好

### 7.1.2一维数组的初始化
```c
//将数组的所有元素初始化为0,例如:
int nums[10] = {0}
//只有全部赋值为0的时候可以这样写,如果要全部为1必须要写10次1
```
注:如果在定义时就给全部元素赋值,可以不给出数组长度

```c
int a[]={1,2,3}
```

## 7.2字符数组
用来存放字符的数组称为字符数组,实际上是一系列字符的集合,也就是字符串.
因为在C语言中没有专门的字符串变量,没有string类型,通常就用一个字符数组来存放一个字符串
如:        char c[10];

### 7.2.1:字符数组的初始化
初始化:
```c
char str[]={"C program"}
//或
char str[]="C program"
```
由于字符串会将 \0 作为结束标志,因此上面的"C program"实际长度为10

### 7.2.2字符数组的输入与输出
```c
//输出
char c[]="lab";
printf("%s",c);
//输入
char st[15];
scanf("%s",st);
printf("%s",st);
```
### 7.2.3字符串处理函数:使用时应包含头文件:"string.h"

1.字符串输出函数puts(字符数组名);

2.字符串输入函数gets(字符数组名);
该函数不以空格作为字符串输入结束的标志,而只以回车作为输入结束.

```c
char st[15];
gets(st);
puts(st);
```
3.连接函数strcat(字符串1,字符串2):将字符串2连接在字符串1后面[字符串1发生改变]
返回值为字符串1的首地址

4.复制函数:strcpy(字符串1,字符串2):将字符串2复制到字符串1中.

5.比较函数:strcmp(字符串1,字符串2);

按照顺序比较两个数组中的字符串.从第1个字符开始如果ASCII相同则继续比较,如果所有字符都相同,则返回值为0.如果有两个字符不相等且第1个比第2个大,则返回一个正数,否则返回一个负数.如果字符串1的长度大于字符串2,且前面的字符相同,则也按字符串1大于字符串2处理.

6.获取长度:strlen(字符串名):不包括表示结束的 '\0'

## 7.3二维数组
```c
//多维数组声明:
类型 说明符 数组名[第1维长度] [第2维长度] ... [第n维长度];
//初始化
int array[3][4]={1,2,3,4,5,6,7,8,9,10,11,12};
int array[3][4]={{1,2,3,4},{5,6,7,8},{9,10,11,12}};
```

注:
1.如果有没被赋值的元素则自动赋值为0
2.如果对全部元素赋值,那么第1维的长度可以不给出.但无论如何不能省略第2维的长度

# 8.函数
## 8.1:函数的定义
```c
类型标识符 函数名(参数){
语句;
return 表达式;
//或者
return (表达式);
}
```
类型标识符为函数返回值的类型

## 8.5:数组作为函数参数
数组可以作为函数实参,但不能作为形参.例如:
```c
float average(float array[10]){
    xxxxxxxx;
}
```
## 8.6:变量的作用域和存储
在函数内部定义的变量只在函数内有效

### 8.6.3变量的存储方式
四种:自动auto,静态static,寄存器register,外部extern

函数中的局部变量,自动分配auto类别,函数调用后内存释放,如果要函数执行后局部变量内存不被释放,则应声明为static类型:
```c
static int a;
```
寄存器变量存储于CPU寄存器,存取速度最快
使用外部变量需要一个文件直接对其定义,另一个将其作为外部变量引用

## 8.7内外部函数
函数声明时前面加 static 可以使其他文件无法引用此函数,避免名称冲突.
如果需要多个文件使用该函数,可以在前面加 extern 从而使其他文件可以引用此函数
默认情况下为 extern,无论是声明还是定义

# 9.指针
## 9.2指针的定义和初始化
### 9.2.1定义
T为某个数据类型,如int,double,char等, p是指向T类型变量的指针
```c
T * p;
//如:
int i, *ip;
//i是int型变量,ip是指向int型对象的指针
```
### 9.2.2初始化和赋值
#### 1.取地址运算符---&
```c
int i=23;
int j;
int *p=&i;//指针初始化指向i
p=&j;//指针改变赋值,p指向j
```
指针类型必须与其指向的对象类型严格匹配

#### 2.格式符%p输出指针的值
```c
#include <stdio.h>
int main(){
int a=10;
int *p=&a;
printf("%p\n",p);
//或
printf("%p\n",&a);
//sizeif()运算指针变量内存占用
printf("size of int*:%d,value:%p\n",sizeof(p),p);
}
 
输出:
000000000062FE14
000000000062FE14
size of int*:8,value:000000000062FE14
```
#### 3.间接运算符 *

如果指针指向了一个对象,可以使用间接运算符 * 访问对象.如果给其赋值,则就是给指针的对象赋值
可视为是&的逆操作,即&*p==p

#### 4.指针值

有四种状态:指向对象,指向对象前后的位置,空指针,无效指针
由此想到一句吵架可用的话:~~你就是一个没有对象的野指针!~~

访问无效指针将引发错误,指向对象前后的位置和空指针尽管有效但是值可能无效,因此不允许访问其对象

#### 5.void*指针

可以存放任意对象的地址,即可以指向任意类型数据.
因为其只是表明相关的值是一个地址值,没有类型信息,所以*不能对其对象进行操作*[一本正经]

其主要作用是做函数参数和函数返回值

#### 6.空指针

值为0的表达式都称为空指针常量,能够转换为任意类型的指针.
但是不能直接把int变量赋值给指针.

获得空指针方法:
```c
int *p1=0;
int *p2=(void*)0;
 
#include <stddef.h>
//或其他头文件定义NULL
int *p=NULL;
 
//这是错误的:不能直接int赋值,即使其值为0
int zero=0;
int *p=zero
```
判断空指针可用`p==NULL`或`p==0`或`!p`等方法.

### 9.2.3指针与const
#### 1.指针定义前加const,使之指向对象的值不能修改(其对象为常量)
```c
const T* p;
//或
T const *p;
```
可以使用一个指向常量的指针指向变量对象
```c
#include <stdio.h>
int main(){
	int b=32;
	const int *cpb=&b;
 
    //如果使用*cpb=30;则会报错
	b=30;
 
	printf("%d",b);
}
```
但是指针指向为变量,指向一个常量,将会引发错误或警告

#### 2.指针常量

指针常量本身的值不能修改,所以必须定义时初始化
```c
T* const cp=&obj;
```
 指针常量的所指向的对象不能为常量

#### 3.指向常量的指针常量

```c
const T * const cp=&obj;
```
###  9.2.4指针与restrict
关键字restrict在C99中引入,表示对象已经被指针引用且不能通过指针以外的任何方式修改对象内容

## 9.3指针与数组
### 9.3.1指针与一维数组
#### 指向数组元素
```c
int a[5]={1,2,3,4,5}
int* p;
p=&a[0]
```
#### 数组名与指针,sizeof函数
数组的指针就是数组首元素的指针
即`int* p=a;`等价于`int* p=&a[0];`

sizeof(数组名);可以得到指针变量的字节数
即`int a[10];`时,`sizeof[a0]`与`sizeof[int];`相等,且为`sizeof(a);`的10倍

#### 指针的运算

```c
int a[5];
int* p=a;
p+=2;
//此时p从指向a[0]改为指向a[2]
//p向后移动4个字节,因为int类型占用字节数为2
```
指针的自增和自减同理
指针也可以相互加减
类型不同的指针不能相互赋值,相同的可以

当两个指针指向同一个数组时,才可以进行数组的关系运算
可以比较两个指针的地址值大小

可以将指针作为表达式,当其为空指针时表达式为假,反之为真

#### 通过指针引用数组
```c
int a[5];
int *p=a;
//或int *p=a[0];
```
此后,使用a或p引用数组方法相同
`a[i]`可以这样访问:`*(a+i)`或`*(p+i)`或`p[i]`
#### 通过指针访问未命名数组
```c
int* p=(int []){2,4,8};
```
这里的`(int []){2,4,8}`就是一个未命名数组,可以使用p来访问数组

如果语句在函数外部，则具有静态生存期，花括号列表中的值必须为常量
若在函数内，则可以为变量
### 9.3.2指针与多维数组
#### 二维数组元素的存储与地址
二位数组其实就是一维数组的数组。
所以，如果定义一个`int a[3][4]`，那么`a`这个指针指向数组首个元素，也就是第一个由4个int组成的一维数组。上一节讲到可以用指针运算来指向数组元素，同样的方法，所以`a[0]+1`表示`a[0][1]`元素地址，`a[2]+3`表示`a[2][3]`元素地址。

| 表示形式  | 含义  | 类型  |
| ------------ | ------------ | ------------ |
| `a`，`&a[0]`，`a+0`  | 指向一维数组a[0]的地址  | 行地址  |
| `*a`，`*(a+0)`，`*a[0]`，`&a[0][0]`，`a[0]+0`，`*(a+0)+0`  | 指向元素a[0][0]的地址  | 列地址  |
| `*(a[1]+2)`，`a[1][2]`  | 元素的值  |  元素的值 |

### 9.3.3指针与字符串
字符串实际上就是一个带有结束标识`\0`的字符数组。
