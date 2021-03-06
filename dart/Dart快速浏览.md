# 变量

## 变量定义

以下代码是Dart中定义变量的方法：



```dart
main() {
  var a = 1;
  int b = 10;
  String s = "hello";
  dynamic c = 0.5;
}
```

你可以明确指定某个变量的类型，如int bool String，也可以用var或 dynamic来声明一个变量，Dart会自动推断其数据类型。

### 变量的默认值

注意：没有赋初值的变量都会有默认值null

### final和const

如果你绝不想改变一个变量，使用final或const，不要使用var或其他类型，一个被final修饰的变量只能被赋值一次，一个被const修饰的变量是一个编译时常量（const常量毫无疑问也是final常量）。可以这么理解：final修饰的变量是不可改变的，而const修饰的表示一个常量。

*注意：实例变量可以是final的但不能是const的*

下面用代码说明：



```swift
var count = 10; 
final Num = count;  // final 只能赋值一次
const Num1 = 10; // const赋值必须是编译时常量
```

#### final和const的区别：

区别一：final 要求变量只能初始化一次，并不要求赋的值一定是编译时常量，可以是常量也可以不是。而 const 要求在声明时初始化，并且赋值必需为编译时常量。

区别二：final 是惰性初始化，即在运行时第一次使用前才初始化。而 const 是在编译时就确定值了。

# 内建数据类型

Dart有如下几种内建的数据类型：

- numbers
- strings
- booleans
- lists(或者是arrays)
- maps
- runes（UTF-32字符集的字符）
- symbols
   下面用一段代码来演示以上各类数据类型：



```dart
main() {
  // numbers
  var a = 0;
  int b = 1;
  double c = 0.1;

  // strings
  var s1 = 'hello';
  String s2 = "world";

  // booleans
  var real = true;
  bool isReal = false;

  // lists
  var arr = [1, 2, 3, 4, 5];
  List<String> arr2 = ['hello', 'world', "123", "456"];
  List<dynamic> arr3 = [1, true, 'haha', 1.0];

  // maps
  var map = new Map();
  map['name'] = 'zhangsan';
  map['age'] = 10;
  Map m = new Map();
  m['a'] = 'a';

  //runes，Dart 中 使用runes 来获取UTF-32字符集的字符。String的 codeUnitAt and codeUnit属性可以获取UTF-16字符集的字符
  var clapping = '\u{1f44f}';
  print(clapping); // 打印的是拍手emoji的表情

  // symbols
  print(#s == new Symbol("s")); // true
}
```

# 函数

### 函数的返回值

Dart是一个面向对象的编程语言，所以即使是函数也是一个对象，也有一种类型Function，这就意味着函数可以赋值给某个变量或者作为参数传给另外的函数。虽然Dart推荐你给函数加上返回值，但是不加返回值的函数同样可以正常工作，另外你还可以用=>代替return语句，比如下面的代码：



```dart
// 声明返回值
int add(int a, int b) {
  return a + b;
}

// 不声明返回值
add2(int a, int b) {
  return a + b;
}

// =>是return语句的简写
add3(a, b) => a + b; 

main() {
  print(add(1, 2)); // 3
  print(add2(2, 3)); // 5
  print(add3(1, 2)); // 3
}
```

### 命名参数、位置参数、参数默认值

#### 命名参数



```dart
sayHello({String name}) {
  print("hello, my name is $name");
}

sayHello2({name: String}) {
  print("hello, my name is $name");
}

main() {
  // 打印 hello, my name is zhangsan
  sayHello(name: 'zhangsan');

  // 打印 hello, my name is wangwu
  sayHello2(name: 'wangwu');
}
```

可以看到，定义命名参数时，你可以以 `{type paramName}` 或者 `{paramName: type}` 两种方式声明参数，而调用命名参数时，需要以 `funcName(paramName: paramValue)` 的形式调用。

命名参数的参数并不是必须的，所以上面的代码中，如果调用sayHello()不带任何参数，也是可以的，只不过最后打印出来的结果是：hello, my name is null，在Flutter开发中，你可以使用@required注解来标识一个命名参数，这代表该参数是必须的，你不传则会报错，比如下面的代码：



```dart
const Scrollbar({Key key, @required Widget child})
```

#### 可变参数

使用中括号[]括起来的参数是函数的可变参数，代表该参数可传可不传，可变参数只能放在函数的参数列表的最后面，如下代码所示：



