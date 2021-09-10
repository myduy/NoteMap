- Radio(单选框)
  - value(开关的值)，一般与状态的值段绑定）
  - onChanged(开关状态变更时调用)
  - groughValue(选择组的值)
- RadioListTile(单选列表)
  - value(开关的值，一般与状态字段绑定)
  - onChanged(开关状态变更时调用)
  - groupValue(选择组的值)

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
        title: Text("Radio"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: RadioDemo(),
    );
  }
}

class RadioDemo extends StatefulWidget {
  const RadioDemo({Key key}) : super(key: key);

  @override
  _RadioDemoState createState() => _RadioDemoState();
}

class _RadioDemoState extends State<RadioDemo> {
  int gender;

  @override
  Widget build(BuildContext context) {
    return Container(
      child: Column(
        children: [
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text('男'),
              Radio(
                value: 1,
                groupValue: this.gender,
                onChanged: (value) {
                  setState(() {
                    this.gender = value;
                  });
                },
              ),
              Text('女'),
              Radio(
                value: 2,
                groupValue: this.gender,
                onChanged: (value) {
                  setState(() {
                    this.gender = value;
                  });
                },
              ),
            ],
          ),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text(this.gender == 1 ? "男" : "女"),
            ],
          ),
          RadioListTile(
            value: 1,
            groupValue: this.gender,
            onChanged: (value) {
              setState(() {
                this.gender = value;
              });
            },
            title: Text("男性"),
            subtitle: Text("有胡子"),
            secondary: Icon(Icons.person),
            selected: this.gender==1,
            selectedTileColor: Colors.green[100],
          ),
          RadioListTile(
            value: 2,
            groupValue: this.gender,
            onChanged: (value) {
              setState(() {
                this.gender = value;
              });
            },
            title: Text("女性"),
            subtitle: Text("没有胡子"),
            secondary: Icon(Icons.person),
            selected: this.gender==2,
            selectedTileColor: Colors.green[100],
          ),
        ],
      ),
    );
  }
}
```

