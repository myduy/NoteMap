- DataTable是Flutter中的表格
  - columns(声明)表头列表
    - DataColumn(表头单元格）
  - rows(声明数据列表)
    - DataRow（一行数据）
      - DataCell（数据单元格）
  - 其他属性

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
        title: Text("首页"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: UserList(),
    );
  }
}

class User {
  String name;
  int age;
  bool selected;

  User(this.name, this.age, {this.selected = false});
}

class UserList extends StatefulWidget {
  @override
  _UserListState createState() => _UserListState();
}

class _UserListState extends State<UserList> {
  List<User> data = [
    User('张三', 18),
    User('张三1', 18),
    User('张三2', 182, selected: true),
    User('张三3', 182),
    User('张三4', 118),
  ];
  var _sortAscending = true;

    dynamic _getUserRows() {
    List <DataRow>dataRows=[];
    for (int i = 0; i < data.length; i++) {
      dataRows.add(
        DataRow(
          selected: data[i].selected,
          onSelectChanged: (selected) {setState(() {data[i].selected = selected!;});},
          cells: [
            DataCell(Text("${data[i].name}"),),
            DataCell(Text("${data[i].age}"),),
            DataCell(Text("男"),),
            DataCell(Text("---"),),
          ],
        ),
      );
    }
    return dataRows;
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      child: SingleChildScrollView(
        scrollDirection: Axis.horizontal,
        child: DataTable(
          sortColumnIndex: 1,
          sortAscending: _sortAscending,
          dataRowHeight: 100,
          horizontalMargin: 20,
          columnSpacing: 100,
          columns: [
            DataColumn(
                label: Text(
                  "姓名",
                ),
                numeric: true,
                onSort: (int columnIndex, bool asscending) {
                  setState(() {
                    _sortAscending = asscending;
                    if (asscending) {
                      data.sort((a, b) => a.age.compareTo(b.age));
                    } else {
                      data.sort((a, b) => b.age.compareTo(a.age));
                    }
                  });
                }),
            DataColumn(label: Text("年龄")),
            DataColumn(label: Text("性别")),
            DataColumn(label: Text("简介")),
          ],
          rows:_getUserRows(),
            // DataRow(
            //   cells: [
            //     DataCell(Text("张三")),
            //     DataCell(Text("18")),
            //     DataCell(Text("male")),
            //     DataCell(Text("一个男人")),
            //   ],
            // ),
        ),
      ),
    );
  }
}
```