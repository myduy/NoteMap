> - ListView
>   - 加载列表的组件(加载所有Wifgets	,使用Widget较少的场景)
>   - ListTile(leading、title、subtitle、trailing、selected)
> - ListView.builder
>   - 按需加载Widget,性能比默认构造函数高,适用Widget较多的场景
> - ListView.separated
>   - 比ListView.builder多了分隔器

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
        title: Text("ListView"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: ListViewDemo(),
    );
  }
}

//Container
class ListViewDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return SingleChildScrollView(
      child: Column(
        children: [
          ListViewBasic(),
          ListViewHorizontal(),
          ListViewBuilderDemo(),
          ListViewSepratedDemo(),
        ],
      ),
    );
  }
}

class ListViewBasic extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      height: 200,
      child: ListView(
        scrollDirection: Axis.vertical,
        children: [
          ListTile(
            leading: Icon(Icons.access_alarm),
            title: Text('access_alarm'),
            subtitle: Text('子标题'),
            trailing: Icon(Icons.keyboard_arrow_right),
          ),
          ListTile(
            leading: Icon(Icons.access_alarm),
            title: Text('access_alarm'),
            subtitle: Text('子标题'),
            trailing: Icon(Icons.keyboard_arrow_right),
            selected: true,
            selectedTileColor: Colors.red[100],
          ),
          ListTile(
            leading: Icon(Icons.access_alarm),
            title: Text('access_alarm'),
            subtitle: Text('子标题'),
            trailing: Icon(Icons.keyboard_arrow_right),
          ),
          ListTile(
            leading: Icon(Icons.add_circle),
            title: Text('add_circle'),
            subtitle: Text('子标题'),
            trailing: Icon(Icons.keyboard_arrow_right),
          ),
        ],
      ),
    );
  }
}

class ListViewHorizontal extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      height: 100,
      child: ListView(
        scrollDirection: Axis.horizontal,
        children: [
          Container(
            width: 160,
            color: Colors.grey,
          ),
          Container(
            width: 160,
            color: Colors.amber,
          ),
          Container(
            width: 160,
            color: Colors.pink,
          ),
          Container(
            width: 160,
            color: Colors.red,
          ),
          Container(
            width: 160,
            color: Colors.pink,
          ),
          Container(
            width: 160,
            color: Colors.blueGrey,
          ),
          Container(
            width: 160,
            color: Colors.transparent,
          ),
        ],
      ),
    );
  }
}

class ListViewBuilderDemo extends StatelessWidget {
  final List<Widget> users = new List<Widget>.generate(
      20,
      (index) =>
          OutlinedButton(onPressed: () {}, child: Text("姓名${index + 1}")));

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 150,
      child: ListView.builder(
        itemBuilder: (context, index) {
          return users[index];
        },
        itemExtent: 30,
        itemCount: users.length,
      ),
    );
  }
}


class ListViewSepratedDemo extends StatelessWidget {
  final List<Widget> products = List.generate(20, (index) => ListTile(
    leading: Image.asset('images/Icon-192.png'),
    title: Text('商品标题$index'),
    subtitle: Text('子标题'),
    trailing: Icon(Icons.keyboard_arrow_right),

  ),);
  @override
  Widget build(BuildContext context) {
    Widget dividerOdd = Divider(
      color: Colors.blue,
      thickness: 2,
    );
    Widget dividerEven = Divider(
      color: Colors.red,
      thickness: 2,
    );
    return Column(
      children: [
        ListTile(
          title: Text("商品列表"),
        ),
        Container(
          height: 200,
          child: ListView.separated(
            itemBuilder: (context,index){
              return products[index];
            },
            separatorBuilder: (context,index){
              return index%2==0? dividerEven:dividerOdd;
            },
            itemCount: products.length,
          ),
        ),
      ],
    );
  }
}
```