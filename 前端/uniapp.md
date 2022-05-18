# 文章目录
## uniapp遇见的问题
### APP开发在ios中overflow不可用
在使用overflow属性的元素上添加如下代码
```
-webkit-backface-visibility: hidden;
-webkit-transform: translate3d(0, 0, 0);
```
### APP的导航栏使用了app-plus后navigationBarBackgroundColor失效
设置了app-plus后的背景颜色需要在app-plus中的titleNView设置backgroundColor属性。

注意：如果设置了style中的navigationBarBackgroundColor属性，并且设置的颜色和globalStyle中的navigationBarBackgroundColor一致，就会变成globalStyle中的navigationBarBackgroundColor颜色，否则会变成透明色。
```
{
	"path": "pages/thirdParty/constructionCompleteWorkList",
	"style": {
		"navigationBarTitleText": "盛和园项目",
		"navigationBarTextStyle": "white",
		"enablePullDownRefresh": true,
		"app-plus": {
			"titleNView": {
				"type": "default",
				"backgroundColor": "rgba(189, 116, 57, 1)",
				"buttons": [ //原生标题栏按钮配置,
					{
						"text": "筛选",
						"id": "constructionCompleteWorkList",
						"fontSize": "12px"
					}
				]
			}
		}
	}
}
```