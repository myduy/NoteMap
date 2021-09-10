#### MaterialApp

title(任务管理器中的标题)

home（主内容）

debugShowCheckedModeBanner(是否形式右上角调试标记)

#### Scaffold

appBar(应用头部)

body(应用主体)

floatingActionButton(浮动按钮)

drawer(左侧抽屉菜单)

endDrawer(右侧抽屉菜单)

```mermaid
graph TD
main-->runApp-->Myapp-->b((MaterialApp))
b-->b1{title}
b-->b2{home}
b-->b3>debugShowCheckedModeBanner]
b2-->c((Scaffold))
c-->c1{drawer}
c-->c2{appBar}
c-->c3{body}
c-->c4>floatingActionButton]
c-->c5{endDrawer}
c2-->da([AppBar])
da-->da1[leading]
da-->da2[title]
da-->da3[actions]
c3-->db((具体组件))
db-->db1[属性1]
db-->db2[属性2]
db-->db3[...]
```

初始化项目App结构

```mermaid

flowchart TD
    subgraph  MyApp
		subgraph MaterialApp
			subgraph Scaffold
			end
		end
    end
```

```mermaid
flowchart LR
    subgraph  MyApp
            subgraph MaterialApp
                subgraph Scaffold
                    subgraph appbar
					subgraph leading
                  	  end
                  	  subgraph Title
                  	  end
					subgraph action1
                  	  end
                  	  subgraph action2
                  	  end
                    end
                    subgraph body
                    floatingActionButton-.-a1((+))
					..
                    end
                    bottomNavigationBar
                    subgraph drawer
                    end
                    subgraph endrawer
                    end
                end
            end
    end
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
    return Container(
        child: Center(
          child: Text(
              "Hello Flutter",
              textDirection: TextDirection.ltr
          ),
        )
    );
  }
}
```
