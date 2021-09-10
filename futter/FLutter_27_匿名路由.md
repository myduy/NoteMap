- Route
  - 一个路由时一个屏幕或界面的抽象
- Navigator
  - 管理路由的组件。Navigator 可以通过路由入栈和出栈来实现页面之间的跳转
  - 常用属性：
    - initialRoute:初始路由，即默认页面
    - onGenerateRoute：动态路由(根据规则，匹配动态路由)
    - onUnknowRoute:未知路由,也就是404
    - routes:路由集合

匿名路由

- ​	Navigator

  - push(跳转到指定组件)

  ```dart
  Navigator.push(
  context,
  MaterialPageRoute(builder:(context) => 组件名称())
  )
  ```

  - pop(回退)

  ```dart
  Navigator.pop(context)
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
        title: Text("匿名路由"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  const HomePage({Key key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
      child: Center(
        child: ElevatedButton(
            onPressed: () {
              return Navigator.push(
                  context, MaterialPageRoute(builder: (context) => Product()));
            },
            child: Text("跳转到商品页面")),
      ),
    );
  }
}


class Product extends StatelessWidget {
  const Product({Key key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text("Flutter"),
        ),
    body: Container(
      child: Center(
        child: ElevatedButton(
          onPressed: (){
            Navigator.pop(context);
          },
          child: Text('回退'),
        ),
      ),
    ));
  }
}
```