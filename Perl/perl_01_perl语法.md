# 认识Perl

#### 简单的perl文件内容

```perl
#!/bin/bash/perl 
print "Hello,World" 
```

#### 交互式Perl

```bash
perl -e 'print "Hello,World"'
```

#### 注释

```perl
# 单行注释
=pod 注释
多行注释
=cut
```

#### 脚本式编程

hello.pl

```perl
#!/usr/bin/perl
#输出 "Hello,World"
print "Hello"
```

代码中第一行使perl解释器路径，在Linux里确保执行脚本先确保可执行权限0755级别以上

print 可以使用两种语句输出结果

```perl
print ("Hello,World\n");
print "Hello,WOrld\n";
```

文件名后缀为pl或者PL

文件名可以包含数字，符号和字母，但不能包含空格，可以使用下划线（_）来替代空格

#### Perl的空白

Perl 解释器不会关心有多少个空白，以下程序也能正常运行：

```perl
print       "Hello, world\n";
```

#### 单引号和双引号

perl 输出字符串可以使用单引号和双引号

```perl
print "Hello, world\n";    # 双引号
print 'Hello, world\n';    # 单引号
$a = 10;
print "a = $a\n";
print 'a = $a\n';
```

Perl双引号和单引号的区别: 双引号可以正常解析一些转义字符与变量，而单引号无法解析会原样输出

#### Here 文档

- 1.必须后接分号，否则编译通不过。

- 2.END可以用任意其它字符代替，只需保证结束标识与开始标识一致。

- 3.结束标识必须顶格独自占一行(即必须从行首开始，前后不能衔接任何空白和字符)。

- 4.开始标识可以不带引号号或带单双引号，不带引号与带双引号效果一致，解释内嵌的变量和转义符号，带单引号则不解释内嵌的变量和转义符号。

- 5.当内容需要内嵌引号（单引号或双引号）时，不需要加转义符，本身对单双引号转义，此处相当与q和qq的用法。

  ```perl
  $a = 10;
  $var = <<"EOF";
  这是一个 Here 文档实例，使用双引号。
  可以在这输如字符串和变量。
  例如：a = $a
  EOF
  print "$var\n";
   
  $var = <<'EOF';
  这是一个 Here 文档实例，使用单引号。
  例如：a = $a
  EOF
  print "$var\n";
  ```

#### 转义符号

如果我们需要输出一个特殊的字符，可以使用反斜线（\）来转义，例如输出美元符号($)

```perl
$result = "Hello \"Perl\"";
print "$result\n";
print "\$result\n";
```

#### Perl标识符

Perl 标识符是用户编程时使用的名字，在程序中使用的变量名，常量名，函数名，语句块名等统称为标识符。

- 标识符组成单元：英文字母（a~z，A~Z），数字（0~9）和下划线（_）。
- 标识符由英文字母或下划线开头。
- 标识符区分大小写，$perl 与 $Perl 表示两个不同变量。

### 数据类型

#### 整型

Perl 实际上把整数存在你的计算机中的浮点寄存器中，所以实际上被当作浮点数看待。

在多数计算机中，浮点寄存器可以存贮约 16 位数字，长于此的被丢弃。整数实为浮点数的特例。

整型变量及运算

```perl
$x=12345;
if(1217 + 116 ==1333){
print "$x \n"
}
```

8 进制和 16 进制数：8 进制以 0 开始，16 进制以 0x 开始。

```perl
$var1 = 047;    # 等于十进制的39
$var2 = 0x1f;   # 等于十进制的31
print "$var1 \n";
print "$var2 \n";
```

#### 浮点数

浮点数数据如：11.4 、 -0.3 、.3 、 3. 、 54.1e+02 、 5.41e03。

浮点寄存器通常不能精确地存贮浮点数，从而产生误差，在运算和比较中要特别注意。指数的范围通常为 -309 到 +308。

```perl
$value = 9.01e+21 + 0.01 - 9.01e+21;
print ("第一个值为：", $value, "\n");
$value = 9.01e+21 - 9.01e+21 + 0.01;
print ("第二个值为:", $value, "\n");
```

#### 浮点型

Perl 中的字符串使用一个标量来表示，定义方式和 c 很像，但是在 Perl 里面字符串不是用 \0 来表示结束的。

Perl 双引号和单引号的区别: 双引号可以正常解析一些转义字符与变量，而单引号无法解析会原样输出。

