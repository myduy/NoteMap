# 子函数（程序）

Perl 子程序也就是用户定义的函数。
Perl 子程序即执行一个特殊任务的一段分离的代码，它可以使减少重复代码且使程序易读。Perl 子程序可以出现在程序的任何地方，语法格式如下：

示例：

```perl
sub subroutine{
statements;
}
```

#### 调用子程序语法格式：

```perl
subroutine( 参数列表 );
```

#### 在 Perl 5.0 以下版本调用子程序方法如下：

```perl
&subroutine( 参数列表 );
```

#### 向子程序传递参数

Perl 子程序可以和其他编程一样接受多个参数，子程序参数使用特殊数组 @_ 标明。

因此子程序第一个参数为 $_[0], 第二个参数为 $_[1], 以此类推。

不论参数是标量型还是数组型的，用户把参数传给子程序时，perl默认按引用的方式调用它们。

```perl
# 定义求平均值函数
sub Average{
   # 获取所有传入的参数
   $n = scalar(@_);
   $sum = 0;
 
   foreach $item (@_){
      $sum += $item;
   }
   $average = $sum / $n;
   print '传入的参数为 : ',"@_\n";           # 打印整个数组
   print "第一个参数值为 : $_[0]\n";         # 打印第一个参数
   print "传入参数的平均值为 : $average\n";  # 打印平均值
}
 
# 调用函数
Average(10, 20, 30);
```

#### 向子程序传递列表

由于 @_ 变量是一个数组，所以它可以向子程序中传递列表。

但如果我们需要传入标量和数组参数时，需要把列表放在最后一个参数上，程序将标量和数组合并。如下所示：

```perl
# 定义函数
sub PrintList{
   my @list = @_;
   print "列表为 : @list\n";
}
$a = 10;
@b = (1, 2, 3, 4);
 
# 列表参数
PrintList($a, @b);
```

#### 向子程序传递哈希

当向子程序传递哈希表时，它将复制到 @_ 中，哈希表将被展开为键/值组合的列表。

```perl
# 方法定义
sub PrintHash{
   my (%hash) = @_;
 
   foreach my $key ( keys %hash ){
      my $value = $hash{$key};
      print "$key : $value\n";
   }
}
%hash = ('name' => 'Mack', 'age' => 3);
 
# 传递哈希
PrintHash(%hash);
```



#### 子程序返回值

子程序可以向其他编程语言一样使用 return 语句来返回函数值。

如果没有使用 return 语句，则子程序的**最后一行**语句将作为返回值。

```perl
# 方法定义
sub add_a_b{
   # 不使用 return
   $_[0]+$_[1];  

   # 使用 return
   # return $_[0]+$_[1];  
}
print add_a_b(1, 2)
```

```perl
sub somefunc {
   my $variable; # $variable 在方法 somefunc() 外不可见
   my ($another, @an_array, %a_hash); #  同时声明多个变量
}
```

#### 变量的临时赋值

```perl
# 全局变量
$string = "Hello, World!";
 
sub PrintRunoob{
   # PrintHello 函数私有变量
   local $string;
   $string = "Hello, Runoob!";
   # 子程序调用的子程序
   PrintMe();
   print "PrintRunoob 函数内字符串值：$string\n";
}
sub PrintMe{
   print "PrintMe 函数内字符串值：$string\n";
}
 
sub PrintHello{
   print "PrintHello 函数内字符串值：$string\n";
}
 
# 函数调用
PrintRunoob();
PrintHello();
print "函数外部字符串值：$string\n";
```

#### 静态变量

state操作符功能类似于C里面的static修饰符，state关键字将局部变量变得持久。

state也是词法变量，所以只在定义该变量的词法作用域中有效，举个例子：

```perl
use feature 'state';
 
sub PrintCount{
   state $count = 0; # 初始化变量
 
   print "counter 值为：$count\n";
   $count++;
}
 
for (1..5){
   PrintCount();
}
```

#### 子程序调用上下文

子程序调用过程中，会根据上下文来返回不同类型的值，比如以下 localtime() 子程序，在标量上下文返回字符串，在列表上下文返回列表:

```perl
#!/usr/bin/perl
 
# 标量上下文
my $datestring = localtime( time );
print $datestring;
 
print "\n";
 
# 列表上下文
($sec,$min,$hour,$mday,$mon, $year,$wday,$yday,$isdst) = localtime(time);
printf("%d-%d-%d %d:%d:%d",$year+1990,$mon+1,$mday,$hour,$min,$sec);
 
print "\n";
```
