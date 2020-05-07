 <p align="center">
参考书籍:<br/>《C Primer Plus》《C程序设计语言》《C和指针》
</p>

# scanf转换说明

<br/>

使用转换说明(除%c)，输入值之前的空白（空格、制表符、换行符）会被跳过，`值后面的空白表示该值的结束`，所以`用%s转换说明输入字符串时，中间不能有空格`。
```
char str[4];
scanf("%s",str);
printf("%s",str);

输入：abc
输出：abc
此时str为"abc"

输入：a b
输出：a
此时str为"a"
```

<br/>

# 三字母词

<br/>

`三字母词`以`??`为开始,`高版本编译器可以不处理三字母词`

|三字母词|等价形式|
|----|----|
| ??= |  # |
| ??( |  [ |
| ??) |  ] |
| ??< |  { |
| ??> |  } |
| ??/ | \\ |
| ??! | \| |
| ??' |  ^ |
| ??- |  ~ |

<br/>

# 注释

<br/>

C语言有两种注释方法

* 以`第一个/*`开始，以`第一个*/`结束,中间可以包含`除*/之外`的任何字符。可以`多行注释`。

* 以`//`开始。只能`注释单行`。

>注意:注释界定符如果出现在字符串中，就不再起注释作用。所有注释会被预处理器用`空格`取代

```
int/*定义并初始化*/x=0;   /************

x=1;       ************/

x的答案是0，x=1;被注释了。
```

<br/>

# 字符串常量

<br/>

* 字符串常量（不像字符常量）可以为空（`""`）。当需要修改字符串时，应把它存储于字符数组中，再对这个数组进行修改，绝对不能修改字符串本身。

