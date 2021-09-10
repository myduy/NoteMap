- 动态路由是指，通过onGEnerateRoute属性指定的路由

```dart
MateriApp(
//通过 OngenerateRoute 生成动态路由
    onGenerateRoute:(settings){
        //处理首页 '/'
        if(setting.name = '/'){
            return MaterialPageRoute(builder:(context) => HomeScreen());
        }
        //处理详情页面 '/detils/:id'
        var url = Uri.pares(settings.name);
        if(url.pathSegments.length = 2 && uri.pathSegments.first = 'details'){
			var id=uri.pathSegments[1];
            return MaterialPageRoute(builder:(context) => DetailScreen(id: id));
        }
        return MaterialPageRoute(builder:(context) => UnknowScreen());
    },
)
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
//     routes: {
//         'home':(context) => Home(),
//       'Product':(context) => Product(),
//     },
//       initialRoute: 'home',
//       onUnknownRoute: (RouteSettings setting) => MaterialPageRoute(builder: (context)=> UnKnowPage()),


      onGenerateRoute: (RouteSettings setting){
      //  匹配首页
        print("当前路径："+setting.name);
        if(setting.name == '/'){
          return MaterialPageRoute(builder: (context)=>Home());
        }
        if(setting.name == '/Product'){
          return MaterialPageRoute(builder: (context)=>Product());
        }
        var uri = Uri.parse(setting.name);
        print(uri.pathSegments);
        if(uri.pathSegments.length == 2 && uri.pathSegments.first=='Product'){
          var id = uri.pathSegments[1];
          return MaterialPageRoute(builder: (context)=>ProductDetail(id: id));
        }
        return MaterialPageRoute(builder: (context)=>UnKnowPage());
      },
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
            ElevatedButton(onPressed: ()=>Navigator.pushNamed(context, '/Product'), child: Text("跳转")),
            ElevatedButton(onPressed: ()=>Navigator.pushNamed(context, '/Product/1'), child: Text("1")),
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

class ProductDetail extends StatelessWidget {
  //Product/1
  final String id;
  const ProductDetail({Key key,this.id}) : super(key: key);
  @override
  Widget build(BuildContext context) {
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
            Text('当前商品id是:${this.id}'),
            ElevatedButton(onPressed: () => Navigator.pop(context), child: Text("返回"))],
        ),
      ),
    );
  }
}
```
