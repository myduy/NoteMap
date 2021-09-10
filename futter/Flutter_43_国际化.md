- 国际化(internationlization 简称i18n)
  - 终端(手机)系统语言切换时,Flutter应用的跟随切换,
- 内容
  - 组件(Widget)国际化
    - 例如:日历，弹窗等常用组件的国际化
  - 文本国际化(包括文本的顺序)
    - 自定义文本的国际化



- 在pubspec.yaml中引入flutter_localizations

  - 安装包 flutter pub get (VS Code中保存自动安装)

- 设置MaterialApp

  - import 'package:flutter_localizations/flutter_localizations.dart

  - locallizationDelegates(指定哪些组件进行国际化)

  - supportedLocales(指定要支持哪些语言)

  - ```dart
    suppertedLocales:[
        const Locale('en','US'),
        const Locale('zh','CN'),
    ]
    ```

- 查看组件国际化效果
  - 在模拟器上，将语言设置为中文

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';
import 'package:flutter_localizations/flutter_localizations.dart';

void run() {
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
      localizationsDelegates: [
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
        GlobalCupertinoLocalizations.delegate,
      ],
      supportedLocales: [
        const Locale('en','US'),
        const Locale('zh' ,'CN'),
      ],
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
    return ListView(
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

  Widget _buildInfoTitle(info){
    return    Padding(
      padding: const EdgeInsets.only(left: 20,top: 20,bottom: 5),
      child: Text(
        info,
        style: TextStyle(color: Colors.blue, fontSize: 16,fontWeight: FontWeight.bold),
      ),
    );
  }
}
```



- 文本创建本地化类
  - CustomLocalizations
- 创建本地化类的代理
  - CustomLocalizatiosDelegate extends LocalizationsDelegate<CustomLocalizations>
    - isSupported(当前本地化，是否在有效的语言范围内)
    - shouldReload(本地化重新构建时，是否调用load方法，加载本地化资源)
    - load(语言发生变更时，加载对于的本地化资源)
  - 使用本地化类
    - CustomLocalizations.delegate

