- GridView(网格布局)
  - children(子组件)
  - scrollDirection (滚动方向)
  - gridDelegate
    - sliverGridDelegateWithFixedCrossAxisCount(指定列数-子组件宽度自适应)
    - sliverGridDelegateWithFixedCrossAxisExtent(指定子组件-列数自适应)
- GridView.count(列数固定)
- Girdbuilder(动态网格布局)

> 列数(固定)：crossAxisCount:2
>
> 格宽：childWidth
>
> 格高：childHeight
>
> 格宽高比: childWidth/childHeight=childAspectRadio
>
> 行距: crossAxisSpacing
>
> 列距:mainAxisSpacing

形式一

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
        title: Text("GridView"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: GridViewDemo(),
    );
  }
}

//Container
class GridViewDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(10),
      child:
        //竖
/*        GridView(
          gridDelegate:
          SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 2,//指定列数
            mainAxisSpacing: 20,//主轴方向的间距
            crossAxisSpacing: 10,//交叉轴的间距
            childAspectRatio: 1.5,
          ),
          children: [
            Container(color: Colors.blue,),
            Container(color: Colors.red,),
            Container(color: Colors.amberAccent,),
            Container(color: Colors.brown,),
            Container(color: Colors.lightBlueAccent,),
            Container(color: Colors.black38,),
            Container(color: Colors.black45,),
            Container(color: Colors.indigoAccent,),
          ],
        ),*/
        //横
          GridView(
        gridDelegate: SliverGridDelegateWithMaxCrossAxisExtent(
          maxCrossAxisExtent: 190,
          mainAxisSpacing: 30,
          crossAxisSpacing: 10,
          childAspectRatio: 0.8,
        ),
        children: [
          Container(color: Colors.indigoAccent,),
          Container(color: Colors.blue,),
          Container(color: Colors.red,),
          Container(color: Colors.amberAccent,),
          Container(color: Colors.brown,),
          Container(color: Colors.lightBlueAccent,),
          Container(color: Colors.black38,),
          ),
        ],
      ),
    );
  }
}

```

形式二

- ScollPhyscs physics(确定可滚动控件的物理特效)
  - BouncingScrollPhtsics(允许超出边界-反弹效果)
  - ClampingScrollPhysics(防止超出边界-夹住效果)
  - AlwaysScrollableScrollPhysics(始终响应滚动)
  - NeverScrollableScrollPhysics(不响应滚动)

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
        title: Text("GridView"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      //   body:GridViewExtendDemo(),
      // body: GridViewCountDemo(),
        body:GridViewBuildDemo(),
    );
  }
}

//Container
class GridViewCountDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: GridView.count(
          children: List.generate(10, (index) => Image.asset('images/Icon-192.png')),
          crossAxisCount: 2,
        padding: EdgeInsets.symmetric(horizontal: 40),
        childAspectRatio: 1.5,

      ),
    );
  }
}

class GridViewExtendDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: GridView.extent(
          children: List.generate(10, (index) => Image.asset('images/Icon-192.png')),
        maxCrossAxisExtent: 190,
        mainAxisSpacing: 20,
        crossAxisSpacing: 20,
        padding: EdgeInsets.symmetric(horizontal: 40),
        // childAspectRatio: 1.5,
      ),
    );
  }
}
class GridViewBuildDemo extends StatelessWidget {
   final List<Widget> _tiles = [            Container(color: Colors.blue,),
   Container(color: Colors.red,),
   Container(color: Colors.amberAccent,),
   Container(color: Colors.brown,),
   Container(color: Colors.lightBlueAccent,),
   Container(color: Colors.black38,),
   Container(color: Colors.black45,),
   Container(color: Colors.indigoAccent,),];
  @override
  Widget build(BuildContext context) {
    return Container(
      child: GridView.builder(
        gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 2,
          mainAxisSpacing: 20,
          crossAxisSpacing: 20,
          childAspectRatio: 1.0,
        ),
        padding: EdgeInsets.symmetric(horizontal: 40),
        itemCount: _tiles.length,
        itemBuilder: (context,index){
          return _tiles[index];
        },
        // physics: BouncingScrollPhysics(),//反弹效果
        // physics: ClampingScrollPhysics(),//夹住效果
        // physics: AlwaysScrollableScrollPhysics(),//滚动
        // physics: NeverScrollableScrollPhysics(), //禁止滚动
        // childAspectRatio: 1.5,
      ),
    );
  }
}
```



