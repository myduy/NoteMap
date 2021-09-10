- CakebdarDatePicker(日历选择器)
  - initialCaledarMode
    - DatePickerMode.day
    - DatePickerMode.year
- ShowDatePicker(日期选择器)
  - initialDatePickerMode(year|day)
  - initialEntryMode(calendaar|input)
- showTimePicker(时间选择器)

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
        title: Text("Calendar"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: CalendarDemo(),
    );
  }
}

class CalendarDemo extends StatefulWidget {
  const CalendarDemo({Key key}) : super(key: key);

  @override
  _CalendarDemoState createState() => _CalendarDemoState();
}

class _CalendarDemoState extends State<CalendarDemo> {
  DateTime _date = DateTime.now();

  @override
  Widget build(BuildContext context) {
    return Container(
      child: Column(
        children: <Widget>[
          Text(
            '当前日期:${_date.toIso8601String()}',
            style: TextStyle(color: Colors.grey, fontSize: 16),
          ),
          _buildInfoTitle('CupertinoDatePickerMode.dateAndTime'),
          buildPicker(CupertinoDatePickerMode.dateAndTime),
          _buildInfoTitle('CupertinoDatePickerMode.date'),
          buildPicker(CupertinoDatePickerMode.date),
          _buildInfoTitle('CupertinoDatePickerMode.time'),
          buildPicker(CupertinoDatePickerMode.time),
        ],
      ),
    );
  }

  Container buildPicker(CupertinoDatePickerMode mode) {
    return Container(
      margin: EdgeInsets.all(10),
      height: 150,
      child: CupertinoDatePicker(
        mode: mode,
        initialDateTime: DateTime.now(),
//        maximumDate: DateTime(2018,8,8),
//        minimumDate: DateTime(2030,8,8),
        minimumYear: 2018,
        maximumYear: 2030,
        use24hFormat: false,
        minuteInterval: 1,
        backgroundColor: CupertinoColors.white,
        onDateTimeChanged: (date) {
          print(date);
          setState(() => _date = date);
        },
      ),
    );
  }

  Widget _buildInfoTitle(info) {
    return Padding(
      padding: const EdgeInsets.only(left: 20, top: 20, bottom: 5),
      child: Text(
        info,
        style: TextStyle(
            color: Colors.blue, fontSize: 16, fontWeight: FontWeight.bold),
      ),
    );
  }
}
```

