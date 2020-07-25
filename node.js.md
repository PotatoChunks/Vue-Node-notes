用2000至65536
不能用的端口
27017 `mongodb`占用

## node .j s是什么

是一个**后端语言**
与前端进行交互与数据库交互
创建文件删除文件
`v8`引擎
异步编程

## 黑窗口的基本命令

### `cd `进入某个文件夹

### `cd` Desktop进入计算机

### 换盘 直接输入盘符 D:

### `cls`清空

### `dir`查看当前文件的目录

### 方向键上下查看历史记录

## node的模块系统

下载别人的`node`先用`npm start`

```js
npm start
```

### 引入

`require()`

### 导出

`module.exports` 数据

```js
//引入
require("./demo")//.js可以不用写 
```

括号**传入地址**
当前目录下必须地址前面先加点
只允许**相对路径**

```js
//导出
module.exports=10//导出的数据
```

一个模块可以**导入多个** 
但一个模块只能**导出一个** 

如果导入的模块没有导出数据,**默认导出的是空对象**
而这个默认的值是`module.exports` 

而`exports`和`module.exports`是**引用**关系
也就是`module.exports`**赋值**给了`exports` 

```js
//默认程序
exports=module.exports
```

因为`module.exports`默认是个空对象所以他们两个**指向了同一个**内存地址
所以添加`exports`的属性就改变了`module.exports`的值

```js
exports.name="名字"//导出的值就带有nam属性和值
```

重复引用是没有意义
做了修改在引入会记录下修改的

### 引入原生模块

原生模块就是自带的

```js
const path = require("path")
```

### global全局变量

`node.js`里面的全局变量

```js
let a="字符串"
global.a=a
```

## 原生模块

### path路径

#### `join`拼接路径

```js
path.join("./a","b")//拼接当前目录下的a拼接上b路径
//a\b
```

#### `resolve`

方法将路径或路径片段的序列解析为绝对路径。

```js
path.resolve('wwwroot', 'static/png/', '../gif/image.gif');
// 如果当前工作目录是 /home/myself/node，
// 则返回 '/home/myself/node/wwwroot/static/gif/image.gif'
```

#### `relative`查询路径

```js
path.relative("a","b")//从a路径到b路径怎么走
```

#### `parse`分析路径

将路径格式化
路径根是什么 ,文件类型是什么 ,文件的路径是什么

```js
path.parse("c:/a/b/c/1.txt")//根是c:/文件类型text
```

#### `basename` 读取文件名

传入两个参数一个是文件的路径 一个是文件后缀(可选)

```js
path.basename('./01text.txt')//返回 01text.txt
path.basename('./01text.txt','txt')//返回 01text
```



### `http` 启动服务

```js
let http = require('http')
let server = http.createServer((req,res)=>{
    res.writeHead(200,{'Contetn-type':'text/html;charset=UTF-8'})
    res.write('<h1>Hellow</h1>')//写入
    res.end('hellow')//结束
})
server.listen(3000,'localhost')//监听端口
```



### `global`全局变量

#### `__dirname`当前文件夹的目录

一般用于拼接

```js
path.join(__dirname,"../a/b")//找出上一级的a下面的b
```

### `url`路径

目前这个方法是遗留的用里面的构造函数

#### URL全面分析地址

```js
//const url=require("url")
//let URL = url.URL
let {URL}=require("url")
new URL("https://www.baidu.com")
```

### `querystring`处理字符

#### `parse`查询字符处理成对象属性

```js
let querystring = require('querystring')
querystring.parse("a=2&b=1&c=7")//以对象形式展现出来
//{a:2,b:1,c:7}
//第二个参数是以什么分割
//第三个是链接符
//第四个 对象 maxKeys分析几个参数
```

#### `stringify`将对象转化为查询字符

```js
querystring.stringify({name:"123",age:12})//name=123&age=12
```

可以自定义分隔符

