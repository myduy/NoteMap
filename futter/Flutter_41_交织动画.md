- why
  - 交织动哈是由多个单个一动画叠加而形成复杂动画
  - 例如：组件变化肯涉及高度、宽度、颜色、透明度、位置等等
  - 需要给每个动画设置时间间隔（Interval）
- transform(对组件进行矩阵变换)
  - 平移:Transform.translate()
  - 旋转：Transform.rotate()
  - 缩放:Transform.scale()

```DART
import 'package:flutter/material.dart';
import 'dart:math';

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
        title: Text("Animation"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: AnimationDemo(),
    );
  }
}

//Container
class AnimationDemo extends StatefulWidget {
  const AnimationDemo({Key key}) : super(key: key);

  @override
  _AnimationDemoState createState() => _AnimationDemoState();
}

class _AnimationDemoState extends State<AnimationDemo>
    with SingleTickerProviderStateMixin {
  AnimationController controller;
  Animation animation;
  Animation sizeAnimation;
  Animation colorAnimation;
  Animation rotationAnimation;

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    //  创建AnimationController
    controller =
        AnimationController(vsync: this, duration: Duration(seconds: 3));
    //  创建动画
    animation = CurvedAnimation(
      parent: controller,
      curve: Interval(0.0, 0.5),
    ) //  监听动画
      ..addListener(
        () {
          setState(() {});
        },
      );

    animation.addStatusListener((status) {
      if (status == AnimationStatus.completed) {
        controller.reverse();
      } else if (status == AnimationStatus.dismissed) {
        controller.forward();
      }
    });
    sizeAnimation = Tween(begin: 0.0, end: 200).animate(animation);
    colorAnimation = ColorTween(begin: Colors.yellow, end: Colors.red).animate(
        CurvedAnimation(
            parent: controller,
            curve: Interval(0.5, 0.8, curve: Curves.bounceIn)))
      ..addListener(() {
        setState(() {});
      });
    rotationAnimation = Tween(begin: 0.0, end: 2 * pi)
        .animate(CurvedAnimation(parent: controller, curve: Curves.easeIn));
  }

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Column(
        children: [
          ElevatedButton(
              onPressed: () {
                controller.forward();
              },
              child: Text("放大")),
          ElevatedButton(
              onPressed: () {
                controller.reverse();
              },
              child: Text("缩小")),
          ElevatedButton(
              onPressed: () {
                controller.stop();
              },
              child: Text("停止")),
          Opacity(
            opacity: controller.value,
            child: Transform.rotate(
              angle: rotationAnimation.value,
              child: Container(
                width: sizeAnimation.value,
                height: sizeAnimation.value,
                color: colorAnimation.value,

              ),
            ),
          )
        ],
      ),
    );
  }
  @override
  void dispose() {
    // TODO: implement dispose
    super.dispose();
    controller.dispose();
  }
}
```