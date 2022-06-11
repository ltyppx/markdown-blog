目录

# widget的状态
无论是有状态还是无状态的widget都是不可变的，其属性的值都为final。
## 无状态的widget
无状态的widget使用类时继承StatelessWidget即可，然后实现其的 `build()` 方法。
## 有状态的widget
有状态的widget的状态可能在widget生命周期中发生变化，实现一个有状态的widget需要两个类：
1. StatefulWidget类：表示有状态的类，其本身不会发生改变。
2. State类：作为StatefulWidget类的内部类，其在widget生命周期始终存在。

在Android Studio中使用stful可以快速生成上面两个类。
```
class RandomWords extends StatefulWidget {
  const RandomWords({Key? key}) : super(key: key);

  @override
  State<RandomWords> createState() => _RandomWordsState();
}

// State类的名称带有下划线前缀(dart语言推荐，可以增强隐私性)
class _RandomWordsState extends State<RandomWords> {
  @override
  Widget build(BuildContext context) {
    final wordPair = WordPair.random();
    return Text(wordPair.asPascalCase);
  }
}
```
有状态的widget能改变的也只是内部的值，且必须要执行 `setState()` 方法才能改变。
```
class Counter extends StatefulWidget {

  const Counter({Key? key}) : super(key: key);

  @override
  _CounterState createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int _counter = 0;

  void _increment() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        ElevatedButton(
          onPressed: _increment,
          child: const Text('Increment'),
        ),
        const SizedBox(width: 16),
        Text('Count: $_counter'),
      ],
    );
  }
}
```

# 使用外部package
flutter使用的dart语言，其如果需要使用外部包必须先用flutter指令下载，并在项目中导入使用。
* 下载外部开源包

下载english_words开源包示例。
```
flutter pub add english_words
```
* pubspec.yaml文件

下载的外部包可以在pubspec.yaml文件中找到，其管理着flutter应用程序的assets和依赖项。
```
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
  english_words: ^4.0.0
```
* 安装缺少的依赖

如果是拉取别人的项目，缺少的依赖可以使用指令安装到项目。
```
flutter pub get
```
该命令会生成pubspec.lock文件，这里面包含了依赖packages的名称和版本。
```
packages:
    english_words:
        dependency: "direct main"
        description:
        name: english_words
        url: "https://mirrors.tuna.tsinghua.edu.cn/dart-pub/"
        source: hosted
        version: "4.0.0"
```
* 引入外部包并使用

使用import引入外部包english_words，并利用该包生成随机字符串。
```
import 'package:flutter/material.dart';
import 'package:english_words/english_words.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // 生成随机字符串
    final wordPair = WordPair.random();
    return MaterialApp(
      title: 'Welcome to Flutter',
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Welcome to Flutter'),
        ),
        body: Center(
          // 随机字符串使用大驼峰命名法展示
          child: Text(wordPair.asPascalCase),
        )
      ),
    );
  }
}
```