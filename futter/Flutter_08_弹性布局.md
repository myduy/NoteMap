- Flex
  - direction(声明主轴方向)
  - mainAxisAlignment(声明主轴对齐方式)
  - textDirection（声明交叉轴对齐方式）
  - verticalDirection（声明垂直方向的排列顺序）
  - children(声明子组件)
- Expanded（可伸缩组件）
  - flex（声明弹性布局）
  - child（声明子组件）

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

void main() {
  //下一个组件
  runApp(MyApp());
}

//MaterialApp
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "flex",
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
      body: FlexDemo(),
    );
  }
}

//Container
class FlexDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    //Column的children可以传多个组件
    return Column(
      children: [
        Row(
          children: [
            //需要声明宽高
            Container(
              color: Colors.lightBlue,
              height: 50,
              width: 50,
            ),
            //自由伸缩 获取父元素
            Expanded(
              child: Container(
                color: Colors.lightGreen,
                height: 50,
              ),
            ),
          ],
        ),
        Flex(
          direction: Axis.horizontal,
          mainAxisAlignment: MainAxisAlignment.spaceAround,
          textDirection: TextDirection.rtl,
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
            )
          ],
        ),
        //水平布局
        Flex(
          direction: Axis.horizontal,
          children: [
            Expanded(
              child: Container(
                color: Colors.tealAccent,
                height: 50,
                // 声明占比不需要width
                // width: 50,
              ),
              flex: 2,
            ),
            Expanded(
              child: Container(
                color: Colors.amberAccent,
                height: 50,
                // 声明占比不需要width
                // width: 50,
              ),
              flex: 1,
            ),
          ],
        ),
        //垂直布局
        Container(
          height: 100,
          margin: EdgeInsets.all(50),
          child: Flex(
            // 排布方式
            direction: Axis.vertical,
            //垂直方向
            verticalDirection: VerticalDirection.up,
            children: [
              Expanded(
                child: Container(
                  color: Colors.tealAccent,
                  height: 50,
                  // 声明占比不需要width
                  // width: 50,
                ),
                //水平布局占比
                flex: 2,
              ),
              //间隔组件
              Spacer(
                flex: 1,
              ),
              Expanded(
                child: Container(
                  color: Colors.amberAccent,
                  height: 50,
                  // 声明占比不需要width
                  // width: 50,
                ),
                flex: 1,
              ),
            ],
          ),
        )
      ],
    );
  }
}
```