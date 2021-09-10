- 09column
  - Column 中的主轴方向是垂直方向
  - mainAxisAlignment:MainAxisAlignment 主轴对齐方式
  - corssAxisAlignment:CorssAxisAlignment 交叉轴对齐方式
  - children:内容
- Row
  - Row中的主轴方向是水平方向（其他属性与Column一致）

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

void main() {
  //下一个组件
  runApp(MyApp());
}

//MaterialApp
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "ContainerRowDemo",
      //下一个组件
      home: Home(),
      debugShowCheckedModeBanner: false,
    );
  }
}

//Scaffold
class Home extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Text"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: ContainerRowDemo(),
    );
  }
}

//Container
class ContainerRowDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    //Column的children可以传多个组件
    return Container(
      color: Colors.lightGreen,
      //自适应 无限
      width: double.infinity,
      child: Column(
        //布局排版
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        crossAxisAlignment: CrossAxisAlignment.center,
        children: [
          Icon(
            Icons.access_alarm,
            size: 50,
          ),
          Icon(
            Icons.accessible_forward_rounded,
            size: 50,
          ),
          Icon(
            Icons.settings,
            size: 50,
          ),
          Icon(
            Icons.add_box,
            size: 50,
          ),
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceAround,
            children: [
              Icon(
                Icons.access_alarm,
                size: 50,
              ),
              Icon(
                Icons.accessible_forward_rounded,
                size: 50,
              ),
              Icon(
                Icons.settings,
                size: 50,
              ),
              Icon(
                Icons.add_box,
                size: 50,
              ),
            ],
          ),
        ],
      ),
    );
  }
}
```