```js
querystring.stringify({name:"123",age:12},";",":")//name:123;age:18
querystring.stringify({name:"123",age:12},":",";")//name;123:age;18
```

第二个是分隔符
第三个是链接符

#### `escape` 将字符串进行编码

#### `unescape` 将字符串进行解码

### `fs`文件系统

#### `readFile`读文件

写上读取的路径文件

读文件是一个异步操作
`node`里面异步操作后面加一个函数

```js
fs.readFile("./1.text",()=>{
    //读取完成之后执行这个函数
})
```

里面的函数参数第一个写`err`
接受报错信息,以对象参数出现
如果没有错错误信息`err`为`null`

```js
fs.readFile("./1.text",(err)=>{
    if(err)return//如果报错就return
})
```

函数参数里第二个参数是内容信息

```js
fs.readFile("./1.text",(err,body)=>{
    if(err)return//如果报错就return
    console.log(body)
})
```

但是内容是文档流的形式转
要加入文件转码

```js
fs.readFile("./1.text","utf8",(err,body)=>{
    if(err)return//如果报错就return
})
```

#### 大部分异步`api`都有同步`api`

##### `readFileSync`

同步如果想知道报错信息要加上`try,catch`

```js
let data
try{
    data = fs.readFileSync("./test2.txt","utf8")
}catch(err){
    console.log(1)
}
```



#### `writeFile`写入文件

文件不存在,就**创建文件写入**
文件存在就**修改文件**
但是**没办法创建**一个**不存在的文件夹**

```js
let fs = require("fs")
fs.writeFile("地址","内容",{},(err,w)=>{}) // w 是总共的字节数
```

第一个参数是文件路径
第二个参数是写入的内容
第三个参数是选项(对象)`options`
	`encoding:`格式`"utf8"`
	`flag:"a"`是追加

第四个参数是回调函数

```js
let fs = require("fs")
fs.writeFill("./test.txt","Hello",{flag:"a"},(err)=>{})
```

#### `unlink`删除文件

第一个参数文件路径
第二个参数回调函数

```js
fs.unlink("路径",()={})
```

文件不存在报错
不能删除目录文件(文件夹)
可以自杀(自己删除自己)

#### `rename`重命名/移动

参数一:原路径
参数二:新路径
参数三:回调函数

```js
fs.rename("./test.txt","./test.md",(err)=>{})
```

**文件可以文件夹也可以移动和更改文件夹**

#### `readdir`读文件夹

```js
fs.readdir("./cs","格式(可以忽略)",(err,data)=>{})
```

以数组的形式传出来
可以遍历

#### `mkdir `创建文件夹

```js
let fs = require("fs")
fs.mkdir("./ds",(err)={})
```

#### `rmdir `删除文件夹

```js
let fs = require("fs")
fs.rmdir("./ds",(err)=>{})
```

能删除空的文件夹
**文件夹里有内容不能删除**

#### `stat`读信息

读取当前文件夹里面的信息

```js
fs.stat("./js",(err,stats)=>{})
```

返回一个**对象**
里面有一些**实例**

##### `isfile`判断是否是文件

```js
fs.stat("./js",(err,stats)=>{
    console.log(stats.isfile())
})
```

##### `isDirectory `判断是否是目录/文件夹

```js
fs.stat("./js",(err,stats)=>{
    console.log(stats.isDirectory())
})
```

#### `createWriteStream`创建可写流

创建一个可写流

```js
fs.createWriteStream("./img/1.jpg")
```



## `npm`

在文件夹里面进行控制台程序
`npm init`
添加上-y就是一路同意

### 引入包

```js
npm install 包名 -参数
```

包名, 找到自己需要的包
参数:
	`-S / --save `安装在当前项目下,生产环境(上线了也需要)
	`-D / --save-dev` 安装在当前项目下,开发环境(写代码才需要)
	`-g` 安装全局 ,一般是在`node` 安装目录

**严格区分大小写**
`nodemailer`处理邮箱的包

