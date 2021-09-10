- Scaffold
  - drawer(左侧抽屉菜单)
  - endDrawer(右侧抽屉菜单)
- UserAccountsDrawerHeader
  - 抽屉菜单头部组件
- AboutListTitle
  - 关于弹窗

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
        title: Text("Drawer"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: HomePage(),
      drawer: DrawerList(),
      endDrawer:DrawerList() ,
    );
  }
}

//Container
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
        child: Center(
      child: Text("Hello Flutter", textDirection: TextDirection.ltr),
    ));
  }
}

class DrawerList extends StatelessWidget {
  const DrawerList({Key key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        padding: EdgeInsets.all(0),
        children: [
          // Text("Drawer"),
          UserAccountsDrawerHeader(
            decoration: BoxDecoration(
              image: DecorationImage(
                image: AssetImage('images/Icon-512.png'),
                fit: BoxFit.cover,
              ),
            ),
            accountName: Text(
              "初六",
              style: TextStyle(color: Colors.black),
            ),
            accountEmail:
                Text("wwww@163.com", style: TextStyle(color: Colors.black)),
            currentAccountPicture: CircleAvatar(
              backgroundImage: AssetImage('images/Icon-512.png'),
            ),
          ),
          ListTile(leading: Icon(Icons.settings),
          title: Text('设置'),
          trailing: Icon(Icons.arrow_back),),
          ListTile(leading: Icon(Icons.account_balance),
          title: Text('余额'),
          trailing: Icon(Icons.arrow_back),),
          Divider(thickness: 2,),
          ListTile(leading: Icon(Icons.settings),
          title: Text('我的'),
          onTap: ()=>Navigator.pop(context),
          trailing: Icon(Icons.arrow_back_ios),),
          AboutListTile(
            child: Text("关于"),
            applicationName: '你的应用名称',
            applicationVersion: '1.0.0',
            icon: CircleAvatar(
              child: Text('aaa'),
            ),
            applicationLegalese: "应用法律条例",
            aboutBoxChildren: [
              Text("条例一：xxx"),
              Text("条例二：xxx"),
            ],
            applicationIcon: Image.asset('images/Icon-512.png',
            width: 50,
            height: 50,),
          )
        ],
      ),
    );
  }
}
```