![](https://github.com/Mrli6/The-introduction-to-C/blob/master/修改字符串问题.png)

* 在程序中使用字符串常量时，会生成一个“指向字符的`常量指针`”。当字符串出现在表达式中，`表达式使用的值是这些字符所存储的地址，而不是字符本身`。所以可以把字符串赋值给一个字符指针，而不可以赋值给一个字符数组。

![](https://github.com/Mrli6/The-introduction-to-C/blob/master/字符串指针.png)

<br/>

# 函数参数处理顺序

<br/>

C语言里的函数处理参数是默认`从右往左`处理，如：

```
int a=1;
int b=2;
int c=3;

printf("%d,%d,%d\n",a+b+c,b=b*2,c++);

结果是9，4，3
```

<br/>

# const和指针

<br/>

```
int const * pci;（或const int * pci;）
pci是一个指向整型常量的指针。
可以修改指针的值，但不能修改它指向的值。

int * const cpi;
cpi是一个指向整型的常量指针。
无法修改指针的值，但可以修改它指向的值。
```

<br/>

# 存储类型

<br/>

>变量的存储类型决定变量何时创建、何时销毁以及它的值保持多久。有三个地方可以存储变量：`普通内存`、`运行时堆栈`、`硬件寄存器`。

* 凡是在任何`代码块之外声明的缺省存储类型的变量`总是存储于静态`内存`中，称为`静态变量`。我们`无法为它们指定其他的存储类型`。静态变量在程序运行之前创建，在程序执行期间始终存在。它`始终保持原先的值，除非给它赋一个不同的值或者程序结束`。

* 在`代码块内部`声明的变量的缺省存储类型是自动的，`存储于堆栈中`，称为`自动变量`。它在程序执行到声明自动变量的代码块时，自动变量才被创建，但程序的执行流离开该代码块时，这些自动变量便自行销毁。如果给它`加上关键字static`，可以使它的`存储类型从自动变为静态`，在程序执行期间一直存在。`函数的形式参数不能声明为静态`，因为实参总是在堆栈中传递给函数，用于支持递归。

* `关键字register可以用于自动变量的声明`，称为`寄存器变量`。`编译器不一定要理睬register关键字`，因为寄存器大小是有限的。由于寄存器值的保存和恢复，某个特定的寄存器在不同的时刻所保存的值不一定相同，所以`机器不会提供寄存器变量的地址`。

>>寄存器变量的创建和销毁时间和自动变量相同，但它需要一些额外的工作。在一个使用寄存器变量的函数返回之前，这些寄存器先前存储的值必须恢复，确保调用者的寄存器变量未被破坏。许多机器使用运行时堆栈来完成这个任务。但函数开始执行时，它把需要使用的所有寄存器的内容都保存到堆栈中，当函数返回时，这些值再复制回寄存器中。

<br/>

# static关键字

<br/>

* 当它用于`函数定义或代码块之外的变量声明`时，static关键字用于`修改标识符的链接属性`，从external（外部链接）改为internal（内部链接），但标识符的`存储类型和作用域不受影响`。用这种方式声明的函数或变量`只能在声明它们的源文件中访问`。

* 当它用于`代码块内部的变量声明`时，static关键字用于`修改变量的存储类型`，从自动变量改为静态变量，但变量的`链接属性和作用域不受影响`。用这种方式声明的变量在程序执行之前创建，并在程序的整个执行期间一直存在，而不是每次在代码块开始执行时创建，在代码块执行完毕后销毁。

<br/>

# default与switch

<br/>

>当switch表达式的值并不匹配所有case标签的值时，default子句就会执行。

switch语句中最多只能有一条default语句，最好在default后面加上break。

```
default后面没加break，可能导致这两个代码结果不同。

switch(x){
case 1:
    printf("1\n");
    break;
default:
    printf("bye");
}

switch(x){
default:
    printf("bye");
case 1:
    printf("1\n");
    break;
}
```

<br/>

# 位操作的返回值

<br/>

```
x = 12 & 1 << 3;
y = 12 & 1 << 2;
z = 12 & 1 << 1;

x = 8 ， y = 4 ， z = 0 。
```

<br/>

# (ch=getchar())!=EOF 问题

<br/>

```
char ch;
...
while((ch=getchar())!=EOF)
...
```

EOF需要的位数比字符型值所能提供的位数要多，这也是getchar返回值是一个整型值的原因。把getchar返回值首先存储于ch中将导致它截断，然后这个被截断的值被升为整型并与EOF进行比较。当这段错误的代码在使用有符号的字符集的机器上运行时，如果取了一个值为\377的字节时，循环将会终止，因为这个值截断再提升之后与EOF相等。当这段代码在使用无符号字符集的机器上运行时，这个循环将永远不会终止。

<br/>

# sizeof(a=b+1) 问题

<br/>

sizeof操作符判断操作数的类型长度，以字节为单位表示；当操作数为数组名时，它返回该数组的长度。

因为判断表达式的长度并不需要对表达式进行求值，所以sizeof(a=b+1)并没有向a赋任何值。

```
int a = 1;
double b = 2.0;
int c = sizeof(a = b + 1);

printf("%d %.0lf %d", a, b, c);

结果为：1 2 4
```

<br/>

# ||和&&操作符的短路性质

<br/>

\|\|和&&操作符具有短路性质，`如果表达式的值根据左操作数便可决定，它就不再对右操作数进行求值`。

<br/>

# 逗号操作符

<br/>

逗号操作符将两个或多个表达式分隔开来。这些表达式`自左向右`逐个进行求值，`整个逗号表达式的值就是最后那个表达式的值`。

```
a=get_value();
count_value(a);
while(a>0){
    ...
    a=get_value();
    count_value(a);
}

上面代码可简化为：

while(a=get_value(),count_value(a),a>0){
    ...
}
```

<br/>

# 左值与右值

<br/>

* 左值意味着一个位置，右值意味着一个值。在使用右值的地方可以使用左值，在需要左值的地方不能使用右值。

<br/>

# 位和移位的运算问题

<br/>

* 负数的二进制是负数绝对值按位取反加一。

* 若给出一个负数的二进制码，可先减一再按位取反，得到的结果是负数的绝对值。

```
 10的二进制为0000 0000 0000 0000 0000 0000 0000 1010，
-25的二进制为1111 1111 1111 1111 1111 1111 1110 0111。
 10&-25结果为0000 0000 0000 0000 0000 0000 0000 0010。（2的二进制码）
 10^-25结果为1111 1111 1111 1111 1111 1111 1110 1101。（-19的二进制码）
 10|-25结果为1111 1111 1111 1111 1111 1111 1110 1111。（-17的二进制码）
 -25>>3结果为1111 1111 1111 1111 1111 1111 1111 1100。（-4的二进制码）（算术移位）
```

<br/>

# 参数传递问题

<br/>

```
float n1=3.0;
double n2=3.0;
long n3=2000000000;
long n4=1234567890;

printf("%ld %ld %ld %ld\n",n1,n2,n3,n4);
结果：
0 1074266112 0 1074266112
```

程序把传入的值放入被成为栈的内存区域。计算机根据`变量类型`把这些值放入栈中，根据`转换说明`从栈中读取值。%d读取4字节，这4个%d只读取了n1和n2，n3和n4并未被读取。

<br/>

# sizeof恒为4问题

<br/>

```
char s[]="...";
void(char*s)
{
    int num=sizeof(s);
}
```
* 对于上面的代码，无论s大小如何，num恒为4，因为数组名作为参数传递给函数时，退化为指针，指针的大小为4字节。

<br/>

# 备注2

<br/>
<br/>

# 备注3

<br/>
<br/>

# 备注4

<br/>
<br/>

# 备注5

<br/>
<br/>













