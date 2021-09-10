路由传参-匿名路由

- 路由中声明参数
  - Navigator.push
- 组件中接受参数

```dart
Navigator.push(context,
	MaterialPageRoute(builder:(context){
        return BlogDetail(
        id:blogitem['id'],
        );
    })
);
```

```dart
class BlogDetail extends StatefulWidget{
    //构造函数
    BlogDetail({Key key,@require this.id})： super(Key:key);
    final int id;
}
```

路由传参数-命名路由

- 路由中声明参数
  - Navigator.pushNamed(context,routename,{arguments})

- 组件中接受参数
  - Modalroute.of(context).settings.arguments

```dart
Navigator.pushNamed(
context,
"/homePage",
arguments:{
    'title':"命名路由传递过来的title"}
);
```

```dart
class HomePage extends StatelessWidget{
//获取参数
final Map arguments = ModalRoute.of(context).setting.arguments;
    String title = arguments['title'];

}
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
//      下一个组件
      home: Home(),
     // 声明路由
    routes: {
        'home':(context) => Home(),
      'Product':(context) => Product(),
      'ProductDetail':(context) => ProductDetail(),
    },
      initialRoute: 'home',
      onUnknownRoute: (RouteSettings setting) => MaterialPageRoute(builder: (context)=> UnKnowPage()),


      // onGenerateRoute: (RouteSettings setting){
      // //  匹配首页
      //   print("当前路径："+setting.name);
      //   if(setting.name == '/'){
      //     return MaterialPageRoute(builder: (context)=>Home());
      //   }
      //   if(setting.name == '/Product'){
      //     return MaterialPageRoute(builder: (context)=>Product());
      //   }
      //   var uri = Uri.parse(setting.name);
      //   print(uri.pathSegments);
      //   if(uri.pathSegments.length == 2 && uri.pathSegments.first=='Product'){
      //     var id = uri.pathSegments[1];
      //     return MaterialPageRoute(builder: (context)=>ProductDetail(id: id));
      //   }
      //   return MaterialPageRoute(builder: (context)=>UnKnowPage());
      // },
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
            ElevatedButton(onPressed: ()=>Navigator.pushNamed(context, 'Product',
            arguments: {"title":"我是主页传来的参数"}
            ), child: Text("跳转")),
            ElevatedButton(onPressed: ()=>Navigator.pushNamed(context, 'ProductDetail',
                arguments: {"id":1}
                ), child: Text("1")),
            ElevatedButton(onPressed: ()=>Navigator.pushNamed(context, 'ProductDetail',
                arguments: {"id":2}
                ), child: Text("2")),
            ElevatedButton(onPressed: ()=>Navigator.pushNamed(context, '/Product/2'), child: Text("2")),
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
    final Map argument = ModalRoute.of(context).settings.arguments;
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
          children: [
            Text("接受的参数是："+argument['title']),
            ElevatedButton(onPressed: () => Navigator.pop(context), child: Text("返回"))],
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

class ProductDetail extends StatelessWidget {
  //Product/1
  final String id;
  const ProductDetail({Key key,this.id}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    final Map argument = ModalRoute.of(context).settings.arguments;
    return Scaffold(
      appBar:AppBar(
        title: Text("ProductDetail"),
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
            Text('当前商品id是:${argument['id'].toString()}'),
            ElevatedButton(onPressed: () => Navigator.pop(context), child: Text("返回"))],
        ),
      ),
    );
  }
}
```