- Flutter 中最好的轮播组件，适配android和IOS
  - https://pub.dev/packages/flutter_swiper
- 使用步骤
  - 在pubsepc.yaml 中添加flutter_sweiper依赖
  - 安装依赖(pub get | flutter packages get | VS Code 中保存配置,自动下载)
  - 引入 import 'package:flutter_swiper/flutter_swiper.dart';
  - 使用

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
class Home extends StatelessWidget{
  @override
  Widget build(BuildContext context){
    return Scaffold(
      appBar:AppBar(
        title: Text("首页"),
        leading: Icon(Icons.menu),
        actions: [
          Icon(Icons.settings)
        ],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: HelloFlutter(),
    );
  }
}

//Container
class HelloFlutter extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
        child: Center(
          child: Text(
              "Hello Flutter",
              textDirection: TextDirection.ltr
          ),
        )
    );
  }
}
```