### 另一种引用

```js
npm i 包名
```

使用别人的包在传过来的文件里运行命令

```js
npm i
```

`node_modules` 里面记录了被人引用的包本地下载快

自己传项目的时候要删除`node_modules`

### **注意**

任何时候不能删除`package.json`

换源: 有的时候下载不顺畅需要镜像网站

```js
npm config set registry https://registry.npm.taobao.org
```

换回来

```js
npm config set registry https://registry.npmjs.org/
```

### 卸载包

将`npm `上下载的卸载

```js
npm un 包名 -参数
```

或

```js
npm uninstall 包名 -参数
```

### 更新包

跟新包

```js
npm update 包名
```

### 查看当前项目的包

```js
npm list
```

全局后面加上  -g

### 上传项目到`npm`服务器上

```js
npm publish
```

## `node `爬虫

### 后端发送请求的包`request`

导入

```js
const request = require("request")
```

请求网址是`get`

```js
request.get({
    url:"https://www.baidu.com"
},(err,res,body)=>{})
```

`err`错误信息
`res`响应相关的信息
`body`返回的数据

`body`返回的是一个字符串

返回的数据是一个字符串需要正则匹配

```js
body.match
```

将图片下载

先`request`地址在`pipe`流入一个可写流

```js
request("地址").pipe(fs.creatWriteStream(".img/1.jpg"))
```

如果不用正则的话用虚拟`dom`

`node`里的虚拟`dom`

```js
npm i jsdom -S
```

node里的虚拟`jq`

```js
npm i cheerio -S
```

原生`jsdom`

```js
const {JSDOM} = require("jsdom")
let document = new JSDOM("html代码").window
```

`jq`里的`dom`

```js
const cheerio = require("cheerio")
let $ = cheerio.load("html代码")
```

### 爬虫的特殊情况

有些网址爬出来的东西和访问的不太一样
需要请求头`Network`里面第一个文件里
有个`request Headers`里面的User-Agent
将里面的东西都带上

`request`里面的传参
对象形式

```js
request({
    method:"GET",//请求方式
    url:"",
    headers:{//存放信息
        "User-Agent":"数据"
    }
})
```

#### 另一种方法用后端访问后端

**XHR**
转换为`JSON`对象

```js
JSON.parse("数据")
```

`url`有的时候会不存在需要判断一下

```js
url && "代码"
```



## express包

关于`node http`请求

是一个函数
创建一个服务

```js
const express = require("express")
let app = express();
```

链接服务器
本地:127.0.0.1
自己的就是自己的`ip`
`https`默认端口443 
`http`默认`80`
本地的用`2000`至`65536`

### 监听端口`app.listen`

```js
app.listen(2333);
```

### 处理请求

#### 创建路由

跟路由是一个斜杠/

必须写跟路由

```js
app.get("/",()=>{})//监听根
```

比如监听`goudan`路由

````js
app.get("/goudan",()=>{})
````

路由可以写正则

```js
app.get(/^\/student\/([\d]{5})$/)
```

回调函数里面有两个参数

`request , response`
`req`是前端访问后端返回来的信息比如`cookie` , 参数 , 信息
要使用`res`去给前端返回的信息

```js
res.send("我给你返回了");//返回文字
```

`send` 固定返回304状态码

#### 自定义状态码`status` 

```js
res.status(404).send('找不到页面')
```

#### `sendFile`返回文件

要使用绝对路径

```js
res.sendFile(path.join(__dirname,"./index.html"))
```

写get前端对应的就访问get
post就访问`post` 

```js
app.post("data",()=>{})
```

#### 重定向`redirect `跳转

```js
(req,res)=>{
    //跳转到某个路由
    res.redirect("index.html")
}
```

### 中间件

帮助处理接受的信息
路由处理的函数叫中间件

```js
const app = express()
app.use((req,res)=>{})//里面的req和res和app.get里面的一样
```

