- Card(卡片)
  - child(子组件)
  - color(背景色)
  - shadowColor(阴影色)
  - elevatioan(阴影高度)
  - shape(边框样式)
  - margin(边框)
- ListTile(列表瓦片)
  - leading(头部组件)
  - title(标题)
  - subtitle(子组件)

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
        title: Text("卡片"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: CardDemo(),
    );
  }
}

//Container
class CardDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Card(
          margin: EdgeInsets.all(30.0),
          color: Colors.purpleAccent[100],
          shadowColor: Colors.yellow,//阴影颜色
          elevation: 20,//阴影高度
          shape: RoundedRectangleBorder(
            borderRadius: BorderRadius.circular(40),
            side: BorderSide(
              color: Colors.yellow,
              width: 3,
            ),
          ),
          child: Column(
            children: [
              ListTile(
                leading: Icon(
                  Icons.supervised_user_circle_rounded,
                  size: 50,
                ),
                title: Text(
                  "张三",
                  style: TextStyle(
                    fontSize: 30,
                  ),
                ),
                subtitle: Text(
                  "董事长",
                  style: TextStyle(
                    fontSize: 30,
                  ),
                ),
              ),

              //分割线
              Divider(),

              ListTile(
                title: Text(
                  "电话：133333333333",
                  style: TextStyle(
                    fontSize: 30,
                  ),
                ),
              ),
              ListTile(
                title: Text(
                  "地址：xxxxxxxxxxxx",
                  style: TextStyle(
                    fontSize: 30,
                  ),
                ),
              ),
            ],
          ),
        ),
        Card(
          margin: EdgeInsets.all(30.0),
          child: Column(
            children: [
              ListTile(
                leading: Icon(
                  Icons.supervised_user_circle_rounded,
                  size: 50,
                ),
                title: Text(
                  "李四",
                  style: TextStyle(
                    fontSize: 30,
                  ),
                ),
                subtitle: Text(
                  "总经理",
                  style: TextStyle(
                    fontSize: 30,
                  ),
                ),
              ),

              //分割线
              Divider(),

              ListTile(
                title: Text(
                  "电话：133333333333",
                  style: TextStyle(
                    fontSize: 30,
                  ),
                ),
              ),
              ListTile(
                title: Text(
                  "地址：xxxxxxxxxxxx",
                  style: TextStyle(
                    fontSize: 30,
                  ),
                ),
              ),
            ],
          ),
        )
      ],
    );
  }
}
```