# 没有使用 token 导致代码上传失败

github 的代码凭证从 2021.8.13 开始就不可以使用了，必须使用个人访问令牌(token)。

创建个人访问令牌的流程如下：

1. 在 github 官网右上角点击头像并选择 Settings
2. 选择开发者设置 Developer setting
3. 选择个人访问令牌 Personal access tokens
4. 点击 Generate new token 生成令牌
5. 设置好 token 的范围和访问权限等等
6. 点击 Generate token 生成个人令牌(生成后的 token 记得保存，刷新后就不可见了)
7. 替换上传的 url 格式为 `https://<token>@github.com/<username>/<item_name>.git`
