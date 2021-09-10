- 使用步骤
  - 创建表单Form,并以GlobalKey 作为唯一性的标识
  - 添加带验证逻辑的TextFormField到Form中
  - 创建按钮以验证和提交
- Form(表单容器)
  - key(GlobalKey)
  - child(子组件)
- TextFormFild(输入框)
  - 与TextField的区别：必须在Form内使用& 带有验证器
  - validator(验证器)

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
        title: Text("首页"),
        leading: Icon(Icons.menu),
        actions: [
          Icon(Icons.settings)
        ],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: FormDemo(),
    );
  }
}

class FormDemo extends StatefulWidget {
  const FormDemo({Key key}) : super(key: key);

  @override
  _FormDemoState createState() => _FormDemoState();
}

class _FormDemoState extends State<FormDemo> {
  final GlobalKey<FormState> _formKey = GlobalKey<FormState>();
  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(20),
      child: Column(
        children: [
          Form(
              key: _formKey,
              child:Column(
           children: [
             TextFormField(
               decoration: InputDecoration(
                 hintText: "手机号",
               ),
               validator: (value){
                 RegExp reg = new RegExp(r'^\d{11}$');
                 if(!reg.hasMatch(value)){
                 return '手机号非法';
                 }
                 return null;
               },
             )
           ],
          )
          ),
          Row(
            children: [
              Expanded(child: ElevatedButton(
                onPressed: (){
                  if (_formKey.currentState.validate()){
                    print('提交成功');
                  }
                },
                child: Text('提交'),
              ))
            ],
          ),
        ],
      ),
    );
  }
}
```

- From(表单容器)
  - c创建表单唯一键: final GlobalKey<formState> _form = GlobalKey<FormState>_()
  - 验证表单：_formKey.currentState.validate()
  - 提交表单:_formKsy.currentState.save()
  - 重置表单:_formKsy.currentState.reset()
- TextFormField(输入框)
  - validator(验证器)
  - obscureTet(密码框)
  - onSaved
    - 设定表单字段的值
    - 在表单的save()执行之后

```dart
import 'package:flutter/material.dart';

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
        title: Text("首页"),
        leading: Icon(Icons.menu),
        actions: [
          Icon(Icons.settings)
        ],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: FormDemo(),
    );
  }
}

class FormDemo extends StatefulWidget {
  const FormDemo({Key key}) : super(key: key);

  @override
  _FormDemoState createState() => _FormDemoState();

}

class _FormDemoState extends State<FormDemo> {
  final GlobalKey<FormState> _formKey = GlobalKey<FormState>();
  String _phone;
  String password;
  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(20),
      child: Column(
        children: [
          Form(
              key: _formKey,
              child:Column(
           children: [
             TextFormField(
               decoration: InputDecoration(
                 hintText: "手机号",
               ),
               validator: (value){
                 RegExp reg = new RegExp(r'^\d{11}$');
                 if(!reg.hasMatch(value)){
                 return '手机号非法';
                 }
                 return null;
               },
               onSaved: (value){
                 print('saveOn');
                 _phone=value;
               },
             ),
             TextFormField(
               obscureText: true,
               decoration: InputDecoration(
                 hintText: "密码",
               ),
               validator: (value){
                 print(password);
                 return value.length<6?"密码长度不够":null;
                 RegExp reg = new RegExp(r'^\d{11}$');
                 if(!reg.hasMatch(value)){
                 return '手机号非法';
                 }
                 return null;
               },
               onSaved: (value){
                 print('saveOn');
                 password=value;
               },
             ),
           ],
          )
          ),
          Row(
            children: [
              SizedBox(width: 20,),
              Expanded(child: ElevatedButton(
                onPressed: (){
                  if (_formKey.currentState.validate()){
                    print('提交成功');
                    print('before');
                    _formKey.currentState.save();
                    print('after');
                  }
                },
                child: Text('提交'),
              ))
            ],
          ),
        ],
      ),
    );
  }
}
```