里面的函数称之为中间件函数  是中间件
**所有处理请求的都是中间件**
函数里面还有一个参数next

#### next

`app.use`写在请求的上面他需要运行next才会进行下一个中间件

```js
const app = experss()
app.use((req,res,next)=>{
    res.name = "布拉"
    next()
})
```

**不能给前端send多次**
如果一个路由经过多个中间件,那么前面的中间件必须有next才会进入下一个中间件

#### 处理前端传来的参数

中间件就是处理前端传来的参数

```js
app.use(express.json());
app.use(express.urlencoded({extended:true}));//写好了next
```

`post` 传来的参数因为安全性不能直接获取,需要中间件

如果不想写就用`req.params`接受`get`参数

##### `req.query ` get接受处理好的参数

post 接受处理好的请求`req.body`

```js
app.use(express.json());
app.use(express.urlencoded({extended:true}));
app.post("/baba",(req,res)=>{
    let data = req.body;
})
```

### 脚手架

全局安装`express-generator`
`express --view=ejs` 

```js
npm i express-generator -g
express --view=ejs
node bin/www//启动项目
```

或者是 没有模板引擎的

```js
express --no-view
y
```

### Router拥有子路由

拥有子路由

```js
let app = express.Router();
app.get("/nin",()=>{})
```

使用子路由用use

```js
app.use("/tech","引入一个子路由的文件")
```

子路由也可以拥有子路由

404页面在没有next时在代码最底下写上

```js
app.use((req,res)=>{res.send("这是404页面")})
```

##### 使用中间件或者子路径是use

**注意引用文件最好用path.join方法**

### 静态文件static

设置静态文件目录

```js
app.use(express.static(path.join(__dirname,"./src")))//开放静态资源目录
```

设置了之后就会自动访问

如果设置了静态目录根路由会自动找静态资源根目录的index

**必须是静态资源的根目录**
**必须名字叫index**

静态资源目录和get访问是分先后顺序

### 多个路由的写法

#### req.params判断路由

判断路由

```js
app.get("/arr:id",(req,res)=>{
    req.params//这个就是传入的id 是一个对象
})
```

#### 设置服务状态码

```js
app.get("/arr:id",(req,res)=>{
    res.status()//自定义状态码
})
```

### 模板引擎

#### 下载ejs

ejs与express一起用
**单独**使用ejs需要引用ejs  require

如果与express一起使用时就不用引用

```js
app.set("view engine","ejs");
```

使用

```js
app.get("/",(req,res)=>{
    res.render("");//render是返回一个模板引擎
})
```

要在根目录创建一个叫views文件
而模板引擎文件后缀是ejs里面写的是html文件
写相对路径的话会自动去views找

#### 加载数据库里的数据

render里面的第二个数据

```js
app.get("/",(req,res)=>{
    //
    res.render("test",{goudan:2})//第二个必须是对象
})
```

```php+HTML
<div>
	<%= goudan %>
</div>
```

等号是直接赋值不用等号就是`js`代码

```js
app.get("/",(req,res)=>{
    let data = [//假装从数据库中拿到了数据
        {name:"名字",age:"12",sext:"女"},
        {name:"名字",age:"16",sext:"男"}
	]
    //
    res.render("test",{data})//第二个必须是对象
})
```

```ejs
<% data.forEach(item=>{ %>
	<div> <%=item.name%> </div>
	<div> <%=item.name%> </div>
	<div> <%=item.name%> </div>
<% })%>
```

`ejs`每一行都需要结束开始

如果有多个页面而且相互之间有许多相同的东西
用引用

```ejs
<%- include("文件",{参数})%>
```

将前端页面模块化

`ejs`里面的注释是

```ejs
<%#sss
```

## 数据库mongodb

mongodb
查看是否安装

```js
mongo//运行
```

### node引入包mongoose

```js
npm i mongoose -S
```

