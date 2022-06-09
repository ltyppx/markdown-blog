文章目录

# 基础widgets
## Text
Text用于编写文本，其构造函数如下：
```
Text(String data, {Key? key, TextStyle? style, StrutStyle? strutStyle, TextAlign? textAlign, TextDirection? textDirection, Locale? locale, bool? softWrap, TextOverflow? overflow, double? textScaleFactor, int? maxLines, String? semanticsLabel, TextWidthBasis? textWidthBasis, TextHeightBehavior? textHeightBehavior})
```
Text默认会占满父元素的一行，且在字符串长度超出一行后会换行。

常用参数的意义：
* data：显示的文本
* textAlign：文本排列方式
* overflow：文本超出对象宽度和高度的处理方式
* style：文本样式
* maxLines：最多多少行触发文本隐藏

如果要更细节的处理文本的样式，可以使用 `Text.rich()` 方法，其接收参数如下：
```
Text.rich(InlineSpan textSpan, {Key? key, TextStyle? style, StrutStyle? strutStyle, TextAlign? textAlign, TextDirection? textDirection, Locale? locale, bool? softWrap, TextOverflow? overflow, double? textScaleFactor, int? maxLines, String? semanticsLabel, TextWidthBasis? textWidthBasis, TextHeightBehavior? textHeightBehavior})
```
其可以配合TextSpan来做到文本内的字符串样式不同的效果，TextSpan的构造函数如下：
```
TextSpan ( { String ? text , List < InlineSpan > ? children , TextStyle ? style , GestureRecognizer ? 识别器, MouseCursor ? mouseCursor , PointerEnterEventListener ? onEnter , PointerExitEventListener ? onExit , String ? semanticsLabel , Locale ? locale , bool ? spellOut } )
```
常用参数的意义：
* text：显示的文本
* children：用于接收其他子元素列表
* style：文本样式
## Row、Column
### Row
Row是在水平方向中存放widget的容器，其构造函数如下：
```
Row({Key? key, MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start, MainAxisSize mainAxisSize = MainAxisSize.max, CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center, TextDirection? textDirection, VerticalDirection verticalDirection = VerticalDirection.down, TextBaseline? textBaseline, List<Widget> children = const <Widget>[]})
```
常用参数的意义：
* children：接收其他子元素列表
* mainAxisAlignment：子集在水平轴的对齐方式，默认为从左向右
* crossAxisAlignment：子集在纵轴的对齐方式，默认为垂直居中
* mainAxisSize：主轴大小适配，默认宽度铺面主轴方向

### Column
Column是在垂直方向中存放widget的容器，其构造函数如下：
```
Column({Key? key, MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start, MainAxisSize mainAxisSize = MainAxisSize.max, CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center, TextDirection? textDirection, VerticalDirection verticalDirection = VerticalDirection.down, TextBaseline? textBaseline, List<Widget> children = const <Widget>[]})
```
常用参数的意义：
* children：不必多说
* mainAxisAlignment：子集在纵轴的对齐方式，默认为从上到下
* crossAxisAlignment：子集在水平轴的对齐方式，默认为垂直居中
* mainAxisSize：主轴大小适配，默认宽度铺面主轴方向

### Expanded
Row和Column子项要想展开并填充可用空间，就要将子项包装在Expanded中，其构造函数如下：
```
Expanded({Key? key, int flex = 1, required Widget child})
```
参数的意义：
* child：单个widget元素
* flex：表示划分剩余未用区域的占比
## Stack
Stack也是存放widget的容器，不过在其里面的widget都是重叠存放的，其构造函数如下：
```
Stack ( { Key ? key , AlignmentGeometry alignment = AlignmentDirectional.topStart , TextDirection ? textDirection , StackFit fit = StackFit.loose , Clip clipBehavior = Clip.hardEdge , List < Widget > children = const <Widget>[] } )
```
参数的意义：
* children：存放widget数组
* alignment：设置widget开始展示的位置，默认是从顶部开始
### Positioned
Stack里面的widget都是重叠的，要设置他们在Stack的位置，就要用到Positioned，其构造函数如下：
```
Positioned({Key? key, double? left, double? top, double? right, double? bottom, double? width, double? height, required Widget child})
```
参数的意义：
* left、top、right、bottom：距离Stack容器左、上、右、下的距离
* width：该widget的宽度
* height：该widget的高度
* child：子widget

