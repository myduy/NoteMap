- Image.asset(加载本地图片)
  - Flutter项目下,创建图片存储目录
  - 在pubspec.yaml中的flutter部分添加图片配置
  - 在代码中添加加载图片
- Image.netWork(加载网络图片)
  - 保证网络畅通
  - 设置网络访问权限
  - 允许http协议访问

```dart
import 'package:flutter/material.dart';
//涉及内容 查看04和10
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
      body: HelloFlutter(),
    );
  }
}

//Container
class HelloFlutter extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        //加载网络图片,需要在yaml 声明
        Image.asset('images/Icon-192.png',
        width: 200,
        height: 200,
        fit: BoxFit.fill,
        ),
        Image.asset('images/Icon-512.png'),
        //网络图片 安卓需要在xml文件声明
        Image.network("",
          repeat: ImageRepeat.repeat,
          //背景与图片混合
          colorBlendMode:BlendMode.colorDodge,
          color: Colors.green,
        ),
      ],
    );
  }
}
```

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

  assets:
   - images/Icon-192.png
   - images/Icon-512.png


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
        - asset: fonts/Source_Sans_Pro/SourceSansPro-Black.ttf
        - asset: fonts/Source_Sans_Pro/SourceSansPro-BlackItalic.ttf
          weight: 300
          style: italic
```
