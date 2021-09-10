- Hero动画用来实现跨页面的动画效果
  - 在不同页面中，声明一个共享组件（Hero）
  - 由于共享组件在不同页面的位置、外观等不同，路由切换时，形成动画效果
- 如何实现
  - 在页面A中定义起始Hero组件(source hero),声明tag
  - 在页面B中定义目标Hero组件(destination hero),绑定系统的tag
  - 页面跳转时，通过Navigator,传递tag
- Hero组件
  - tag(路由切换时，共享组件的标记)
  - child(声明子组件)

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
class Home extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("HeroAnimation"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: HeroAnimation(),
    );
  }
}

//Container
class HeroAnimation extends StatelessWidget {
  const HeroAnimation({Key key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
      child: GridView.extent(
        padding: EdgeInsets.symmetric(vertical: 20),
        maxCrossAxisExtent: 200.0,
        mainAxisSpacing: 20,
        children: List.generate(
          20,
          (index) {
            String imageURL = "https://picsum.photos/id/$index/300/400";
            return GestureDetector(
              onTap: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (BuildContext ctx) {
                      return ImageDetail(imageURL);
                    },
                  ),
                );
              },
              child:Hero(
                tag: imageURL,
                child: Image.network(imageURL),
              ) ,
            );
          },
        ),
      ),
    );
  }
}


//Scaffold
class ImageDetail extends StatelessWidget {
  final String imageURL;
  ImageDetail(this.imageURL);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.black12,
      //下一个组件
      body: Center(child: GestureDetector(
        onTap: (){
          Navigator.pop(context);
        },
        child: Hero(
          tag: imageURL,
          child: Image.network(imageURL,
          width: double.infinity,
          fit:BoxFit.cover),
        ),
      ),),
    );
  }
}
```