但是用单引号定义可以使用多行文本，如下所示：

```perl
$var='这是一个使用

多行字符串文本

的例子';

print($var);
```

| 转义字符 | 含义                                         |
| :------- | :------------------------------------------- |
| \\       | 反斜线                                       |
| \'       | 单引号                                       |
| \"       | 双引号                                       |
| \a       | 系统响铃                                     |
| \b       | 退格                                         |
| \f       | 换页符                                       |
| \n       | 换行                                         |
| \r       | 回车                                         |
| \t       | 水平制表符                                   |
| \v       | 垂直制表符                                   |
| \0nn     | 创建八进制格式的数字                         |
| \xnn     | 创建十六进制格式的数字                       |
| \cX      | 控制字符，x可以是任何字符                    |
| \u       | 强制下一个字符为大写                         |
| \l       | 强制下一个字符为小写                         |
| \U       | 强制将所有字符转换为大写                     |
| \L       | 强制将所有的字符转换为小写                   |
| \Q       | 将到\E为止的非单词（non-word）字符加上反斜线 |
| \E       | 结束\L、\U、\Q                               |

### 变量

#### Perl变量

变量是存储在内存中的数据，创建一个变量即会在内存上开辟一个空间。

解释器会根据变量的类型来决定其在内存中的存储空间，因此你可以为变量分配不同的数据类型，如整型、浮点型、字符串等。

Perl的三个基本的数据类型：标量、数组、哈希。

- 1. 标量 $ 开始， 如$a $b 是两个标量。

- 2. 数组 @ 开始 ， 如 @a @b 是两个数组。

- 3. 哈希 % 开始 ， %a %b 是两个哈希。

- Perl 为每个变量类型设置了独立的命令空间，所以不同类型的变量可以使用相同的名称，你不用担心会发生冲突。例如 $foo 和 @foo 是两个不同的变量。

#### 创建变量

变量不需要显式声明类型，在变量赋值后，解释器会自动分配匹配的类型空间。

变量使用等号(=)来赋值。

> *我们可以在程序中使用 **use strict** 语句让所有变量需要强制声明类型。*

等号左边为变量，右边为值，实例如下：

```
$age = 25;             # 整型
$name = "Perl";      # 字符串
$salary = 1445.50;     # 浮点数
```

以上代码中 25, "runoob" 和 1445.50 分别赋值给 *$age*, *$name* 和 *$salary* 变量。

接下来我们会看到数组和哈希的使用。

#### 标量变量

标量是一个单一的数据单元。 数据可以是整数，浮点数，字符，字符串，段落等。简单的说它可以是任何东西。以下是标量的简单应用：

```perl
$age = 25;             # 整型
$name = "runoob";      # 字符串
$salary = 1445.50;     # 浮点数
print "Age = $age\n";
print "Name = $name\n";
print "Salary = $salary\n";
```

#### 特殊字符

```perl
print "文件名 ". __FILE__ . "\n";
print "行号 " . __LINE__ ."\n";
print "包名 " . __PACKAGE__ ."\n";
```

#### v 字符串

一个以 v 开头,后面跟着一个或多个用句点分隔的整数,会被当作一个字串文本。

当你想为每个字符 直接声明其数字值时,v-字串提供了一种更清晰的构造这类字串的方法

$smile  = v9786;
$foo    = v102.111.111;
$martin = v77.97.114.116.105.110; 
print "smile = $smile\n";
print "foo = $foo\n";
print "martin = $martin\n";

#### 数组变量

数组是用于存储一个有序的标量值的变量。

数组 @ 开始。

要访问数组的变量，可以使用美元符号($)+变量名，并指定下标来访问，

数组变量以 @ 开头。访问数组元素使用 **$ + 变量名称 + [索引值]** 格式来读取,

实例如下所示：

```perl
@ages = (25, 30, 40);             
@names = ("google", "runoob", "taobao");
print "\$ages[0] = $ages[0]\n";
print "\$ages[1] = $ages[1]\n";
print "\$ages[2] = $ages[2]\n";
print "\$names[0] = $names[0]\n";
print "\$names[1] = $names[1]\n";
print "\$names[2] = $names[2]\n";
print "$sites[-1]\n";    # 负数，反向读取
```

#### 数组序列号

Perl 提供了可以按序列输出的数组形式，格式为 **起始值 + .. + 结束值**

