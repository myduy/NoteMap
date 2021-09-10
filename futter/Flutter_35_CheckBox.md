- Checkbox
  - value(复选框的值)
  - onChanged(复选框状态更改时调用)
  - activeColor(选中时，复选框背景的颜色)
  - chckColor(选中时，复选框中对号的颜色)
- CheckboxListTile
  - title(标题)
  - subtitle(子标题)

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
        title: Text("Checkbox"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: CheckboxDemo(),
    );
  }
}

//Container
class CheckboxDemo extends StatefulWidget {
  const CheckboxDemo({Key key}) : super(key: key);

  @override
  _CheckboxDemoState createState() => _CheckboxDemoState();
}

class _CheckboxDemoState extends State<CheckboxDemo> {
  bool _male = true;
  bool _female = false;
  bool _transgender = true;
  bool _value1 = true;
  bool _value2 = true;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        ListTile(
          leading: Checkbox(
            value: this._male,
            onChanged: (bool val) {
              setState(() {
                this._male = val;
              });
            },
          ),
          title: Text('男'),
        ),
        ListTile(
          leading: Checkbox(
            value: this._female,
            onChanged: (bool val) {
              setState(() {
                this._female = val;
              });
            },
          ),
          title: Text('女'),
        ),
        ListTile(
          leading: Checkbox(
            value: this._transgender,
            onChanged: (bool val) {
              setState(() {
                this._transgender = val;
              });
            },
            activeColor: Colors.pink,
            checkColor: Colors.yellow,
          ),
          title: Text('人妖'),
        ),
        CheckboxListTile(
          secondary: Icon(Icons.settings),
          value: this._value1,
          onChanged: (bool val) {
            setState(() {
              this._value1 = val;
            });
          },
          activeColor: Colors.pink,
          checkColor: Colors.yellow,
          title: Text('1:00叫我起床'),
          subtitle: Text("太困了起不来"),
          selected: this._value1,
        ),
        CheckboxListTile(
          secondary: Icon(Icons.settings),
          value: this._value2,
          onChanged: (bool val) {
            setState(() {
              this._value2 = val;
            });
          },
          activeColor: Colors.black12,
          checkColor: Colors.yellow,
          title: Text('3:00叫我起床'),
          subtitle: Text("这还差不多"),
        ),
      ],
    );
  }
}
```