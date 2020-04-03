 参考书籍《C Primer Plus》《C程序设计语言》《C和指针》

# 三字母词


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


# 注释


C语言有两种注释方法

  * 以`/*`开始，以`*/`结束,中间可以包含`除*/之外`的任何字符。可以`多行注释`。

  * 以`//`开始。只能`注释单行`。

>**注意：**  注释界定符如果出现在字符串中，就不再起注释作用。所有注释会被预处理器用`空格`取代

```
int/*定义并初始化*/x=0;   /************

x=1;       ************/

x的答案是0，x=1;被注释了。
```


# 字符串常量


字符串常量（不像字符常量）可以为空（`""`）。当需要修改字符串时，应把它存储于字符数组中，再对这个数组进行修改，决对不能修改字符串本身。

![示例](https://github.com/Mrli6/The-introduction-to-C/blob/master/修改字符串问题.png)

在程序中使用字符串常量时，会生成一个“指向字符的`常量指针`”。当字符串出现在表达式中，`表达式使用的值是这些字符所存储的地址，而不是字符本身`。所以可以把字符串赋值给一个字符指针，而不可以赋值给一个字符数组。

![示例](https://github.com/Mrli6/The-introduction-to-C/blob/master/字符串指针.png)


# printf转换说明

使用转换说明(除%c)，输入值之前的空白（空格、制表符、换行符）会被跳过，`值后面的空白表示该值的结束`，所以`用%s转换说明输入字符串时，中间不能有空格`。


# 函数参数处理顺序

C语言里的函数处理参数是默认`从右往左`处理，如：

```
int a=1;
int b=2;
int c=3;

printf("%d,%d,%d\n",a+b+c,b=b*2,c++);

结果是9，4，3
```

















