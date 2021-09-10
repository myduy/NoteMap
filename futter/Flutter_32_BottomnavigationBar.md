- items
  - 包含导航(BottomnavigationBarItem)的列表
- currentIndex
  - 当前导航索引
- type
  - 导航类型（BottomNavigationBatType）
- onTap()
  - 导航的点击事件(一般会更新导航索引)

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
class Home extends StatefulWidget {
  const Home({Key key}) : super(key: key);

  @override
  _HomeState createState() => _HomeState();
}

class _HomeState extends State<Home> {
  final List<BottomNavigationBarItem> bottomNavItems = [
    BottomNavigationBarItem(
        backgroundColor: Colors.blue,
        icon: Icon(Icons.home),
        label: "首页"
    ),
    BottomNavigationBarItem(
        backgroundColor: Colors.blue,
        icon: Icon(Icons.home),
        label: "消息"
    ),
    BottomNavigationBarItem(
        backgroundColor: Colors.blue,
        icon: Icon(Icons.home),
        label: "购物车"
    ),
    BottomNavigationBarItem(
        backgroundColor: Colors.blue,
        icon: Icon(Icons.home),
        label: "我"
    ),
  ];

  final  pages = [
    Center(
      child: Text("home",style: TextStyle(fontSize: 50),),
    ),
    Center(
      child: Text("message",style: TextStyle(fontSize: 50),),
    ),

    Center(
      child: Text("Cart",style: TextStyle(fontSize: 50),),
    ),
    Center(
      child: Text("Profile",style: TextStyle(fontSize: 50),),
    )
  ];
  int currentIndex;
  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    currentIndex=0;

  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Drawer"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      bottomNavigationBar: BottomNavigationBar(items: bottomNavItems,
      currentIndex: currentIndex,
      // type: BottomNavigationBarType.fixed,
        type: BottomNavigationBarType.shifting,
      onTap: (index){
        _changePage(index);
      },),

      body:pages[currentIndex],
    );;
  }
  void _changePage(int index){
    if(index != currentIndex){
      setState(() {
        currentIndex = index;
      });
    }
  }
}
```