``` perl 
@var_10 = (1..10);
@var_20 = (10..20);
@var_abc = ('a'..'z');
 
print "@var_10\n";   # 输出 1 到 10
print "@var_20\n";   # 输出 10 到 20
print "@var_abc\n";  # 输出 a 到 z
```

#### 数组大小

数组大小由数组中的标量上下文决定

```perl
@array = (1,2,3);
print "数组大小1: ",scalar @array,"\n";
$size=@array;
print "数组大小2:  $size\n";
$max_index = $#array;
print "最大索引: $max_index\n";
```

| 序号 | 类型和描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | **push @ARRAY, LIST**将列表的值放到数组的末尾                |
| 2    | **pop @ARRAY**删除数组的最后一个值                           |
| 3    | **shift @ARRAY**弹出数组第一个值，并返回它。数组的索引值也依次减一。 |
| 4    | **unshift @ARRAY, LIST**将列表放在数组前面，并返回新数组的元素个数。 |

#### 切割数组

我们可以切割一个数组，并返回切割后的新数组：

```perl
@sites = qw/google taobao runoob weibo qq facebook 网易/;
@sites2 = @sites[3,4,5];
print "@sites2\n";
```

#### 替换数组元素

Perl 中数组元素替换使用 splice() 函数，语法格式如下：

```
splice @ARRAY, OFFSET [ , LENGTH [ , LIST ] ]
```

参数说明：

1. @ARRAY：要替换的数组。
2. OFFSET：起始位置。
3. LENGTH：替换的元素个数。
4. LIST：替换元素列表。

```perl
@nums = (1..20);
print "替换前 - @nums\n";
splice(@nums, 5, 5, 21..25); 
print "替换后 - @nums\n";
```

## 将字符串转换为数组

Perl 中将字符串转换为数组使用 split() 函数，语法格式如下：

```
split [ PATTERN [ , EXPR [ , LIMIT ] ] ]
```

参数说明：

1. PATTERN：分隔符，默认为空格。
2. EXPR：指定字符串数。
3. LIMIT：如果指定该参数，则返回该数组的元素个数。

```perl
# 定义字符串
$var_test = "runoob";
$var_string = "www-runoob-com";
$var_names = "google,taobao,runoob,weibo";
 
# 字符串转为数组
@test = split('', $var_test);
@string = split('-', $var_string);
@names  = split(',', $var_names);
 
print "$test[3]\n";  # 输出 o
print "$string[2]\n";  # 输出 com
print "$names[3]\n";   # 输出 weibo
```

#### 将数组转换为字符串

Perl 中将数组转换为字符串使用 join() 函数，语法格式如下：

```
join EXPR, LIST
```

参数说明：

1. EXPR：连接符。
2. LIST：列表或数组。

```perl
# 定义字符串
$var_string = "www-runoob-com";
$var_names = "google,taobao,runoob,weibo";
# 字符串转为数组
@string = split('-', $var_string);
@names  = split(',', $var_names);
# 数组转为字符串
$string1 = join( '-', @string );
$string2 = join( ',', @names );
print "$string1\n";
print "$string2\n";
```

#### 数组排序

Perl 中数组排序使用 sort() 函数，语法格式如下：

```
sort [ SUBROUTINE ] LIST
```

参数说明：

- SUBROUTINE：指定规则。
- LIST：列表或数组。

```perl
# 定义数组
@sites = qw(google taobao baidu facebook);
print "排序前: @sites\n";
# 对数组进行排序
@sites = sort(@sites);
print "排序后: @sites\n";
```

#### 特殊变量： $[