## Container
Container用于生成一个可见的矩形元素，其构造函数如下：
```
Container({Key? key, AlignmentGeometry? alignment, EdgeInsetsGeometry? padding, Color? color, Decoration? decoration, Decoration? foregroundDecoration, double? width, double? height, BoxConstraints? constraints, EdgeInsetsGeometry? margin, Matrix4? transform, AlignmentGeometry? transformAlignment, Widget? child, Clip clipBehavior = Clip.none})
```
参数的意义：
* alignment：在容器内对齐子widget的方式，默认显示在左上角
* child：子widget，默认如果Container内没有子widget，其会占满整个屏幕，如有，则会自适应子widget大小
* color：背景色
* width、height：设置宽高
* padding：设置内边距
* margin：设置外边距
* constraints：确定控件的大小
* transform：在绘制矩形前变化矩阵
* decoration：装饰矩形，会在子widget后
* foregroundDecoration：装饰矩形，会在子widget前

# Material控件
Material控件用于Material应用，其从MaterialApp widget开始，底层构建了许多的widget，包括了Navigator，它管理着由字符串标识的widget栈，又称routes。

Material控件使用于 `runApp()` 方法中，如下：
```
import 'package:flutter/material.dart';

void main() {
  runApp(
    const MaterialApp(
      title: 'Flutter Tutorial',
      home: TutorialHome(),
    ),
  );
}
```
Material控件的构造函数如下：
```
MaterialApp({Key? key, GlobalKey<NavigatorState>? navigatorKey, GlobalKey<ScaffoldMessengerState>? scaffoldMessengerKey, Widget? home, Map<String, WidgetBuilder> routes = const <String, WidgetBuilder>{}, String? initialRoute, RouteFactory? onGenerateRoute, InitialRouteListFactory? onGenerateInitialRoutes, RouteFactory? onUnknownRoute, List<NavigatorObserver> navigatorObservers = const <NavigatorObserver>[], TransitionBuilder? builder, String title = '', GenerateAppTitle? onGenerateTitle, Color? color, ThemeData? theme, ThemeData? darkTheme, ThemeData? highContrastTheme, ThemeData? highContrastDarkTheme, ThemeMode? themeMode = ThemeMode.system, Locale? locale, Iterable<LocalizationsDelegate>? localizationsDelegates, LocaleListResolutionCallback? localeListResolutionCallback, LocaleResolutionCallback? localeResolutionCallback, Iterable<Locale> supportedLocales = const <Locale>[Locale('en', 'US')], bool debugShowMaterialGrid = false, bool showPerformanceOverlay = false, bool checkerboardRasterCacheImages = false, bool checkerboardOffscreenLayers = false, bool showSemanticsDebugger = false, bool debugShowCheckedModeBanner = true, Map<ShortcutActivator, Intent>? shortcuts, Map<Type, Action<Intent>>? actions, String? restorationScopeId, ScrollBehavior? scrollBehavior, bool useInheritedMediaQuery = false})
```
参数的意义：
* routes：应用程序顶级路由表
* home：首页
* title：应用程序的单行描述

