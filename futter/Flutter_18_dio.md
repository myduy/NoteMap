- dio是一个强大的Dart Http请求库(类似axios)
  - https://pub.dev/packages/dio
- 使用步骤
  - 在pubsepc.yaml中添加dio依赖
  - 安装依赖(pub get | flutter packages get | vs Code 中保存配置，自动下载)
  - 引入import 'package:dio/dio.dart'
  - 使用：https://pub.dev/docmentation.dio/latest/

```dart
import 'package:dio/dio.dart';
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
        title: Text("Dio"),
        leading: Icon(Icons.menu),
        actions: [
          Icon(Icons.settings)
        ],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: DioDemo(),
    );
  }
}

//Container
class DioDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
        child: ElevatedButton(
          child: Text("点击发送请求"),
          onPressed:(){
            // 调用 Http请求
            getIpAddress();
          },
      ),
    );
  }
  void getIpAddress() async {
   try{
     final url = "https://httpbin.org/ip";
     Response response = await Dio().get(url);
     String ip = response.data['orgin'];
     print(ip);
   }catch( e ) {
     print(e);
   }
  }
}
```

