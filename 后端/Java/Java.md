# 文章目录
## 数据证书管理工具keytool
### keytool介绍
Keytool 是一个Java 数据证书的管理工具 ,Keytool 将密钥（key）和证书（certificates）存在一个称为keystore的文件中 在keystore里，包含两种数据： 

密钥实体（Key entity）——密钥（secret key）又或者是私钥和配对公钥（采用非对称加密） 

可信任的证书实体（trusted certificate entries）——只包含公钥

### 生成签名证书
```
keytool -genkey -alias 证书别名 -keyalg RSA -keysize 2048 -validity 36500 -keystore 证书文件名.keystore
```
* -alias：设置证书别名
* -keystore：设置生成证书的文件名(可为路径，后缀必为.keystore)
* -keyalg：设置密钥的算法（RSA DSA等，默认DSA）
* -keysize：设置密钥长度（uniapp那边使用2048）
* -validity：设置有效天数（单位为天）

### 查看签名证书信息
```
keytool -list -v -keystore 证书文件名.keystore
```
* -list：显示密钥库中的证书信息
* -v：显示密钥库中的证书详细信息
* -keystore：指定要查询的证书文件名（可用路径）

### 修改keystore的别名
```
keytool -changealias -keystore 证书文件名.keystore -alias 旧别名 -destalias 新别名
```
* -changealias：修改证书别名
* -keystore：指定要查询的证书文件名（可用路径）
* -alias：输入旧别名
* -destalias：输入新别名