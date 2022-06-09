文章目录

# flutter在Android Studio的配置问题
## 在模拟器启动后找不到运行的模拟器
要排查flutter的配置是否正确可以使用 `flutter doctor` 指令。

保证flutter配置里面的路径正确：

1. 查看flutter配置信息 `flutter config`
2. 设置flutter正确的配置信息
```
// 设置android studio路径
flutter config --android-studio-dir="D:\Program Files\Android\Android Studio"
// 设置android sdk路径
flutter config --android-sdk="D:\Program Files\Android\SDK"
```

实测sdk路径可以在windows的环境变量中设置，设置正确这里不设置也可以。