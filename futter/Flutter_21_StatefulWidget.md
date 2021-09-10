- flutter 中 的组件，按状态划分
  - StatelessWidget(无状态组件)
  - StatefulWidget(状态组件）
- 按状态作用域划分
  - 组件内私有状态（StatefulWidget）
  - 跨组件状态共享（inheritedWidget、provider）
  - 全局状态（Redux | fish-redux、Mobx...）
- 状态组件的组成
  - statefulWidget(组件本身不可变-@immutable)
  - State(将变化的状态放到State中维护)

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
        title: Text("StatefulWidget"),
        leading: Icon(Icons.menu),
        actions: [
          Icon(Icons.settings)
        ],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: MyState(),
    );
  }
}



class MyState extends StatefulWidget {
  @override
  _MyStateState createState() => _MyStateState();
}

class _MyStateState extends State<MyState> {
  int _num = 0;
  void _increment(){
    setState(
            (){
          _num++;
        });
  }
  void _decrement(){
    setState(
            (){
          _num--;
        });
  }
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Column(
        children: [
          ElevatedButton(onPressed:_decrement, child: Text('-')),
          Padding(
           padding: EdgeInsets.all(20),
           child: Text('$_num'),
          ),
          ElevatedButton(onPressed:_increment, child: Icon(Icons.add)),
        ],
      ),
    );
  }
}
```
