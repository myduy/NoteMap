- DefaultTapController(整个Tap导航的容器)
  - length(声明导航组件数量)
  - child(指定子组件组件)
- TabBar(导航菜单)
  - tabs(导航菜单数组)
- TabBarView(导航页面)
  - children(多个导航页面内容)

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
  final List<Widget> _tabs = [
    Tab(text: "首页",icon: Icon(Icons.home),),
    Tab(text: "添加",icon: Icon(Icons.home),),
    Tab(text: "搜索",icon: Icon(Icons.home),),
  ];
  final List<Widget> _tabViews = [
    Icon(Icons.home,size: 120,color:Colors.red,),
    Icon(Icons.home,size: 120,color:Colors.green,),
    Icon(Icons.home,size: 120,color:Colors.black,),
  ];
  @override
  Widget build(BuildContext context) {
    return DefaultTabController(length: _tabs.length, child:   Scaffold(
      appBar: AppBar(
        title: Text("Drawer"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
        bottom: TabBar(
          tabs: _tabs,
          labelColor: Colors.yellow,
          unselectedLabelColor: Colors.black45,
          indicatorSize: TabBarIndicatorSize.tab,
          indicatorColor: Colors.yellow,
          indicatorWeight: 10,
        ),
      ),
      //下一个组件
      body: TabBarView(
        children: _tabViews,
      ),
      bottomNavigationBar: TabBar(
        tabs: _tabs,
        labelColor: Colors.blue,
        unselectedLabelColor: Colors.black,
      ),
    ));



  }
}
```