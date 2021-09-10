```dart
import 'dart:io';

class Person{
  
  static String name = '张三';
  int age = 18;
  
  static printInfo(){
    //不能通过this关键字,访问静态方法
    // print(this.name);
    print(name);
    // 静态方法不能访问非静态方法
    // print(age);
    // 静态方法，不能直接访问非静态方法
    // printUserInfo(); 
    
  }
  
  printUserInfo(){
    //非静态方法，可以访问静态属性
    print(name);
    print(age);
    printInfo();
  }
}


void main(){
  
  print(Person.name);
  print(Person.printInfo());
  // 不能通过类名称，直接访问非静态方法
  // print(Person.printUserInfo());
  
  var p = new Person();
  // 不能访问静态属性
  // print(p.name);
  print(p.printUserInfo());
  
}
```