# 事件处理
## 手势处理
flutter有提供检测输入手势的控件 `GestureDetector` ，该控件在一些widget也有相应的回调函数，可以自行了解，GestureDetector的构造函数如下：
```
GestureDetector({Key? key, Widget? child, GestureTapDownCallback? onTapDown, GestureTapUpCallback? onTapUp, GestureTapCallback? onTap, GestureTapCancelCallback? onTapCancel, GestureTapCallback? onSecondaryTap, GestureTapDownCallback? onSecondaryTapDown, GestureTapUpCallback? onSecondaryTapUp, GestureTapCancelCallback? onSecondaryTapCancel, GestureTapDownCallback? onTertiaryTapDown, GestureTapUpCallback? onTertiaryTapUp, GestureTapCancelCallback? onTertiaryTapCancel, GestureTapDownCallback? onDoubleTapDown, GestureTapCallback? onDoubleTap, GestureTapCancelCallback? onDoubleTapCancel, GestureLongPressDownCallback? onLongPressDown, GestureLongPressCancelCallback? onLongPressCancel, GestureLongPressCallback? onLongPress, GestureLongPressStartCallback? onLongPressStart, GestureLongPressMoveUpdateCallback? onLongPressMoveUpdate, GestureLongPressUpCallback? onLongPressUp, GestureLongPressEndCallback? onLongPressEnd, GestureLongPressDownCallback? onSecondaryLongPressDown, GestureLongPressCancelCallback? onSecondaryLongPressCancel, GestureLongPressCallback? onSecondaryLongPress, GestureLongPressStartCallback? onSecondaryLongPressStart, GestureLongPressMoveUpdateCallback? onSecondaryLongPressMoveUpdate, GestureLongPressUpCallback? onSecondaryLongPressUp, GestureLongPressEndCallback? onSecondaryLongPressEnd, GestureLongPressDownCallback? onTertiaryLongPressDown, GestureLongPressCancelCallback? onTertiaryLongPressCancel, GestureLongPressCallback? onTertiaryLongPress, GestureLongPressStartCallback? onTertiaryLongPressStart, GestureLongPressMoveUpdateCallback? onTertiaryLongPressMoveUpdate, GestureLongPressUpCallback? onTertiaryLongPressUp, GestureLongPressEndCallback? onTertiaryLongPressEnd, GestureDragDownCallback? onVerticalDragDown, GestureDragStartCallback? onVerticalDragStart, GestureDragUpdateCallback? onVerticalDragUpdate, GestureDragEndCallback? onVerticalDragEnd, GestureDragCancelCallback? onVerticalDragCancel, GestureDragDownCallback? onHorizontalDragDown, GestureDragStartCallback? onHorizontalDragStart, GestureDragUpdateCallback? onHorizontalDragUpdate, GestureDragEndCallback? onHorizontalDragEnd, GestureDragCancelCallback? onHorizontalDragCancel, GestureForcePressStartCallback? onForcePressStart, GestureForcePressPeakCallback? onForcePressPeak, GestureForcePressUpdateCallback? onForcePressUpdate, GestureForcePressEndCallback? onForcePressEnd, GestureDragDownCallback? onPanDown, GestureDragStartCallback? onPanStart, GestureDragUpdateCallback? onPanUpdate, GestureDragEndCallback? onPanEnd, GestureDragCancelCallback? onPanCancel, GestureScaleStartCallback? onScaleStart, GestureScaleUpdateCallback? onScaleUpdate, GestureScaleEndCallback? onScaleEnd, HitTestBehavior? behavior, bool excludeFromSemantics = false, DragStartBehavior dragStartBehavior = DragStartBehavior.start})
```
参数的意义：
* child：子widget
* onTap()：单击触发
* onDoubleTap()：双击触发
* onLongPress()：长按触发

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
# 有状态的widget
无论是有状态还是无状态的widget都是不可变的，其属性的值都为final。

但是有状态的widget的状态可能在widget生命周期中发生变化，实现一个有状态的widget需要两个类：
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
生成两个类后即可在Widget中调用。
```
import 'package:flutter/material.dart';
import 'package:english_words/english_words.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    final wordPair = WordPair.random();
    return MaterialApp(
      title: 'Welcome to Flutter',
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Welcome to Flutter'),
        ),
        body: const Center(
          child: RandomWords(),
        )
      ),
    );
  }
}
```