```js
const mongoose = require("mongoose");
//链接数据库服务
mongoose.connect("mongodb://localhost:27017/goudan",{useNewUrlParser:true,useUnifiedTopology:true})//必须是27017
//服务器里面也是localhost
```

`mongodb`返回一个promise可以.then

```js
mongoose
    .connect("mongodb://localhost:27017/goudan")
    .then(()=>{})
    .catch(()=>{})
```

### 在数据库里建表

```js
let Schema = mongoose.Schema;//准备建表
```

建表之前要定义好表的规则

```js
let userSchema = new Schema({
    //key 以及规则
    username : {type:String,required:true},//必须有username
    password : {type:String,required:true},
    sex : String,
    age : {type: Number,required:true}
});
```

必须拥有这个属性在后方加上`required:true`

默认值default:"你要设置的默认值"

#### 建表

规则创建好后就是建表

```js
let user = mongoose.model("user",userSchema)//userSchema这个是你创建表的规则
```

第一个参数:表名字
第二个:表规则

#### 添加数据

一般单独创建一个文件夹进行添加数据

```js
user.create({
    username:data.username,
    password:data.password
})
	.then(()=>{
    console.log("成功")
})
	.catch(()=>{
    console.log("失败")
})
```

#### 删除数据

先引用创建的表
remove  但是remove已经不怎么用了
但首先根据条件删

```js
const user = require("目录")
module.exports = (req,res)=>{
    //查找条件
    user
      .remove({_id:"32344"})//删除_id是32344的数据
      .then(()=>{})
      .catch()
}
```

##### deleteOne删除一条数据

##### deleteMany删除多个数据

#### 查找数据

##### find通过一个值查寻 多个

```js
const user = require("目录")
module.exports = (req,res)=>{
    //查找条件
    user
      .find({_id:"32344"})//_id是32344的数据
      .then((data)=>{})
      .catch()
}
```

查找出来的结果在then的形参里面
数组的形式传出来

没有返回空数组 []

不写条件就是找出所以数据

##### findOne 查找一个

对象形式传出来
返回单个数据

没有数据返回 null

##### findById 以id形式查找

条件你写的是id
所以你要知道id才能查寻

##### find与findOne的参数

参数一:conditions 查询条件
参数二:projection 返回内容的选项
参数三:options 查询配置选项
参数四: callback 回调函数

```js
user
	.find(//小于等于20
		{age:{$let:20}}
	)
```

小于$lt 
小于等于$lte
大于$gt 
大于等于$gte 
不等于$ne
指定字段的某一个$in

```js
{age:{$in:[28,20]}}//要么是28 要么是20
```

$nin 不是某一个

多个条件$or  $nor

```js
{$or[{sex:"女"},{age:"20"}]}//要么是女 要么年龄是20
```

存在某个字段 (属性)$exists

````js
{goudan:{$exists}}//查找存在goudan 字段的
````

找出数组的长度$size

```js
{hobby:{$size:3}}
```

**代码查询语句$where** 

```js
{$where:"this.hobby.length <= 3"} //hobby的数组长度长度
//this 表示数据
```

会当成代码执行 可以写 &&  ||

可以写正则

```js
{username:/[a-z]/i}
```

数组里有没有满足指定的项 $all

```js
{hobby:{$all:{"篮球"}}}
```

##### 模糊查找

```js
user.find({title:new RegExp(data,"i")})//user是你建立好的数据
//data是前端返回给后端的数据
//后面加上引号i表示不区分大小写
```

`new RegExp`是正则的构造函数

#### 改数据 , find属性

##### 需要什么属性显示

显示是1不显示是0在find第二个参数

```js
user.find(
		{age:{$lte:28}},
    	{_id:0,_v:0,sex:0}//不显示_id _v sex
	)
//--------------
user.find(
		{age:{$lte:28}},
    	{age:1}//只显示age _id除外
	)
```

##### 限制数据

###### skip跳过前面的几条数据

###### limit显示后面几条数据

###### sort以什么顺序排列  

