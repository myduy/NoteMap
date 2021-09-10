```dart
class Circle {
  final double PI = 3.1415;
  num r;
  
  Circle(this.r);
  
  // num area(){
  //   return this.PI*this.r*this.r;
  // }

//使用get声明的方法不能有小括号
//  Getter
num get area{
  return this.PI*this.r*this.r;
}
// Setter
set setR(value){
  this.r=value;
}
}

void main(){
  var c = new Circle(10);
  // print(c.area());
    
  print(c.area);
  c.setR=20;
  print(c.area);
}
```