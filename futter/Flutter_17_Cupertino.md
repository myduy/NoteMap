- Material
  - 安卓风格组将
  - import 'package:flutter/material.dart';
- Cupertino
  - [IOS风格组件](https://flutter.dev/docs/development/ui/widgets/cupertino)
  - import 'package:flutter/cupertino.dart'

- SafeArea 可以有效解决异性屏的问题（刘海屏）

```dart
import 'dart:io';
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';

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
        title: Text("cupertino"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: MyBody(),
    );
  }
}

//Container
class MyBody extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Widget dialogBox = MaterialDemo();
    String a = "未知设备";
    // // 判断当前平台详细
    if (Platform.isAndroid) {
      //  加载IOS的组件
      a = '安卓';
      dialogBox = MaterialDemo();
    } else if (Platform.isWindows) {
      a = 'Windows';
      dialogBox = MaterialDemo();
    } else if (Platform.isIOS) {
      // 加载Ios组件
      dialogBox = CupertinoDemo();
      a = 'IOS';
    }
    return Container(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.spaceAround,
        children: [
          Text("设备断结果为$a"),
          dialogBox,
          Text("Material-安卓风格组件"),
          //  安卓风格组件
          MaterialDemo(),
          Text("Cupertino-Ios风格组件"),
          //  Ios风格组件
          CupertinoDemo(),
        ],
      ),
    );
  }
}

class MaterialDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return AlertDialog(
      title: Text('提示'),
      content: Text('确认删除吗？'),
      actions: [
        TextButton(
            onPressed: () {
              print('取消逻辑');
            },
            child: Text('取消')),
        TextButton(
            onPressed: () {
              print('确认逻辑');
            },
            child: Text('确认'))
      ],
    );
  }
}

class CupertinoDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: CupertinoAlertDialog(
        title: Text("提示"),
        content: Text("确认删除吗？"),
        actions: [
          TextButton(
              onPressed: () {
                print('取消逻辑');
              },
              child: Text('取消')),
          TextButton(
              onPressed: () {
                print('确认逻辑');
              },
              child: Text('确认'))
        ],
      ),
    );
  }
}
```
