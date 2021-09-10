

##### 声明[字体](https://fonts.google.com)

加压压缩包，将字体文件复制到Flutter项目中

##### 在pubspec.yaml声明字体

```yaml
name: flutter_space
description: A new Flutter project.

# The following line prevents the package from being accidentally published to
# pub.dev using `pub publish`. This is preferred for private packages.
publish_to: 'none' # Remove this line if you wish to publish to pub.dev

# The following defines the version and build number for your application.
# A version number is three numbers separated by dots, like 1.2.43
# followed by an optional build number separated by a +.
# Both the version and the builder number may be overridden in flutter
# build by specifying --build-name and --build-number, respectively.
# In Android, build-name is used as versionName while build-number used as versionCode.
# Read more about Android versioning at https://developer.android.com/studio/publish/versioning
# In iOS, build-name is used as CFBundleShortVersionString while build-number used as CFBundleVersion.
# Read more about iOS versioning at
# https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html
version: 1.0.0+1

environment:
  sdk: ">=2.12.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter


  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^1.0.2

dev_dependencies:
  flutter_test:
    sdk: flutter

# For information on the generic Dart part of this file, see the
# following page: https://dart.dev/tools/pub/pubspec

# The following section is specific to Flutter.
flutter:

  # The following line ensures that the Material Icons font is
  # included with your application, so that you can use the icons in
  # the material Icons class.
  uses-material-design: true

  # To add assets to your application, add an assets section, like this:
  # assets:
  #   - images/a_dot_burr.jpeg
  #   - images/a_dot_ham.jpeg

  # An image asset can refer to one or more resolution-specific "variants", see
  # https://flutter.dev/assets-and-images/#resolution-aware.

  # For details regarding adding assets from package dependencies, see
  # https://flutter.dev/assets-and-images/#from-packages

  # To add custom fonts to your application, add a fonts section here,
  # in this "flutter" section. Each entry in this list should have a
  # "family" key with the font family name, and a "fonts" key with a
  # list giving the asset and other descriptors for the font. For
  # example:
  # fonts:
  #   - family: Schyler
  #     fonts:
  #       - asset: fonts/Schyler-Regular.ttf
  #       - asset: fonts/Schyler-Italic.ttf
  #         style: italic
  #   - family: Trajan Pro
  #     fonts:
  #       - asset: fonts/TrajanPro.ttf
  #       - asset: fonts/TrajanPro_Bold.ttf
  #         weight: 700
  #
  # For details regarding fonts from package dependencies,
  # see https://flutter.dev/custom-fonts/#from-packages
  fonts:
    - family: SourceSansPro
      fonts:
      #字体已经下载解压到 项目/fonts/Source_Sans_Pro/
        - asset: fonts/Source_Sans_Pro/SourceSansPro-Black.ttf
        - asset: fonts/Source_Sans_Pro/SourceSansPro-BlackItalic.ttf
          weight: 300
          style: italic

```

##### 使用

- 为整个应用设置默认自定义字体
- 为某个组件设置自定义字体

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
    return Column(children: [
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
        text: "Flutter",
        // 文本样式
        style: TextStyle(
          //字体大小
          fontSize: 40,
          // 样式颜色
          color: Colors.black45,
        ),
      )),
    ]);
  }
}

```

