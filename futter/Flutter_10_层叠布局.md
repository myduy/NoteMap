- Stack(层叠组件-类似css中的z-index)

  - alignment(声明未定位组件的对齐方式)
  - textDirection(声明未得组件的排列顺序)

- Positioned（绝对定位组件）

  - child (声明子组件)
  - left,top,right,bottom
  - width,height

- NetworkLmage(网络图片组件)

  - NetworkImage('图片地址')

  - \<uses-permission android:name="android.permission.INTERNET"/\>
   > 安卓xml声明
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.flutter_space">
<!--  声明网络访问权限  -->
    <uses-permission android:name="android.permission.INTERNET"/>
    <!--同意http协议 android:usesCleartextTraffic="true" -->
   <application
        android:label="flutter_space"
       
        android:usesCleartextTraffic="true"
        android:icon="@mipmap/ic_launcher">
        <activity
            android:name=".MainActivity"
            android:launchMode="singleTop"
            android:theme="@style/LaunchTheme"
            android:configChanges="orientation|keyboardHidden|keyboard|screenSize|smallestScreenSize|locale|layoutDirection|fontScale|screenLayout|density|uiMode"
            android:hardwareAccelerated="true"
            android:windowSoftInputMode="adjustResize">
            <!-- Specifies an Android theme to apply to this Activity as soon as
                 the Android process has started. This theme is visible to the user
                 while the Flutter UI initializes. After that, this theme continues
                 to determine the Window background behind the Flutter UI. -->
            <meta-data
              android:name="io.flutter.embedding.android.NormalTheme"
              android:resource="@style/NormalTheme"
              />
            <!-- Displays an Android View that continues showing the launch screen
                 Drawable until Flutter paints its first frame, then this splash
                 screen fades out. A splash screen is useful to avoid any visual
                 gap between the end of Android's launch screen and the painting of
                 Flutter's first frame. -->
            <meta-data
              android:name="io.flutter.embedding.android.SplashScreenDrawable"
              android:resource="@drawable/launch_background"
              />
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
        <!-- Don't delete the meta-data below.
             This is used by the Flutter tool to generate GeneratedPluginRegistrant.java -->
        <meta-data
            android:name="flutterEmbedding"
            android:value="2" />
    </application>
</manifest>
```

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
        title: Text("stack"),
        leading: Icon(Icons.menu),
        actions: [Icon(Icons.settings)],
        elevation: 0.0,
        centerTitle: true,
      ),
      //下一个组件
      body: StackDemo(),
    );
  }
}

//Container
class StackDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
        child: Stack(
      //    声明未得的子组件的排序方式
      textDirection: TextDirection.rtl,
      //    声明未定位的子组件的对齐方式
      alignment: AlignmentDirectional.bottomCenter,
      children: [
        CircleAvatar(
          //android 默认http无法加载内容
          backgroundImage: NetworkImage(
              'https://img.alicdn.com/tfs/TB1R5fsgyDsXe8jSZR0XXXK6FXa-281-80.jpg'),
//              大小
          radius: 200,
        ),
        // 绝对定位
        Positioned(
          child: Container(
            color: Colors.red,
            padding: EdgeInsets.all(10),
            child: Text(
              "热卖",
              style: TextStyle(
                color: Colors.white,
                fontSize: 20,
              ),
            ),
          ),
          top: 100,
          right: 60,
        ),
        Text(
          "Hello",
          style: TextStyle(
            color: Colors.black,
            fontSize: 40,
          ),
        ),
      ],
    ));
  }
}
```
