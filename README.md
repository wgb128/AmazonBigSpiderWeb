# 亚马逊大爬虫可视化界面Web端

[![GitHub forks](https://img.shields.io/github/forks/hunterhug/AmazonBigSpiderWeb.svg?style=social&label=Forks)](https://github.com/hunterhug/AmazonBigSpiderWeb/network)
[![GitHub stars](https://img.shields.io/github/stars/hunterhug/AmazonBigSpiderWeb.svg?style=social&label=Stars)](https://github.com/hunterhug/AmazonBigSpiderWeb/stargazers)
[![GitHub last commit](https://img.shields.io/github/last-commit/hunterhug/AmazonBigSpiderWeb.svg)](https://github.com/hunterhug/AmazonBigSpiderWeb)
[![Go Report Card](https://goreportcard.com/badge/github.com/hunterhug/AmazonBigSpiderWeb)](https://goreportcard.com/report/github.com/hunterhug/AmazonBigSpiderWeb)
[![GitHub issues](https://img.shields.io/github/issues/hunterhug/AmazonBigSpiderWeb.svg)](https://github.com/hunterhug/AmazonBigSpiderWeb/issues)


此为亚马逊BI产品网站端，没有爬虫端，这个网站端没有价值，请先启动爬虫端。

亚马逊四站BI产品分布式爬虫端见： [Full Golang Automatic Amazon Distributed crawler|spider (USA, Japan, Germany and UK) | 亚马逊四站BI产品分布式爬虫端](https://github.com/hunterhug/AmazonBigSpider)

亲爱的，请用[支付宝APP](https://auth.alipay.com/login/index.htm)先扫红包码，然后如果你想打赏的话可以用红包给我打赏<br/>

![](https://raw.githubusercontent.com/hunterhug/rabbit/master/file/red/red.png)<br/>

![](https://raw.githubusercontent.com/hunterhug/rabbit/master/file/red/red1.png)

v2.0

1. 支持用户权限控制, 精确到每个操作
2. 支持报告数据功能, 允许统计亚马逊产品UV,PV等
3. 支持多站点亚马逊爬虫数据汇聚
4. 支持Asin产品库查找
5. 支持定义类目, 控制爬虫端爬虫策略
6. 支持亚马逊商品大类数据/小类数据查询/筛选
7. 支持数据导出
8. 支持单商品历史趋势查看

此Web框架已经优化，改BUG，定制成为另外的强大的网站，见[https://www.github.com/hunterhug/rabbit](https://www.github.com/hunterhug/rabbit)

请安装Golang1.8环境和Mysql数据库，如何安装请百度。

# 文件目录
```
----conf 配置文件夹

	----app.conf 		应用配置文件
	----local_**.ini 	国际化文件

----controllers 控制器
	----admin	后台控制器
		----blog 博客模块
		----rbac 权限模块
	----home 	前台控制器

-----lib 公共库
-----file 上传文件保存地址
-----models ORM模型
	----admin RBAC主要数据库
	----blog 博客主要数据库
	----home 

----routers 路由
----static  静态文件
----views	视图
	----admin 	后台视图
		----default 默认主题
	----home 	前台视图
		----default 默认主题

----log 日志
----doc 说明文档
----test 测试文件夹
```

# 运行步骤

1.获取代码

```
go get -u -v github.com/hunterhug/AmazonBigSpiderWeb
或者
git clone https://www.github.com/hunterhug/AmazonBigSpiderWeb
```

2.配置MYSQL数据库，更改配置文件conf/app.conf中密码，将459527502改为你的密码，用户名仍然为root

```
httpport = 8080
db_host = 127.0.0.1
db_port = 3306
db_user = root
db_pass = 459527502
db_name = beauty
db_type = mysql
db_prefix = tb_
usadatadb = root:459527502@tcp(127.0.0.1:3306)/smartdb?charset=utf8
usabasicdb = root:459527502@tcp(127.0.0.1:3306)/smart_base?charset=utf8
usahashdb = root:459527502@tcp(127.0.0.1:3306)/smart_hash?charset=utf8
jpdatadb = root:459527502@tcp(127.0.0.1:3306)/jp_smartdb?charset=utf8
jpbasicdb = root:459527502@tcp(127.0.0.1:3306)/jp_smart_base?charset=utf8
jphashdb = root:459527502@tcp(127.0.0.1:3306)/jp_smart_hash?charset=utf8
dedatadb = root:459527502@tcp(127.0.0.1:3306)/de_smartdb?charset=utf8
debasicdb = root:459527502@tcp(127.0.0.1:3306)/de_smart_base?charset=utf8
dehashdb = root:459527502@tcp(127.0.0.1:3306)/de_smart_hash?charset=utf8
ukdatadb = root:459527502@tcp(127.0.0.1:3306)/uk_smartdb?charset=utf8
ukbasicdb = root:459527502@tcp(127.0.0.1:3306)/uk_smart_base?charset=utf8
ukhashdb = root:459527502@tcp(127.0.0.1:3306)/uk_smart_hash?charset=utf8
```

运行过程中如果数据库连接爆了，请编辑MYSQL配置文件，添加以下（百度可得），ulimit也需改大。

```
[mysqld]
max_connections = 15000
max_connect_errors = 6000
open_files_limit = 65535
table_open_cache = 1000
```

3.初始化基本数据库

```
go build main.go 
./main -s=1
```

以上为初始化基本数据库beauty，你还需要自行增加uk_smart_base等八个数据库以及80*4=320个Hash分表数据库，此类数据库初始化请参考[爬虫端](https://github.com/hunterhug/AmazonBigSpider)

4.运行

```
go build main.go
./main
或者
go run main.go
或者
bee run
```

5.其他设置

文件上传下载目录加权限:

```
mkdir file
chmod 777 file

mkdir file/back
mkdir file/data
```

6.使用

打开浏览器：[http://127.0.0.1:8080](http://127.0.0.1:8080)即可登录，账号密码为admin，admin

![](web.png)


# 项目约定
>RBAC权限相关的models统一放在admin文件夹，其他都放在home文件夹.
	前台控制相关的controllers统一放在home文件夹，其他都放在admin文件夹
	URL router统一M/C/A方式，该正则url需要验证权限，如rbac/public/index，其他如public/index不验证。

>登录说明
	登陆过的用户只能注销后登录，支持定义cookie登录。进入后台时验证session，session不存在则验证cookie，如果用户未被冻结，增加session，
	同时更改用户登录时间、登录IP等，cookie与登录IP绑定。

>系统时间默认数据库本地时间为东八区，北京时间。

>后台模板在views/admin，前台模板在views/home，子文件夹为主题，默认主题为default

>所有配置在conf文件夹conf/app.conf，支持国际化

>数据库数据填充在models/*/*Init.go中定义

>视图模板均放在static中

# 展示

权限控制

![](doc/rbac.png)

Asin产品库

![](doc/asin.png)

小类数据查看,筛选

![](doc/small.png)

大类数据查看

![](doc/big.png)

大类数据导出

![](doc/csv.png)

类目查看/勾选

![](doc/lei.png)

报告数据导入/查看/导出(报告数据是从亚马逊后台按天导出, 重新汇聚后可以自己掌控自己店铺的运营情况)

![](doc/report-data.png)

产品历史趋势查看

![](doc/trend.png)

更多精彩...