```dart
sayHello(String name, int age, [String hobby]) { // 可变参数可以有多个，比如[String a, int b]
  StringBuffer sb = new StringBuffer();
  sb.write("hello, this is $name and I am $age years old");
  if (hobby != null) {
    sb.write(", my hobby is $hobby");
  }
  print(sb.toString());
}

main() {
  // hello, this is zhangsan and I am 20 years old
  sayHello("zhangsan", 20);
  // hello, this is zhangsan and I am 20 years old, my hobby is play football
  sayHello("zhangsan", 20, "play football");
}
```

#### 参数默认值

你可以为命名参数或者位置参数设置默认值，如下代码所示：



```cpp
// 命名参数的默认值
int add({int a, int b = 3}) { // 不能写成：int add({a: int, b: int = 3})
  return a + b;
}

// 可变参数的默认值
int sum(int a, int b, [int c = 3]) {
  return a + b + c;
}
```

#### main()函数

不论在Dart还是Flutter中，必须都需要一个顶层的main()函数，它是整个应用的入口函数，main()函数的返回值是void，还有一个可选的参数，参数类型是List<String>。

#### 函数作为一类对象

你可以将一个函数作为参数传给另一个函数，比如下面的代码：



```dart
printNum(int a) {
  print("$a");
}

main() {
  //  依次打印：
  //  1
  //  2
  //  3
  var arr = [1, 2, 3];
  arr.forEach(printNum);
}
```

你也可以将一个函数赋值给某个变量，比如下面的代码：



```dart
printNum(int a) {
  print("$a");
}

main() {
  var f1 = printNum;
  Function f2 = printNum;
  var f3 = (int a) => print("a = $a");
  f1(1);
  f2(2);
  f3(6);
}
```

#### 匿名函数 = lambda表达式

大多数函数都是有名称的，比如main() printName()等，但是你也可以写匿名函数，如果你对Java比较熟悉，那下面的Dart代码你肯定也不会陌生：



```php
test(Function callback) {
  callback("hello");
}

main() {
  test((param) {
    // 打印hello
    print(param);
  });
}
```

匿名函数类似于Java中的接口，往往在某个函数的参数为函数时使用到。

#### 函数返回值

所有的函数都有返回值，如果没有指定return语句，那么该函数的返回值为null。

# 运算符

Dart中的运算符与Java中的类似，比如++a a == b b ? a : b，但是也有一些与Java不太一样的运算符，下面用代码说明：



```dart
main() {
  // 与Java相同的运算符操作

  int a = 1;
  ++a;
  a++;
  var b = 1;
  print(a == b);  // false
  print(a * b); // 3
  bool real = false;
  real ? print('real') : print('not real'); // not real
  print(real && a == b); // false
  print(real || a == 3); // true
  print(a != 2); // true
  print(a <= b); // false
  var c = 9;
  c += 10;
  print("c = $c"); // c = 19
  print(1<<2); // 4

  // 与Java不太一样的运算符操作

  // is运算符用于判断一个变量是不是某个类型的数据
  // is!则是判断变量不是某个类型的数据
  var s = "hello";
  print(s is String); // true
  var num = 6;
  print(num is! String); // true

  // ~/才是取整运算符，如果使用/则是除法运算，不取整
  int k = 1;
  int j = 2;
  print(k / j); // 0.5
  print(k ~/ j); // 0

  // as运算符类似于Java中的cast操作，将一个对象强制类型转换
  (emp as Person).teach();

  // ??=运算符 如果 ??= 运算符前面的变量为null，则赋值，否则不赋值
  var param1 = "hello", param2 = null;
  param1 ??= "world";
  param2 ??= "world";
  print("param1 = $param1"); // param1 = hello
  print("param2 = $param2"); // param2 = world
  
  // ?.运算符
  var str1 = "hello world";
  var str2 = null;
  print(str1?.length); // 11
  print(str2?.length); // null 
  print(str2.length); // 报错
}
```

### ..运算符（级联操作）

如果你对Java中的建造者模式比较熟悉的话，Dart中的..运算符也很好理解，先看下面的代码：



```dart
class Person {
  eat() {
    print("I am eating...");
  }

  sleep() {
    print("I am sleeping...");
  }

  study() {
    print("I am studying...");
  }
}

main() {
  // 依次打印
  //  I am eating...
  //  I am sleeping...
  //  I am studying...
  new Person()..eat()
      ..sleep()
      ..study();
}
```

可以看到，使用..调用某个对象的方法（或者成员变量）时，返回值是这个对象本身，所以你可以接着使用..调用这个对象的其他方法，这不就类似于Java中的建造者模式，每次build某个属性时，都返回一个this对象吗。

### 控制流程

if / else switch for /while try / catch语句跟Java中都类似，try / catch语句可能稍有不同，下面用一段代码说明：



