# 循环

#### 循环

| 循环类型                                                     | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [while 循环](https://www.runoob.com/perl/perl-while-loop.html) | 当给定条件为 true 时，重复执行语句或语句组。循环主体执行之前会先测试条件。 |
| [until 循环](https://www.runoob.com/perl/perl-until-loop.html) | 重复执行语句或语句组，直到给定的条件为 true。 循环主体执行之前会先测试条件。 |
| [for 循环](https://www.runoob.com/perl/perl-for-loop.html)   | 多次执行一个语句序列，简化管理循环变量的代码。               |
| [foreach 循环](https://www.runoob.com/perl/perl-foreach-loop.html) | foreach 循环用于迭代一个列表或集合变量的值。                 |
| [do...while 循环](https://www.runoob.com/perl/perl-do-while-loop.html) | 除了它是在循环主体结尾测试条件外，其他与 while 语句类似。    |
| [嵌套循环](https://www.runoob.com/perl/perl-nested-loops.html) | 您可以在 while、for 或 do..while 循环内使用一个或多个循环。  |

#### 循环控制语句

| 控制语句                                                     | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [next 语句](https://www.runoob.com/perl/perl-next-statement.html) | 停止执行从next语句的下一语句开始到循环体结束标识符之间的语句，转去执行continue语句块，然后再返回到循环体的起始处开始执行下一次循环。 |
| [last 语句](https://www.runoob.com/perl/perl-last-statement.html) | 退出循环语句块，从而结束循环                                 |
| [continue 语句](https://www.runoob.com/perl/perl-continue-statement.html) | continue 语句块通常在条件语句再次判断前执行。                |
| [redo 语句](https://www.runoob.com/perl/perl-redo-statement.html) | redo 语句直接转到循环体的第一行开始重复执行本次循环，redo语句之后的语句不再执行，continue语句块也不再执行； |
| [goto 语句](https://www.runoob.com/perl/perl-goto-statement.html) | Perl 有三种 goto 形式：got LABLE，goto EXPR，和 goto &NAME。 |

#### 无限循环

```perl
for( ; ; )
{
   printf "循环会无限执行。\n";
}
```

