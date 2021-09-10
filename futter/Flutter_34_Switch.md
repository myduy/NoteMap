- Switch
  - value(开关的值，一般与状态字段绑定)
  - onChanged(开关状态变更时调用)
  - activeColor(开关开启时的圆圈颜色）
  - activeTrackColor(开关开启时的轨道颜色)
  - inactiveThumbColor(开关关闭时的圆圈颜色)
  - inactiveTrackColor(开关关闭时的轨道颜色)
- CupertionSweitch(IOS风格的开关)
  - import 'package:flutter/cupertino.dart'

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';

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
        title: Text("Switch"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: SwitchDemo(),
    );
  }
}

class SwitchDemo extends StatefulWidget {
  const SwitchDemo({Key key}) : super(key: key);

  @override
  _SwitchDemoState createState() => _SwitchDemoState();
}

class _SwitchDemoState extends State<SwitchDemo> {
  bool _switchValue = false;
  @override
  Widget build(BuildContext context) {
    return Container(
        child: ListView(
      children: [
        ListTile(
          leading: Switch(
            value: _switchValue,
            onChanged: (bool val) {
              setState(() {
                _switchValue = val;
              });
            },
            activeColor: Colors.orange,
            activeTrackColor: Colors.pink,
            inactiveThumbColor: Colors.blue,
            inactiveTrackColor: Colors.black12,
          ),
          title: Text("当前状态${_switchValue == true ? "选" : '未选'}"),
        ),
        ListTile(
          leading: CupertinoSwitch(
              value: _switchValue,
              onChanged: (bool val) {
                setState(() {
                  _switchValue = val;
                });
              }),
        ),
        ListTile(
          leading: CupertinoSwitch(

              value: _switchValue,
              onChanged: (bool val) {
                setState(() {
                  _switchValue = val;
                });
              },
              activeColor: Colors.orange,
            trackColor: Colors.yellow,
          ),
        )
      ],
    ));
  }
}
```