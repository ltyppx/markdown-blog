目录
- [Material控件](#material控件)
  - [MaterialApp](#materialapp)
  - [Scaffold](#scaffold)
- [布局](#布局)
  - [Stack和Positioned](#stack和positioned)
    - [Stack](#stack)
    - [Positioned](#positioned)
  - [Row和Column](#row和column)
    - [Row](#row)
    - [Column](#column)
    - [Expanded](#expanded)
- [元素](#元素)
  - [Text](#text)
  - [TextSpan](#textspan)
  - [Container](#container)
- [事件处理](#事件处理)
  - [GestureDetector](#gesturedetector)
# Material控件
Material控件用于Material应用，其从MaterialApp widget开始，底层构建了许多的widget，包括了Navigator，它管理着由字符串标识的widget栈，又称routes。

## MaterialApp
MaterialApp使用于 `runApp()` 方法中，如下：
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
MaterialApp的构造函数如下：
```
MaterialApp({Key? key, GlobalKey<NavigatorState>? navigatorKey, GlobalKey<ScaffoldMessengerState>? scaffoldMessengerKey, Widget? home, Map<String, WidgetBuilder> routes = const <String, WidgetBuilder>{}, String? initialRoute, RouteFactory? onGenerateRoute, InitialRouteListFactory? onGenerateInitialRoutes, RouteFactory? onUnknownRoute, List<NavigatorObserver> navigatorObservers = const <NavigatorObserver>[], TransitionBuilder? builder, String title = '', GenerateAppTitle? onGenerateTitle, Color? color, ThemeData? theme, ThemeData? darkTheme, ThemeData? highContrastTheme, ThemeData? highContrastDarkTheme, ThemeMode? themeMode = ThemeMode.system, Locale? locale, Iterable<LocalizationsDelegate>? localizationsDelegates, LocaleListResolutionCallback? localeListResolutionCallback, LocaleResolutionCallback? localeResolutionCallback, Iterable<Locale> supportedLocales = const <Locale>[Locale('en', 'US')], bool debugShowMaterialGrid = false, bool showPerformanceOverlay = false, bool checkerboardRasterCacheImages = false, bool checkerboardOffscreenLayers = false, bool showSemanticsDebugger = false, bool debugShowCheckedModeBanner = true, Map<ShortcutActivator, Intent>? shortcuts, Map<Type, Action<Intent>>? actions, String? restorationScopeId, ScrollBehavior? scrollBehavior, bool useInheritedMediaQuery = false})
```
参数的意义：
* Widget home：首页
* String title：应用程序的单行描述

## Scaffold
MaterialApp可以配合 `Scaffold` widget使用，其实现了基本的布局，构造函数如下：
```
Scaffold({Key? key, PreferredSizeWidget? appBar, Widget? body, Widget? floatingActionButton, FloatingActionButtonLocation? floatingActionButtonLocation, FloatingActionButtonAnimator? floatingActionButtonAnimator, List<Widget>? persistentFooterButtons, Widget? drawer, DrawerCallback? onDrawerChanged, Widget? endDrawer, DrawerCallback? onEndDrawerChanged, Widget? bottomNavigationBar, Widget? bottomSheet, Color? backgroundColor, bool? resizeToAvoidBottomInset, bool primary = true, DragStartBehavior drawerDragStartBehavior = DragStartBehavior.start, bool extendBody = false, bool extendBodyBehindAppBar = false, Color? drawerScrimColor, double? drawerEdgeDragWidth, bool drawerEnableOpenDragGesture = true, bool endDrawerEnableOpenDragGesture = true, String? restorationId})
```
参数的意义：
* PreferredSizeWidget appBar：标题栏
* Widget body：当前页面主要内容
* Widget floatingActionButton：悬浮在body上面的按钮
* FloatingActionButtonLocation floatingActionButtonLocation：设置悬浮按钮的位置，默认右下角

# 布局
## Stack和Positioned
### Stack
Stack也是存放widget的容器，不过在其里面的widget都是重叠存放的，其构造函数如下：
```
Stack ( { Key ? key , AlignmentGeometry alignment = AlignmentDirectional.topStart , TextDirection ? textDirection , StackFit fit = StackFit.loose , Clip clipBehavior = Clip.hardEdge , List <Widget> children = const <Widget>[] } )
```
参数的意义：
* List\<Widget> children
* AlignmentGeometry alignment：设置widget开始展示的位置，默认是从顶部开始
### Positioned
Stack里面的widget都是重叠的，要设置他们在Stack的位置，就要用到Positioned，其构造函数如下：
```
Positioned({Key? key, double? left, double? top, double? right, double? bottom, double? width, double? height, required Widget child})
```
参数的意义：
* Widget child
* double left、top、right、bottom：距离Stack容器左、上、右、下的距离
* double width：该widget的宽度
* double height：该widget的高度
## Row和Column
### Row
Row是在水平方向中存放widget的容器，其构造函数如下：
```
Row({Key? key, MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start, MainAxisSize mainAxisSize = MainAxisSize.max, CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center, TextDirection? textDirection, VerticalDirection verticalDirection = VerticalDirection.down, TextBaseline? textBaseline, List<Widget> children = const <Widget>[]})
```
常用参数的意义：
* List\<Widget> children
* MainAxisAlignment mainAxisAlignment：子集在横轴的对齐方式，默认为从左向右
* CrossAxisAlignment crossAxisAlignment：子集在纵轴的对齐方式，默认为垂直居中
* MainAxisSize mainAxisSize：主轴大小适配，默认宽度铺面主轴方向

### Column
Column是在垂直方向中存放widget的容器，其构造函数如下：
```
Column({Key? key, MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start, MainAxisSize mainAxisSize = MainAxisSize.max, CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center, TextDirection? textDirection, VerticalDirection verticalDirection = VerticalDirection.down, TextBaseline? textBaseline, List<Widget> children = const <Widget>[]})
```
常用参数的意义：
* children
* mainAxisAlignment：子集在纵轴的对齐方式，默认为从上到下
* crossAxisAlignment：子集在横轴的对齐方式，默认为垂直居中
* MainAxisSize mainAxisSize：主轴大小适配，默认宽度铺面主轴方向

### Expanded
Row和Column子项要想展开并填充可用空间，就要将子项包装在Expanded中，其构造函数如下：
```
Expanded({Key? key, int flex = 1, required Widget child})
```
参数的意义：
* Widget child：单个widget元素
* int flex：表示划分剩余未用区域的占比

# 元素
## Text
Text用于编写文本，其构造函数如下：
```
Text(String data, {Key? key, TextStyle? style, StrutStyle? strutStyle, TextAlign? textAlign, TextDirection? textDirection, Locale? locale, bool? softWrap, TextOverflow? overflow, double? textScaleFactor, int? maxLines, String? semanticsLabel, TextWidthBasis? textWidthBasis, TextHeightBehavior? textHeightBehavior})
```
Text默认会占满父元素的一行，且在字符串长度超出一行后会换行。

常用参数的意义：
* String data：显示的文本
* TextAlign textAlign：文本排列方式
* TextOverflow overflow：文本超出对象宽度和高度的处理方式
* TextStyle style：文本样式
* int maxLines：最多多少行触发文本隐藏

如果要更细节的处理文本的样式，可以使用 `Text.rich()` 方法，其接收参数如下：
```
Text.rich(InlineSpan textSpan, {Key? key, TextStyle? style, StrutStyle? strutStyle, TextAlign? textAlign, TextDirection? textDirection, Locale? locale, bool? softWrap, TextOverflow? overflow, double? textScaleFactor, int? maxLines, String? semanticsLabel, TextWidthBasis? textWidthBasis, TextHeightBehavior? textHeightBehavior})
```
## TextSpan
`Text.rich()` 方法可以配合TextSpan来做到文本内的字符串样式不同的效果，TextSpan的构造函数如下：
```
TextSpan ( { String ? text , List < InlineSpan > ? children , TextStyle ? style , GestureRecognizer ? 识别器, MouseCursor ? mouseCursor , PointerEnterEventListener ? onEnter , PointerExitEventListener ? onExit , String ? semanticsLabel , Locale ? locale , bool ? spellOut } )
```
常用参数的意义：
* List \<InlineSpan> children
* String text：显示的文本
* TextStyle style：文本样式


## Container
Container用于生成一个可见的矩形元素，其构造函数如下：
```
Container({Key? key, AlignmentGeometry? alignment, EdgeInsetsGeometry? padding, Color? color, Decoration? decoration, Decoration? foregroundDecoration, double? width, double? height, BoxConstraints? constraints, EdgeInsetsGeometry? margin, Matrix4? transform, AlignmentGeometry? transformAlignment, Widget? child, Clip clipBehavior = Clip.none})
```
参数的意义：
* Widget child：默认如果Container内没有child，其会占满整个屏幕，如有，则会自适应子widget大小
* Color color：背景色
* double width、height：设置宽高
* EdgeInsetsGeometry padding：设置内边距
* EdgeInsetsGeometry margin：设置外边距
* Decoration decoration：装饰矩形，会在child后
* Decoration foregroundDecoration：装饰矩形，会在child前

# 事件处理
## GestureDetector
flutter有提供检测输入手势的控件 `GestureDetector` ，该控件在一些widget也有相应的回调函数，可以自行了解，GestureDetector的构造函数如下：
```
GestureDetector({Key? key, Widget? child, GestureTapDownCallback? onTapDown, GestureTapUpCallback? onTapUp, GestureTapCallback? onTap, GestureTapCancelCallback? onTapCancel, GestureTapCallback? onSecondaryTap, GestureTapDownCallback? onSecondaryTapDown, GestureTapUpCallback? onSecondaryTapUp, GestureTapCancelCallback? onSecondaryTapCancel, GestureTapDownCallback? onTertiaryTapDown, GestureTapUpCallback? onTertiaryTapUp, GestureTapCancelCallback? onTertiaryTapCancel, GestureTapDownCallback? onDoubleTapDown, GestureTapCallback? onDoubleTap, GestureTapCancelCallback? onDoubleTapCancel, GestureLongPressDownCallback? onLongPressDown, GestureLongPressCancelCallback? onLongPressCancel, GestureLongPressCallback? onLongPress, GestureLongPressStartCallback? onLongPressStart, GestureLongPressMoveUpdateCallback? onLongPressMoveUpdate, GestureLongPressUpCallback? onLongPressUp, GestureLongPressEndCallback? onLongPressEnd, GestureLongPressDownCallback? onSecondaryLongPressDown, GestureLongPressCancelCallback? onSecondaryLongPressCancel, GestureLongPressCallback? onSecondaryLongPress, GestureLongPressStartCallback? onSecondaryLongPressStart, GestureLongPressMoveUpdateCallback? onSecondaryLongPressMoveUpdate, GestureLongPressUpCallback? onSecondaryLongPressUp, GestureLongPressEndCallback? onSecondaryLongPressEnd, GestureLongPressDownCallback? onTertiaryLongPressDown, GestureLongPressCancelCallback? onTertiaryLongPressCancel, GestureLongPressCallback? onTertiaryLongPress, GestureLongPressStartCallback? onTertiaryLongPressStart, GestureLongPressMoveUpdateCallback? onTertiaryLongPressMoveUpdate, GestureLongPressUpCallback? onTertiaryLongPressUp, GestureLongPressEndCallback? onTertiaryLongPressEnd, GestureDragDownCallback? onVerticalDragDown, GestureDragStartCallback? onVerticalDragStart, GestureDragUpdateCallback? onVerticalDragUpdate, GestureDragEndCallback? onVerticalDragEnd, GestureDragCancelCallback? onVerticalDragCancel, GestureDragDownCallback? onHorizontalDragDown, GestureDragStartCallback? onHorizontalDragStart, GestureDragUpdateCallback? onHorizontalDragUpdate, GestureDragEndCallback? onHorizontalDragEnd, GestureDragCancelCallback? onHorizontalDragCancel, GestureForcePressStartCallback? onForcePressStart, GestureForcePressPeakCallback? onForcePressPeak, GestureForcePressUpdateCallback? onForcePressUpdate, GestureForcePressEndCallback? onForcePressEnd, GestureDragDownCallback? onPanDown, GestureDragStartCallback? onPanStart, GestureDragUpdateCallback? onPanUpdate, GestureDragEndCallback? onPanEnd, GestureDragCancelCallback? onPanCancel, GestureScaleStartCallback? onScaleStart, GestureScaleUpdateCallback? onScaleUpdate, GestureScaleEndCallback? onScaleEnd, HitTestBehavior? behavior, bool excludeFromSemantics = false, DragStartBehavior dragStartBehavior = DragStartBehavior.start})
```
参数的意义：
* Widget child
* GestureTapCallback onTap()：单击触发
* GestureTapCallback onDoubleTap()：双击触发
* GestureLongPressCallback onLongPress()：长按触发