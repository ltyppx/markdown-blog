目录
# 变量声明
# var
var可以接受任何类型变量，但其一旦赋值，变量类型就会被确定，且不能再改变。
# dynamic和Object
Object是所有dart对象的基类，所有类型的数据都可以赋值给Object，dynamic也一样，并且Object和dynamic后期都能改变对象的类型。

Object和dynamic的不同之处是Object声明的对象只能使用Object的属性和方法，而dynamic的则是所有可能都会写，要注意的是dynamic在编译器中不会报错，但是运行后可能会报错。
# const和final
const和final的特点如下：
* const和final必须拥有初始值，且只能赋值一次
* final可修饰实例变量，而const则不可以修饰实例变量
* 访问类中的const修饰的变量需要static修饰
* const修饰的List集合任意索引不可修改，final修饰的可以修改
* const在编译时会被直接替换成常量，而final则是第一次使用时才被初始化

由上述特点可知const和final的使用场景：
* final：修饰变量、修饰传递参数
* const：修饰不可改变的变量

# 空安全
dart一切都是对象，在没使用空安全时编译器不会校验是否为空，所以如果有空的变量可以为其使用'?'符号来定义可空类型 `int ?i;`。

如果预期变量不为空，但是定义时不能确定其初始值，则可以使用late关键字 `late int i;`。

如果定义的是函数变量为可空类型，则调用时可以使用语法糖让函数变量不为空时调用 `fun?.call()`。

# 函数
dart的函数也是对象，类型为Function，所以其能作为变量或参数传递。
## 函数声明
dart的函数声明没有显式声明返回值会默认作为dynamic处理，且dart的函数返回值没有类型推断。
## 函数的可选参数
### 可选的位置参数
包装一组函数参数，用'[]'标记为可选的位置参数，并放在参数列表的最后：
```
String say(String from, String msg, [String? device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
```
### 可选的命名参数
定义函数时，使用'{ 类型 命名, 类型 命名, ...}'，放在参数列表的最后：
```
// 定义
void enableFlags({bool bold, bool hidden}) {
    // ... 
}

// 使用
enableFlags(bold: true, hidden: false);
```
# mixin
Dart不支持多继承，只支持mixin，我们可以通过定义mixin，然后用with关键字组合成不同的类，如果多个mixin有同名方法，则只会使用最后一个mixin的。
```
class Person {
  say() {
    print('say');
  }
}

mixin Eat {
  eat() {
    print('eat');
  }
}

mixin Walk {
  walk() {
    print('walk');
  }
}

mixin Code {
  code() {
    print('key');
  }
}

class Dog with Eat, Walk{}
class Man extends Person with Eat, Walk, Code{}
```
# 异步支持
Dart同样支持异步操作，主要使用的是Future和Stream对象的函数，并且Dart也支持async和await关键字。
## Future
then方法来接收return出来的数据：
```
// then
Future.delayed(Duration(seconds: 2),(){
   return "hi world!";
}).then((data){
   print(data);
});
```
catchError来接收throw抛出的异常:
```
// catchError
Future.delayed(Duration(seconds: 2),(){
   throw AssertionError("Error");  
}).then((data){
   print("success");
}).catchError((e){
   print(e);
});
```
使用then的可选参数onError捕获异常：
```
Future.delayed(Duration(seconds: 2), () {
	throw AssertionError("Error");
}).then((data) {
	print("success");
}, onError: (e) {
	print(e);
});
```
whenComplete，任务无论是成功还是失败都会执行：
```
Future.delayed(Duration(seconds: 2),(){
   //return "hi world!";
   throw AssertionError("Error");
}).then((data){
   //执行成功会走到这里 
   print(data);
}).catchError((e){
   //执行失败会走到这里   
   print(e);
}).whenComplete((){
   //无论成功或失败都会走到这里
});
```
wait方法执行多个Future操作再触发then：
```
Future.wait([
  Future.delayed(Duration(seconds: 2), () {
    return "hello";
  }),
  Future.delayed(Duration(seconds: 4), () {
    return " world";
  })
]).then((results){
  print(results[0] + results[1]);
}).catchError((e){
  print(e);
});
```
Futurn和JavaScript的Promise相似，也会有回调地狱，消除的方法同样是使用多个then或者使用async/await：
```
// 多个then
login("alice","******").then((id){
  	return getUserInfo(id);
}).then((userInfo){
    return saveUserInfo(userInfo);
}).then((e){
   //执行接下来的操作 
}).catchError((e){
  //错误处理  
  print(e);
});

// async/await
task() async {
   try{
    String id = await login("alice","******");
    String userInfo = await getUserInfo(id);
    await saveUserInfo(userInfo);
    //执行接下来的操作   
   } catch(e){
    //错误处理   
    print(e);   
   }  
}
```
## Stream
Stream用来处理多个异步操作，且一个异步操作的异常不会影响其他异步操作，通常用于内容下载和文件读写等等操作。
```
Stream.fromFutures([
  Future.delayed(Duration(seconds: 1), () {
    return "hello 1";
  }),

  Future.delayed(Duration(seconds: 2),(){
    throw AssertionError("Error");
  }),

  Future.delayed(Duration(seconds: 3), () {
    return "hello 3";
  })
]).listen((data){
   print(data);
}, onError: (e){
   print(e.message);
},onDone: (){

});
```