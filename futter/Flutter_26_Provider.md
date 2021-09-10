- Provider 是对InheritedWidget的封装
  - https://pub.dev/packages/provider
- 优点：
  - 简化资源的分配与处置
  - 懒加载
- Provider

```mermaid
graph TD
subgraph Provider
changeNotifier-->data
changeNotifier-->top[ChangeNotifierProviser]
top-->A[Listener]
A-.->top
A-->B
B-->Producer-.->top
B-->E
A-->C-->F
C-->Listener-.->top
end
```

```mermaid
graph TD
subgraph model
被观察者 
A(["数据模型(ChangeNotifier)"])
end
subgraph ViewModel
观察者
B(["Provider(ChangeNotifierProvider)"])
end
subgraph View
生产者 --> C1(["Producer"]) 
C1-->生产者
C2(["Listenner(Consumer)"])-->消费者
消费者-->C2
end

A-->B
B-->A
B-->C1
C1-->B
B-->C2
C2-->B
```

```mermaid
flowchart RL
		A["- 安装Provider(第三方库)"]
	subgraph Model
	B["- 创建数据模型 (T extends ChangeNotifier)"]
	end
	subgraph ViewModel
	C["- 创建Provider (注册数据模型)"]
		D["		- Proviser() //不会被要求随着变动而变动"]
		E["		- ChangeNotifierProvider() //随着某些数据改变而被通知更新"]
	end
	subgraph View
		F["- 获取数据模型并更新UI"]
			G["		- 通过上下文(BuildContext)"]
			H["		- 通过静态方法(Provider.of<T>(context))"]
	end
```

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

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
    // 创建Provider
    return ChangeNotifierProvider(
      create:(BuildContext context)=>new LikesModel(),
      child: Scaffold(
        appBar: AppBar(
          title: Text("LikesModel"),
          leading: Icon(Icons.menu),
          actions: [Icon(Icons.settings)],
          elevation: 0.0,
          centerTitle: true,
        ),
        //下一个组件
        body: MyHomePage(),
      ),

    );
  }
}

class LikesModel extends ChangeNotifier {
  int _counter = 0;

  int get counter => _counter;

  incrementCounter() {
    //累加
    _counter++;
    //通过 UI 更新
    notifyListeners();
  }
}

class MyHomePage extends StatelessWidget {
  const MyHomePage({Key key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Column(
        children: [
          Text(
            //在子组件中使用数据类型
            "${ context.watch<LikesModel>().counter }",
          ),
          TextButton(
            onPressed:Provider.of<LikesModel>(context).incrementCounter,
            child: Icon(Icons.thumb_up),
          ),
        ],
      ),
    );
  }
}
```
