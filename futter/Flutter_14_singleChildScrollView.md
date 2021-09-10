- SingleChildCScrollView(类似Android中的ScrollView)
  - child(子组件)
  - padding(内边距)
  - scrollDirection(滚动方向:Axis.horizontal | Axis.vertical)
  - reverse(初始滚动位置,false 头部、ture尾部)
  - physics
    - clampingScollPhysics:Android下微光效果
    - BouncingScrollPhysics:IOS下弹性效果

```dart
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
      title: "Flutter",
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
        title: Text("SingleChildScrollView"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: SingleChildScrollViewDemo(),
    );
  }
}

//Container
class SingleChildScrollViewDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Stack(
      children: [
        SingleChildScrollView(
          // 滚动方向
          scrollDirection: Axis.horizontal,
          padding: EdgeInsets.all(10),
          reverse: true,
          child: Row(
            children: [
              OutlinedButton(
                onPressed: () {},
                child: Text("按钮1"),
              ),
              OutlinedButton(
                onPressed: () {},
                child: Text("按钮2"),
              ),
              OutlinedButton(
                onPressed: () {},
                child: Text("按钮3"),
              ),
              OutlinedButton(
                onPressed: () {},
                child: Text("按钮4"),
              ),
              OutlinedButton(
                onPressed: () {},
                child: Text("按钮5"),
              ),
              OutlinedButton(
                onPressed: () {},
                child: Text("按钮6"),
              ),
              OutlinedButton(
                onPressed: () {},
                child: Text("按钮7"),
              ),
            ],
          ),
        ),
        // 垂直方向的滚动
        SingleChildScrollView(
          // 滚动方向
          scrollDirection: Axis.vertical,
          padding: EdgeInsets.all(10),
          reverse: true,
          physics: BouncingScrollPhysics(),
          child: Column(
            children: List.generate(
              100,
              (index) => OutlinedButton(
                onPressed: () {},
                child: Text("按钮$index"),
              ),
            ),
          ),
        ),
      ],
    );
  }
}
```