```dart
main() {
  // if else语句
  int score = 80;
  if (score < 60) {
    print("so bad!");
  } else if (score >= 60 && score < 80) {
    print("just so so!");
  } else if (score >= 80) {
    print("good job!");
  }

  // switch语句
  String a = "hello";
  // case语句中的数据类型必须是跟switch中的类型一致
  switch (a) {
    case "hello":
      print("haha");
      break;
    case "world":
      print("heihei");
      break;
    default:
      print("WTF");
  }

  // for语句
  List<String> list = ["a", "b", "c"];
  for (int i = 0; i < list.length; i++) {
    print(list[i]);
  }
  for (var i in list) {
    print(i);
  }
  // 这里的箭头函数参数必须用圆括号扩起来
  list.forEach((item) => print(item));

  // while语句
  int start = 1;
  int sum = 0;
  while (start <= 100) {
    sum += start;
    start++;
  }
  print(sum);

  // try catch语句
  try {
    print(1 ~/ 0);
  } catch (e) {
    // IntegerDivisionByZeroException
    print(e);
  }
  try {
    1 ~/ 0;
  } on IntegerDivisionByZeroException { // 捕获指定类型的异常
    print("error"); // 打印出error
  } finally {
    print("over"); // 打印出over
  }
}
```

# 类（Class）

### 类的定义与构造方法

Dart中的类没有访问控制，所以你不需要用private, protected, public等修饰成员变量或成员函数，一个简单的类如下代码所示：



```dart
class Person {
  String name;
  int age;
  String gender;
  Person(this.name, this.age, this.gender);
  sayHello() {
    print("hello, this is $name, I am $age years old, I am a $gender");
  }
}
```

上面的Person类中有3个成员变量，一个构造方法和一个成员方法，看起来比较奇怪的是Person的构造方法，里面传入的3个参数都是this.xxx，而且没有大括号{}包裹的方法体，这种语法是Dart比较独特而简洁的构造方法声明方式，它等同于下面的代码：



```dart
Person(String name, int age, String gender) {
    this.name = name;
    this.age = age;
    this.gender = gender;
}
```

要调用Person类的成员变量或成员方法，可以用下面的代码：



```csharp
  var p = new Person("zhangsan", 20, "male");
  p.sayHello(); // hello, this is zhangsan, I am 20 years old, I am a male
  p.age = 50;
  p.gender = "female";
  p.sayHello(); // hello, this is zhangsan, I am 50 years old, I am a female
```

类除了有跟类名相同的构造方法外，还可以添加命名的构造方法，如下代码所示：



```dart
class Point {
  num x, y;
  Point(this.x, this.y);
  // 类的命名构造方法
  Point.origin() {
    x = 0;
    y = 0;
  }
}

main() {
  // 调用Point类的命名构造方法origin()
  var p = new Point.origin();
  var p2 = new Point(1, 2);
}
```

Dart中使用extends关键字做类的继承，如果一个类只有命名的构造方法，在继承时需要注意，如下代码：



```dart
class Human {
  String name;
  Human.fromJson(Map data) {
    print("Human's fromJson constructor");
  }
}

class Man extends Human {
  Man.fromJson(Map data) : super.fromJson(data) {
    print("Man's fromJson constructor");
  }
}
```

由于Human类没有默认构造方法，只有一个命名构造方法fromJson，所以在Man类继承Human类时，需要调用父类的fromJson方法做初始化，而且必须使用Man.fromJson(Map data) : super.fromJson(data)这种写法，而不是像Java那样将super写到花括号中。

有时候你仅仅只是在某个类的构造方法中，调用这个类的另一个构造方法，你可以这么写：



```kotlin
class Point {
  num x, y;
  Point(this.x, this.y);
  // 命名构造方法调用了默认的构造方法
  Point.alongXAxis(num x) : this(x, 0);
}
```

### 类的成员方法

一个类的成员方法是一个函数，为这个类提供某些行为。上面的代码中已经有了一些类的成员方法的定义，这些定义方式跟Java很类似，你可以为某个类的成员变量提供getter/setter方法，如下代码：



```dart
class Rectangle {
  num left, top, width, height;

  // 构造方法传入left, top, width, height几个参数
  Rectangle(this.left, this.top, this.width, this.height);

  // right, bottom两个成员变量提供getter/setter方法
  num get right => left + width;
  set right(num value) => left = value - width;
  num get bottom => top + height;
  set bottom(num value) => top = value - height;
}
```

### 抽象类和抽象方法

使用abstract修饰一个类，则这个类是抽象类，抽象类中可以有抽象方法和非抽象方法，抽象方法没有方法体，需要子类去实现，如下代码：