特殊变量 **$[** 表示数组的第一索引值，一般都为 0 ，如果我们将 **$[** 设置为 1，则数组的第一个索引值即为 1，第二个为 2，以此类推。实例如下：

```perl
# 定义数组
@sites = qw(google taobao baidu facebook);
print "网站: @sites\n";
# 设置数组的第一个索引为 1
$[ = 1;
print "\@sites[1]: $sites[1]\n";
print "\@sites[2]: $sites[2]\n";
```

#### 合并数组

数组的元素是以逗号来分割，我们也可以使用逗号来合并数组

```perl
@numbers = (1,3,(4,5,6));
print "numbers = @numbers\n";
```

#### 从列表中选择元素

一个列表可以当作一个数组使用，在列表后指定索引值可以读取指定的元素

```perl
$var = (5,4,3,2,1)[4];
print "var 的值为 = $var\n"
```

#### 哈希变量

哈希是一个 **key/value** 对的集合。

哈希 % 开始。

如果要访问哈希值，可以使用 **$ + {key}** 格式来访问：

```perl
%data = ('google', 45, 'baidu', 30, 'taobao', 40);
print "\$data{'google'} = $data{'google'}\n";
print "\$data{'baidu'} = $data{'baidu'}\n";
print "\$data{'taobao'} = $data{'taobao'}\n";
```

也可以使用 **=>** 符号来设置 key/value:

```perl
%data = ('google'=>'google.com', 'baidu'=>'baidu.com','taobao'=>'taobao.com');
```

以下实例是上面实例的变种，使用 **-** 来代替引号：

```perl
%data = (-google=>'google.com', -baidu=>'baidu.com', -taobao=>'taobao.com');
```

**读取所有key**

我们可以使用 **keys** 函数读取哈希所有的键，语法格式如下：

```
keys %HASH
```

该函数返回所有哈希的所有 key 的数组。

```perl 
\#!/usr/bin/perl   
%data = ('google'=>'google.com', 'baidu'=>'baidu.com','taobao'=>'taobao.com'); 
@names = keys %data;  
print "$names[0]\n"; 
print "$names[1]\n"; 
print "$names[2]\n";
```

**读取value**

```perl
%data = ('google'=>'google.com', 'baidu'=>'baidu.com', 'taobao'=>'taobao.com');
@urls = values %data;
print "$urls[0]\n";
print "$urls[1]\n";
print "$urls[2]\n";
```

#### 检测元素是否存在

如果你在哈希中读取不存在的 key/value 对 ，会返回 **undefined** 值，且在执行时会有警告提醒。

为了避免这种情况，我们可以使用 **exists** 函数来判断key是否存在，存在的时候读取：

``` perl
%data = ('google'=>'google.com', 'baidu'=>'baidu.com', 'taobao'=>'taobao.com');
 
if( exists($data{'facebook'} ) ){
   print "facebook 的网址为 $data{'facebook'} \n";
}
else
{
   print "facebook 键不存在\n";
}
```

#### 获取哈希大小

哈希大小为元素的个数，我们可以通过先获取 key 或 value 的所有元素数组，再计算数组元素多少来获取哈希的大小，实例如下：

```perl
%data = ('google'=>'google.com', 'baidu'=>'baidu.com', 'taobao'=>'taobao.com');
@keys = keys %data;
$size = @keys;
print "1 - 哈希大小: $size\n";
@values = values %data;
$size = @values;
print "2 - 哈希大小: $size\n";
```

#### 哈希中添加或删除元素

添加 key/value 对可以通过简单的赋值来完成。但是删除哈希元素你需要使用 **delete** 函数：

```perl
%data = ('google'=>'google.com', 'runoob'=>'runoob.com', 'taobao'=>'taobao.com');
@keys = keys %data;
$size = @keys;
print "1 - 哈希大小: $size\n";
# 添加元素
$data{'facebook'} = 'facebook.com';
@keys = keys %data;
$size = @keys;
print "2 - 哈希大小: $size\n";
# 删除哈希中的元素
delete $data{'taobao'};
@keys = keys %data;
$size = @keys;
print "3 - 哈希大小: $size\n";
```

#### 迭代哈希

我们可以使用 foreach 和 while 来迭代哈希：

**使用 foreach**

```perl
%data = ('google'=>'google.com', 'baidu'=>'baidu.com', 'taobao'=>'taobao.com');
foreach $key (keys %data){
    print "$data{$key}\n";
}
```

**使用 while**

```perl
%data = ('google'=>'google.com', 'baidu'=>'baidu.com', 'taobao'=>'taobao.com');
while(($key, $value) = each(%data)){
    print "$data{$key}\n";
}
```

#### 变量上下文

所谓上下文：指的是表达式所在的位置。

上下文是由等号左边的变量类型决定的，等号左边是标量，则是标量上下文，等号左边是列表，则是列表上下文。

Perl 解释器会根据上下文来决定变量的类型。实例如下：

```perl
@names = ('google', 'baidu', 'taobao');
@copy = @names;   # 复制数组
$size = @names;   # 数组赋值给标量，返回数组元素个数
print "名字为 : @copy\n";
print "名字数为 : $size\n";
```

