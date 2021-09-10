- Wrap(解决内容溢出问题)
  - spacing(主轴方向组件的间距)
  - alignment(主轴方向的对齐方式)
  - runSpacing(纵轴方向组件的间距)
  - runAlignment(纵轴方向的对齐方式)
- Chip（标签）
- CircleAvatar(圆形头像)

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
      title: "FlutterDemo",
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
        title: Text("Warp"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: WrapDemo(),
    );
  }
}

//Container
class WrapDemo extends StatelessWidget {
  List<String> _list = ['曹操', '司马懿', '曹仁', '曹洪', '张辽', '许诸'];

  List<Widget> _weiGuo() {
    return _list
        .map(
          (e) => Chip(
            avatar: CircleAvatar(
              backgroundColor: Colors.pink,
              child: Text('魏'),
            ),
            label: Text(e),
          ),
        )
        .toList();
  }


  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: [
        Wrap(
          children: _weiGuo(),
          //水平间距
          spacing: 18.0,
          // 主轴方向对齐方式
          alignment: WrapAlignment.spaceAround,
          //垂直间距
          runSpacing: 100,
          runAlignment: WrapAlignment.spaceAround,//交叉轴方向的对齐方式
        ),
        // Row 内容会溢出
        Wrap(
          children: [
            Chip(
              //圆体体现
              avatar: CircleAvatar(
                // 背景颜色
                backgroundColor: Colors.blue,
                //内容
                child: Text('蜀国'),
              ),
              // 标签
              label: Text('刘备'),
            ),
            Chip(
              avatar: CircleAvatar(
                backgroundColor: Colors.blue,
                child: Text('蜀国'),
              ),
              label: Text('张飞'),
            ),
            Chip(
              avatar: CircleAvatar(
                backgroundColor: Colors.blue,
                child: Text('蜀国'),
              ),
              label: Text('诸葛亮'),
            ),
            Chip(
              avatar: CircleAvatar(
                backgroundColor: Colors.blue,
                child: Text('蜀国'),
              ),
              label: Text('赵云'),
            ),
          ],
        ),
      ],
    );
  }
}

```

