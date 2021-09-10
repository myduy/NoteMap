##### Icon

- Flutter 中的图标库
- Icon(Icons.具体名称)

在线预览

[Icon图标](https://material.io/resources/icons)



##### Color(自定义颜色)

- ​	Flutter中通过ARGB来声明
  - const Color(0xFF42A5F5); //16进制的ARGB=透明度+6位十六位进制颜色
  - const Color.fromARGB(0xFF,0x42,0xA5,0xF5);
  - const Color.fromARGB(255,66,165,254);
  - const Color.fromRGBO(66,165,254,1.0);  //O=Opacity
- Color(英文字母声明的颜色)
  - Colors.red

```dart
import 'package:flutter/cupertino.dart';
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
      title: "Text",
      //下一个组件
      home: Home(),
      //全局设置字体
      // theme: ThemeData(fontFamily: 'SourceSansPro'),
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
        title: Text("Text"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: TextDemo(),
    );
  }
}

//Container
class TextDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    //Column的children可以传多个组件
    return Column(
      children: [
        Text(
          //文本内容
          "Flutter可以方便的加入现有的工程中。在全世界，Flutter 正在被越来越多的开发者和组织使用，并且 Flutter是完全免费、开源的。它也是构建未来的 Google Fuchsia 应用的主要方式.Flutter组件采用现代响应式框架构建，这是从React中获得的灵感，中心思想是用组件(widget)构建你的UI。 组件描述了在给定其当前配置和状态时他们显示的样子。当组件状态改变，组件会重构它的描述(description)，Flutter 会对比之前的描述， 以确定底层渲染树从当前状态转换到下一个状态所需要的最小更改。",
          //文本方向
          textDirection: TextDirection.ltr,
          // 样式
          style: TextStyle(
            // 字体大小
            fontSize: 30,
            //字体颜色
            color: Colors.red,
            //字体粗细
            fontWeight: FontWeight.w500,
            //字体样式 italic斜体
            fontStyle: FontStyle.italic,
            //文本修饰
            decoration: TextDecoration.lineThrough,
//            修饰颜色
            decorationColor: Colors.blue,
            // 局部设置字体
            fontFamily: 'SourceSansPro',
          ),
          //字体排列
          textAlign: TextAlign.left,
          //最大行数
          maxLines: 3,
          //溢出省略
          overflow: TextOverflow.ellipsis,
          //文本比例
          textScaleFactor: 1.5,
        ),
        //富文本 为文本生成多个样式
        RichText(
          // 文本范围
          text: TextSpan(
            text: "Hello",
            // 文本样式
            style: TextStyle(
              //字体大小
              fontSize: 40,
              // 样式颜色
              color: Color.fromARGB(255, 0, 0, 255),
            ),
            children: [
              TextSpan(
                text: "flutter",
                style: TextStyle(
                  fontSize: 40,
                  color: Colors.blue[200],
                ),
                children: [
                  TextSpan(
                    text: "你好世界",
                    style: TextStyle(
                      fontSize: 40,
                      color: Color.fromARGB(0xFF, 0x00, 0xFF, 0x00
                      ),
                    ),
                    children: [
                      TextSpan(
                        text: 'Dart',
                        style: TextStyle(
                          fontSize: 40,
                          color:Color.fromRGBO(255, 0, 0, 0.5)
                        ),
                      ),
                    ]
                  ),
                ],
              ),
            ],
          ),
        ),
      ],
    );
  }
}

```



