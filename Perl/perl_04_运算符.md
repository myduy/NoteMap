# 运算符

#### 算术运算符

| 运算符 | 描述                   | 实例（变量 $a 为 10， $b 为 20。） |
| :----- | :--------------------- | :--------------------------------- |
| +      | 加法运算               | $a + $b 结果为 30                  |
| -      | 减法运算               | $a - $b 结果为 -10                 |
| *      | 乘法运算               | $a * $b 结果为 200                 |
| /      | 除法运算               | $b / $a 结果为 2                   |
| %      | 求余运算，整除后的余数 | $b % $a 结果为 0                   |
| **     | 乘幂                   | $a**$b 结果为 10 的 20 次方        |

#### 比较运算符

| 运算符 | 描述                                                         | 实例（变量 $a 为 10， $b 为 20。） |
| :----- | :----------------------------------------------------------- | :--------------------------------- |
| ==     | 检查两个操作数的值是否相等，如果相等则条件为 true，否则为 false。 | ($a == $b) 为 false                |
| !=     | 检查两个操作数的值是否相等，如果不相等则条件为 true，否则为 false。 | ($a != $b) 为 true。               |
| <=>    | 检查两个操作数的值是否相等, 如果左边的数小于右边的数返回 -1，如果相等返回 0, 如果左边的数大于右边的数返回 1 。 | ($a <=> $b) 返回 -1。              |
| >      | 检查左操作数的值是否大于右操作数的值，如果是则条件为 true，否则为 false。 | ($a > $b) 返回 false。             |
| <      | 检查左操作数的值是否小于右操作数的值，如果是则条件为 true，否则返回 false。 | ($a < $b) 返回 true。              |
| >=     | 检查左操作数的值是否大于或等于右操作数的值，如果是则条件为 true，否则返回 false。 | ($a >= $b) 返回 false。            |
| <=     | 检查左操作数的值是否小于或等于右操作数的值，如果是则条件为 true，否则返回 false。。 | ($a <= $b) 返回 true。             |

| 运算符 | 描述                                                         | 实例变量 （$a 为 "abc" ， $b 为 "xyz"） |
| :----- | :----------------------------------------------------------- | :-------------------------------------- |
| lt     | 检查左边的字符串是否小于右边的字符串，如果是返回 true，否则返回 false。 | ($a lt $b) 返回 true。                  |
| gt     | 检查左边的字符串是否大于右边的字符串，如果是返回 true，否则返回 false。 | ($a gt $b) 返回 false。                 |
| le     | 检查左边的字符串是否小于或等于右边的字符串，如果是返回 true，否则返回 false。 | ($a le $b) 返回 true                    |
| ge     | 检查左边的字符串是否大于或等于右边的字符串，如果是返回 true，否则返回 false。 | ($a ge $b) 返回 false。                 |
| eq     | 检查左边的字符串是否等于右边的字符串，如果是返回 true，否则返回 false。 | ($a eq $b) 返回 false。                 |
| ne     | 检查左边的字符串是否不等于右边的字符串，如果是返回 true，否则返回 false。 | ($a ne $b) 返回 true                    |
| cmp    | 如果左边的字符串大于右边的字符串返回 1，如果相等返回 0，如果左边的字符串小于右边的字符串返回 -1。 | ($a cmp $b) 返回 -1。                   |

#### 赋值运算符

| 运算符 | 描述                                                         | 实例（变量 $a 为 10， $b 为 20）      |
| :----- | :----------------------------------------------------------- | :------------------------------------ |
| =      | 简单的赋值运算符，把右边操作数的值赋给左边操作数             | $c = $a + $b 将把 $a + $b 的值赋给 $c |
| +=     | 加且赋值运算符，把右边操作数加上左边操作数的结果赋值给左边操作数 | $c += $a 相等于 $c = $c + $a          |
| -=     | 减且赋值运算符，把左边操作数减去右边操作数的结果赋值给左边操作数 | $c -= $a 相等于 $c = $c - $a          |
| *=     | 乘且赋值运算符，把右边操作数乘以左边操作数的结果赋值给左边操作数 | $c *= $a 相等于 $c = $c * $a          |
| /=     | 除且赋值运算符，把左边操作数除以右边操作数的结果赋值给左边操作数 | $c /= $a 相等于 $c = $c / $a          |
| %=     | 求模且赋值运算符，求两个操作数的模赋值给左边操作数           | $c %= $a 相等于 $c = $c % a           |
| **=    | 乘幂且赋值运算符，求两个操作数的乘幂赋值给左边操作数         | $c **= $a 相等于 $c = $c ** $a        |

#### 位运算符

| 运算符 | 描述                                                         | 实例（$a = 0011 1100  $b = 0000 1101）                       |
| :----- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| &      | 如果同时存在于两个操作数中，二进制 AND 运算符复制一位到结果中。 | ($a & $b) 将得到 12，二进制为 0000 1100                      |
| \|     | 如果存在于任一操作数中，二进制 OR 运算符复制一位到结果中。   | ($a \| $b) 将得到 61 ，二进制为 0011 1101                    |
| ^      | 如果存在于其中一个操作数中但不同时存在于两个操作数中，二进制异或运算符复制一位到结果中。 | ($a ^ $b) 将得到 49，二进制为 0011 0001                      |
| ~      | 二进制反码运算符是一元运算符，具有"翻转"位效果，即0变成1，1变成0。 | (~$a ) 将得到 -61 ，二进制为 1100 0011 ，一个有符号二进制数的反码形式。 |
| <<     | 二进制左移运算符。左操作数的值向左移动右操作数指定的位数。   | $a << 2 将得到 240 ，二进制为 1111 0000                      |
| >>     | 二进制右移运算符。左操作数的值向右移动右操作数指定的位数。   | $a >> 2 将得到 15 ，二进制为 0000 1111                       |