`sort:{age:1}`整数位升序(小到大)负数降序(大到小)

```js
user.find(
		{age:{$lte:28}},
    	{_id:0,_v:0}//不显示_id _v sex
    	{skip:2,limit:3}//跳过两条 显示三条
	)
```

##### 改`updata` / `updataOne` /` updataMany`

```js
user
	.updata(
		{username:"名字"},//查询的属性 和值
    	{age:20}//age改为20
	)
	.then(d=>{})
	.catch(e=>{})
```

如果改对象 $set

```js
user
	.updata(
		{username:"名字"},//查询的属性 和值
    	{$set:{"inof.a":12}}//改inof对象里面的a属性值
	)
	.then(d=>{})
	.catch(e=>{})
```



```js
user
	.updataOne(
		{username:"名字"},//查询的属性 和值
    	{$set:{""}}
	)
	.then(d=>{})
	.catch(e=>{})
```



##### 自增 自减$inc 

值正为加 负为减

```js
user
	.updata(
		{username:"名字"},//查询的属性 和值
    	{$inc:{age:1}}//age 自增1
	)
	.then(d=>{})
	.catch(e=>{})
```

删除某一个属性 $unset

```js
{$unset:{age:0}}
```

### 验证

#### 自己设施报错信息 required

```js
let userSchema = new Schema({
    username:String,
	age:{trpe:Nummber,required:[true,"报错信息"]}
})
```

#### 限制数据的大小 min/max

```js
let userSchema = new Schema({
    username:String,
	age:{trpe:Nummber,required:true,min:0,max:109}//min最小 max最大
})
```

#### 限制枚举属性enum

```js
let userSchema = new Schema({
    username:String,
	age:{trpe:Nummber,required:[true,"报错信息"]}
    sex:{type:String,enum:["男","女"]}//要么是男要么是女
})
```

#### 最大/小 长度  minlength/maxlength

```js
let userSchema = new Schema({
    username:String,
    password:{type:String,minlength:6,maxlength:12},
	age:{trpe:Nummber,required:[true,"报错信息"]}
})
```

#### 满足正则规则 match

```js
let userSchema = new Schema({
    username:String,
    password:{type:String,match:/^[a-z]\w{5,11}$/i},
	age:{trpe:Nummber,required:[true,"报错信息"]}
})
```

#### 自定义验证 validate

返回一个布尔值

```js
let userSchema = new Schema({
    username:String,
    password:{type:String,validate:{
        validator:(value)=>{//value是输入的数据
            return ()
        },
        message:"验证失败的错误信息"
    }},
	age:{trpe:Nummber,required:[true,"报错信息"]}
})
```

### 中间件 userSchema

#### userSchema.pre

```js
userSchema.pre("find",function(next){
    console.log("在find之前");
    next()
})
```

#### userSchema.post

```js
userSchema.post("find",function(doc){
    console.log("在find之后");
    //doc就是返回的东西
})
```

存储是save

当你想存储数据中的id时用Types.ObjectID

```js
author:{type:Schema.Types.ObjectID}
```

#### 表关联

```js
let userSchema = new Schema({
    username:String,
	author:{type:Schema.Types.ObjectID}
    content:{type:String,ref:"关联的表"}
})
//----------------------
user
	.populate("关联的表")
	.then(d=>{})
	.catch()
```

### 后端记忆功能token

#### 安装包express-session

功能是判断用户是否登录了

```js
//添加session中间件
let app = express()
app.use(session({
    secret:"eee"//秘钥, 一个字符, 用于加密, 不用自己解密可以自己随便写
    ,cookie:{maxAge:10*60*1000}//给前端设置的cookie有效时间:10分钟
    ,rolling:true //用户和页面交互的时候刷新cookie时间
    ,resave:false //是否每次重新存储session
    ,saveUninitialized:false //初始化
//不需要的可以不用写
}))
```

在数据库比对里面进行的操作

