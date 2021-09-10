> - Flutter 1.22之前
>   - Flatbutton(扁平按钮)
>   - RaisedButtion(突起按钮)
>   - OtlineButton(轮廓按钮)
> - Flutter 1.22之后
>   - TextButton (文本按钮-用来替换FlatButton)
>   - ElevatedButton(凸起按钮-用来替换RaisedButton)
>   - OutLineButton(轮廓按钮-用来替换OutLineButton)

| 按钮           | 主题               |
| -------------- | ------------------ |
| TextButton     | TextButtonTheme    |
| OutLineButtom  | OutLineButtomTheme |
| ElevatedButton | ElevateButtonTheme |

> - 图标按钮
>   - IconButton
>   - TextButton.icon()
>   - ElevatedButton.icon()
>   - OutLineButton.icon()
> - ButtonBar(按钮组)
> - FloatingActionButton(浮动按钮)
> - BackButton(回退按钮)
> - CloseButton(关闭按钮)

```dart
import 'dart:io';

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
        title: Text("button"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: ButtonDemo(),
      floatingActionButton:FloatingActionButton(
        onPressed: (){},
        tooltip: 'Increment',
        child: Icon(Icons.add),
        backgroundColor: Colors.green,
        elevation: 0,
      ),
    );
  }
}

//Container
class ButtonDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(10),
      child: Wrap(
        children: [
          TextButton(
            onPressed: () {
              print('点击TextButton');
            },
            onLongPress: () {
              print("长按TextButton");
            },
            child: Text("TextButton"),
          ),
          ElevatedButton(
            onPressed: () {
              print('点击ElevatedButton');
            },
            onLongPress: () {
              print("长按ElevatedButton");
            },
            child: Text("ElevatedButton"),
          ),
          OutlinedButton(
            onPressed: () {
              print('点击OutlineButton');
            },
            onLongPress: () {
              print("长按OutlineButton");
            },
            child: Text("OutlineButton"),
          ),
          OutlinedButton(
            onPressed: () {
              print('点击OutlineButton');
            },
            onLongPress: () {
              print("长按OutlineButton");
            },
            child: Text(
              "轮廓按钮",
            ),
            style: ButtonStyle(
              textStyle: MaterialStateProperty.all(
                TextStyle(
                  fontSize: 30,
                ),
              ),
              foregroundColor: MaterialStateProperty.resolveWith(
                (states) {
                  if (states.contains(MaterialState.pressed)) {
                    //  按下按钮时的前景色
                    return Colors.red;
                  }
                  // 默认状态颜色
                  return Colors.blue;
                },
              ),
              backgroundColor: MaterialStateProperty.resolveWith(
                (states) {
                  if (states.contains(MaterialState.pressed)) {
                    //  按下按钮时的前景色
                    return Colors.yellow;
                  }
                  // 默认状态颜色
                  return Colors.white;
                },
              ),
              shadowColor: MaterialStateProperty.all(Colors.yellow),
              elevation: MaterialStateProperty.all(20),
              side: MaterialStateProperty.all(
                BorderSide(
                  color: Colors.green,
                  width: 2,
                ),
              ),
              //声明按钮形状
              shape: MaterialStateProperty.all(
                //CircleBorder圆形按钮
                StadiumBorder(
                  side: BorderSide(
                    color: Colors.green,
                    width: 2,
                  ),
                ),
              ),
              //  设置按钮大小
              minimumSize: MaterialStateProperty.all(
                Size(200, 100),
              ),
              //  设置水波纹颜色
              overlayColor: MaterialStateProperty.all(Colors.purple),
            ),
          ),
          OutlinedButtonTheme(
            data: OutlinedButtonThemeData(
              style: ButtonStyle(
                overlayColor: MaterialStateProperty.all(Colors.red),
              ),
            ),
            child: OutlinedButton(
              onPressed: () {
                print('点击OutlineButton');
              },
              onLongPress: () {
                print("长按OutlineButton");
              },
              child: Text(
                "轮廓按钮",

              ),

//              有全局失效
              // style: ButtonStyle(
              //   overlayColor: MaterialStateProperty.all(Colors.red),
              // ),

            ),
          ),
        //  图标按钮
          IconButton(
            icon:Icon(Icons.add_alarm),
              onPressed: (){
              print("IconButton");
              },
              color: Colors.red,
              splashColor: Colors.lightBlue,
              // 声明高光颜色 水波纹小时
              // highlightColor: Colors.purple,
              tooltip: "怎么了",
              ),
          TextButton.icon(
            icon:Icon(Icons.add_circle),
            onPressed: (){},
            label: Text("文本按钮"),
          ),
          ElevatedButton.icon(
            icon:Icon(Icons.add_circle),
            onPressed: (){},
            label: Text("凸起按钮"),
          ),
          OutlinedButton.icon(
            icon:Icon(Icons.add_circle),
            onPressed: (){},
            label: Text("轮廓按钮"),
          ),
          // 按钮组
          Container(
            color: Colors.pink[100],
            width: double.infinity,
            child: ButtonBar(
              children: [
                //超出水平n，垂直显示
                ElevatedButton(onPressed: (){}, child: Text("按钮1"),),
                ElevatedButton(onPressed: (){}, child: Text("按钮2"),),
                ElevatedButton(onPressed: (){}, child: Text("按钮3"),),
                ElevatedButton(onPressed: (){}, child: Text("按钮1"),),
                ElevatedButton(onPressed: (){}, child: Text("按钮2"),),
                ElevatedButton(onPressed: (){}, child: Text("按钮3"),),
              ],
            ),
          ),
          BackButton(
            color: Colors.red,
            onPressed: (){
            },
          ),
          CloseButton(
            color: Colors.red,
            onPressed: (){
            },

          ),
        //  浮动按钮需要配合Scaffold使用 上翻查找
        ],
      ),
    );
  }
}
```