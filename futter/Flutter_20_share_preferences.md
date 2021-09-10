- share_preferences是一个本地数据缓存库(类似asyncStorage)
  - https://pub.dev/packages/shared_preferences
- 使用步骤
  - 在pubsepc.yaml中添加shared_preferences依赖
  - 安装依赖(pub get |flutter packages get | VS Code 中保存配置，自动下载)
  - 引入 import 'package:shared_preferences/shared_preferences.dart';
  - 使用 SharePreferences pres = await SharedPreferences.getinstance();

shared_preferences-操作

- 增
  - setString(key,value)
  - setint(key,value)
- 删
  - remove(Key)
  - clear()
- 改
  - 更改就是重新设置数据
  - setString(key,value)
- 查
  - getString(key)

```dart
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

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
        title: Text("shared_preferences"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: SharedPreferencesDemo(),
    );
  }
}

//Container
class SharedPreferencesDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      width: double.infinity,
      child: Column(
        mainAxisAlignment: MainAxisAlignment.spaceAround,
        crossAxisAlignment: CrossAxisAlignment.center,
        children: [
          ElevatedButton(
              onPressed: () {
                _incrementCounter();
              },
              child: Text("递增")),
          ElevatedButton(
              onPressed: () {
                _decrementCounter();
              },
              child: Text("递减")),
          ElevatedButton(
              onPressed: () {
                _removeCounter();
              },
              child: Text("删除")),
          ElevatedButton(
              onPressed: () {
                _addMyCounter();
              },
              child: Text("设置")),
          ElevatedButton(
              onPressed: () {
                _getCounter();
              },
              child: Text("获取")),
          ElevatedButton(
              onPressed: () {
                _clearContent();
              },
              child: Text("清空")),
        ],
      ),
    );
  }
}

_incrementCounter() async {
  // 获取保存示例
  SharedPreferences prefs = await SharedPreferences.getInstance();
  int counter = (prefs.getInt('counter') ?? 0) + 1;
  print('Pressed $counter times');
  await prefs.setInt('counter', counter);
}

_decrementCounter() async {
  // 获取保存示例
  SharedPreferences prefs = await SharedPreferences.getInstance();
  int counter = prefs.getInt('counter') ?? 0;
  if (counter > 0){
    counter--;
  }
  print('Pressed $counter times');
  await prefs.setInt('counter', counter);
}
_removeCounter() async {
  // 获取保存示例
  SharedPreferences prefs = await SharedPreferences.getInstance();
  await prefs.remove('counter');
  int counter = (prefs.getInt('counter') ?? 0)+1;
  print('Pressed $counter times');
  await prefs.setInt('counter', counter);
}
_addMyCounter() async {
  // 获取保存示例
  SharedPreferences prefs = await SharedPreferences.getInstance();
  await prefs.setString('hi', 'hello world');
  String counter = (prefs.getString('hi') ?? '');
  print('设置字符串的内容是 $counter');
}

_getCounter() async {
  // 获取保存示例
  SharedPreferences prefs = await SharedPreferences.getInstance();
  String counter = (prefs.getString('hi') ?? "");
  print('获取字符串的内容是 $counter');
}

_clearContent() async{
  SharedPreferences prefs = await SharedPreferences.getInstance();
  await prefs.clear();
}
```