```js
user.findOne({user:data.pwd})//data是数据库里的数据
	.then(d=>{
    	//d是前端发过来的数据
    	//判断
    	req.session.goudan = true//在合适的位置添加一条属性
		//可以在别的路由进行判断
	})
```

#### 将数据库session存到数据库里

```js
npm i connect-mongo -S//下载这个包
```

以防自己的服务器满了

##### 引入connect-mongo

一般不直接使用 而是执行

```js
const sessionMong = require("connect-mongo")("session")
```

在session中间件里面添加属性

```js
//添加session中间件
let app = express()
app.use(session({
    secret:"eee"//秘钥, 一个字符, 用于加密, 不用自己解密可以自己随便写
    ,cookie:{maxAge:10*60*1000}//给前端设置的cookie有效时间:10分钟
    ,rolling:true //用户和页面交互的时候刷新cookie时间
    ,resave:false //是否每次从新存储session
    ,saveUninitialized:false //初始化
	,store:new sessionMong({//添加中间件
        url:"mongdb://localhost:27017/test"//设置添加到的路径
    })
}))

```

#### 删除session的状态

```js
(req,res)=>{
    req.session.destroy();//销毁session状态
    res.redirect("/")//重定向到根目录去
}
```

### 上传图片`multer`包

在网页里面的上传文件
要`multer`函数

```js
const multer = require("multer")
let upload = multer({
    dest:"../state/img"//存在硬盘里的目录
    ,fileFliter(req,file,cb){
        //限制上传的文件
        //file当前上传上来的文件
        cb(null,"布尔值")//false不上传, true上传
    },
    limits:{//限制文件的大小
        fileSize:1024*1024//1Mb
    }
}).single("file")//单个文件/图片
```

在数据里面

```js
(req,res)=>{
    upload(req,res,function(err){
        
    })
}
```

保存到磁盘

```js
let storage = multer.diskStorage({
    //存储位置目录
    destination:function(req,fill,cb){
        cb(null,path)//path 是路径
    }
})
```

## `formidable` 上传文件

需要结合`http` 
`const formidable = require('formidable')`

```js
const server = http.createServer((req,res)=>{
  if(req.url === '/upload' && req.method.toLowerCase() === 'post'){//判断路由
    const form = formidable({ multiples: true });//必须写

    form.uploadDir = "./uploads"//上传的路径s

    form.parse(req, (err, fields, files) => {
        //这里上传成功
      res.writeHead(200, {"Content-type":"text/plain"})
      res.end(JSON.stringify({ fields, files }, null, 2));
    });
  }
})
```



## `svg-captcha` 

### 登录验证码包

`npm i scg-captcha -S`

```js
const svgCaptcha = require("scg-captcha")
svgCaptcha.create()//返回一个对象
```

## 进度条的包

### `nprogress`  

`npm i nprogress -S`

全局导入

```js
import nprogress from "nprogress"
import("nprogress/nprogress.css");//导入css
router.beforeEach((to,from,next)=>{//路由守卫
    nprogress.start();
    next()
});
router.afterEach(()=>{
    nprogress.done()
})
```

## `crypto`密码加密

```js
const crypto = require("crypto")

crypto.createHash("sha256").update(pwd).digest("hex")//pwd是密码
```

## 长轮询`WebScoket`

### `ws` 

导入`ws` 模块

```js
const webSocket = new ws.Server({port:3000})//监听端口
```

服务器建立响应

```js
webSocket.on('connection',(w)=>{
  w.on('message',message=>{
    console.log('客户端发送过来的数据'+message);
    w.send("我接受到了信息-服务端")
  })
})
```

在前端使用`WebSocket` 

```js
let ws = new WebSocket('ws://localhost:3000')
```

open链接成功
message向服务器接受和发送消息
close链接关闭

### `socket.IO` 

下载这个模块之后自带一个`socket.io`客户端
客户端引入`/socket.io/socket.io.js`
全局暴露一个`io`属性
