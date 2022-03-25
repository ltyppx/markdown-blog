# 文章目录
## uniapp遇见的问题
### APP开发在ios中overflow不可用
在使用overflow属性的元素上添加如下代码
```
-webkit-backface-visibility: hidden;
-webkit-transform: translate3d(0, 0, 0);
```