```java
abstract class Doer {
  // 抽象方法，没有方法体，需要子类去实现
  void doSomething();
  // 普通的方法
  void greet() {
    print("hello world!");
  }
}

class EffectiveDoer extends Doer {
  // 实现了父类的抽象方法
  void doSomething() {
    print("I'm doing something...");
  }
}
```

### 运算符重载

Dart中有类似于C++中的运算符重载语法，比如下面的代码定义了一个向量类，重载了向量的+ -运算：



```dart
class Vector {
  num x, y;
  Vector(this.x, this.y);
  Vector operator +(Vector v) => new Vector(x + v.x, y + v.y);
  Vector operator -(Vector v) => new Vector(x - v.x, y - v.y);
  printVec() {
    print("x: $x, y: $y");
  }
}

main() {
  Vector v1 = new Vector(1, 2);
  Vector v2 = new Vector(3, 4);
  (v1 - v2).printVec(); // -2, -2
  (v1 + v2).printVec(); // 4, 6
}
```

### 枚举类

使用enum关键字定义一个枚举类，这个语法跟Java类似，如下代码：



```rust
enum Color { red, green, blue }
```

### mixins

mixins是一个重复使用类中代码的方式，比如下面的代码：



```swift
class A {
  a() {
    print("A's a()");
  }
}

class B {
  b() {
    print("B's b()");
  }
}

// 使用with关键字，表示类C是由类A和类B混合而构成
class C = A with B;

main() {
  C c = new C();
  c.a(); // A's a()
  c.b(); // B's b()
}
```

### 静态成员变量和静态成员方法



```dart
// 类的静态成员变量和静态成员方法
class Cons {
  static const name = "zhangsan";
  static sayHello() {
    print("hello, this is ${Cons.name}");
  }
}

main() {
  Cons.sayHello(); // hello, this is zhangsan
  print(Cons.name); // zhangsan
}
```

# 泛型（Generics）

Java和C++语言都有泛型，Dart语言也不例外，使用泛型有很多好处，比如：

正确指定泛型类型会产生更好的生成代码。
 泛型可以减小代码的复杂度

Dart内置的数据类型List就是一个泛型数据类型，你可以往List中塞任何你想的数据类型比如整型、字符串、布尔值等
 关于Dart更多的泛型知识点，可以查看这里。

# Dart库（Libraries）

Dart目前已经有很多的库提供给开发者，许多功能不需要开发者自己去实现，只需要导入对应的包即可，使用import语句来导入某个包，比如下面的代码：



```dart
import 'dart:html';
```

如果你想导入自己写的某个代码文件，使用相对路径即可，例如当前有一个demo.dart文件，跟该文件同级目录下有个util.dart文件，文件代码如下：



```cpp
// util.dart文件内容

int add(int a, int b) {
  return a + b;
}
```

在demo.dart文件中如果要引用util.dart文件，使用下面的方式导入：



```dart
// demo.dart

import './util.dart';

main() {
  print(add(1, 2));
}
```

你可以使用as关键字为导入的某个包设置一个前缀，或者说别名，比如下面的代码：



```dart
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

// Uses Element from lib1.
Element element1 = Element();

// Uses Element from lib2.
lib2.Element element2 = lib2.Element();
```

你也可以在导入包时使用show hide关键字来导入某个包中的部分功能，比如下面的代码：



```dart
// 只导入foo
import 'package:lib1/lib1.dart' show foo;

// 导入除了foo的所有其他部分
import 'package:lib2/lib2.dart' hide foo;
```

导入包时使用deferred as可以让这个包懒加载，懒加载的包只会在该包被使用时得到加载，而不是一开始就加载，比如下面的代码：



```dart
import 'package:greetings/hello.dart' deferred as hello;
```

# 异步

Dart提供了类似ES7中的async await等异步操作，这种异步操作在Flutter开发中会经常遇到，比如网络或其他IO操作，文件选择等都需要用到异步的知识。
 async和await往往是成对出现的，如果一个方法中有耗时的操作，你需要将这个方法设置成async，并给其中的耗时操作加上await关键字，如果这个方法有返回值，你需要将返回值塞到Future中并返回，如下代码所示：



```csharp
Future checkVersion() async {
  var version = await lookUpVersion();
  // Do something with version
}
```

下面的代码使用Dart从网络获取数据并打印出来：



```dart
import 'dart:async';
import 'package:http/http.dart' as http;

Future<String> getNetData() async{
  http.Response res = await http.get("http://www.baidu.com");
  return res.body;
}

main() {
  getNetData().then((str) {
    print(str);
  });
}
```

