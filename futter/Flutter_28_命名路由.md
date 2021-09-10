- 声明路由

  - routes路由表(Mao类型)
  - initialRoute (初始化路由)
  - onUnknowRoute(未知路由-404)

- 跳转路由命名路由

  - ```dart
    Navigator.pushNamed(context,‘路由名称’）
    ```

### 命名路由

```dart
MaterialApp(
//...//其他配置
    routes:{//注册路由（路由表）
        'firest':(context) => FirstPage(),
        'second':(context) = > SecondPage(),
    },
    initialRoute:'firest',//初始化路由
    onUnknowRoute:(RouteSettings setting) => MaterialPageRoute(
    builder:(context) =>UnknownPage()//位置路由
    ),
);
```

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
      // home: Home(),
//      声明路由
    routes: {
        'home':(context) => Home(),
      'Product':(context) => Product(),
    },
      initialRoute: 'home',
      onUnknownRoute: (RouteSettings setting) => MaterialPageRoute(builder: (context)=> UnKnowPage()),
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
      body:Center(
        child: Column(
          children: [
            ElevatedButton(onPressed: ()=>Navigator.pushNamed(context, 'Product'), child: Text("跳转")),
            ElevatedButton(onPressed: ()=>Navigator.pushNamed(context, 'product'), child: Text("错误")),
          ],
        ),
      ),
    );
  }
}

class Product extends StatelessWidget {
  const Product({Key key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar:AppBar(
        title: Text("路由页"),
        leading: Icon(Icons.menu),
        actions: [
          Icon(Icons.settings)
        ],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body:Center(
        child: Column(
          children: [ElevatedButton(onPressed: () => Navigator.pop(context), child: Text("返回"))],
        ),
      ),
    );
  }
}
class UnKnowPage extends StatelessWidget {
  const UnKnowPage({Key key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar:AppBar(
        title: Text("UnKnowPage"),
        leading: Icon(Icons.menu),
        actions: [
          Icon(Icons.settings)
        ],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body:Center(
        child: Column(
          children: [ElevatedButton(onPressed: () => Navigator.pop(context), child: Text("返回"))],
        ),
      ),
    );
  }
}
```