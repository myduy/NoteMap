#### 布局-container

- child(声明组件)
- padding（margin）
  - Edgelnsets (all()、fromLTEB()、only())
- decoration
  - Boxdecoration （边框、圆角、渐变、阴影、背景色、北京图片）
- alinment
  - Alinment(内容对齐)
- transform
  - Matrix4(平移-translate、旋转-rotate、缩放-scale、斜切-skew)

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
      body: ContainerDemo(),
    );
  }
}

//Container
class ContainerDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
        child: Text(
          "Flutter可以方便的加入现有的工程中。在全世界，Flutter 正在被越来越多的开发者和组织使用，并且 Flutter是完全免费、开源的。它也是构建未来的 Google Fuchsia 应用的主要方式.Flutter组件采用现代响应式框架构建，这是从React中获得的灵感，中心思想是用组件(widget)构建你的UI。 组件描述了在给定其当前配置和状态时他们显示的样子。当组件状态改变，组件会重构它的描述(description)，Flutter 会对比之前的描述， 以确定底层渲染树从当前状态转换到下一个状态所需要的最小更改。",
          textDirection: TextDirection.ltr,
          style: TextStyle(
            fontSize: 20,
          ),
        ),
        //宽高
        // width: 200,
        // height: 200,
        //无线
        width: double.infinity,
        height: double.infinity,
        //四边内边距
        padding: EdgeInsets.all(10.0),
        //外边距
        margin: EdgeInsets.fromLTRB(10.0, 30.0, 0.0, 5.0),
        // 控件居中
        alignment: Alignment.center,
        //位移
        // transform: Matrix4.translationValues(100, 0, 0),
        //旋转
        // transform: Matrix4.rotationZ(0.1),
        // transform: Matrix4.rotationZ(-0.1),
        //斜切
        transform: Matrix4.skewX(0.2),
        
        //设置边框线样式
        decoration: BoxDecoration(
          // 方式一
          // border: Border(
          //   top: BorderSide(
          //     width: 10.0,
          //     color: Colors.red,
          //   ),
          //   bottom: BorderSide(
          //     width: 10.0,
          //     color: Colors.red,
          //   ),
          //   left: BorderSide(
          //     width: 10.0,
          //     color: Colors.red,
          //   ),
          //   right: BorderSide(
          //     width: 10.0,
          //     color: Colors.red,
          //   ),
          // ),
          //方式二
          border:Border.all(
            width: 10.0,
            color: Colors.blue,
          ),

          //设置边框角
          // 方式一
          // borderRadius: BorderRadius.all(Radius.circular(30)),
          //方式二
          borderRadius: BorderRadius.only(
            topLeft: Radius.circular(30),
          ),
        // 背景色
          color: Colors.lightGreen[100],
          // 渐变设置渐变背景色失效
          gradient: LinearGradient(
            colors: [
              Colors.lightBlue,
              Colors.white12,
            ],
          ),
        ));
  }
}

```

