`Vue` 是基于`MVVM`设计模式
是单页面应用

## 引入Vue代码

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

## 将标签绑定为Vue

### el

指定一个选择器, 代表该元素中使用vue来渲染

```js
let app = new Vue({
    el:"#app"
})//app为标签id
```

el支持class(以点)、标签名方式

### 在标签里显示数据用双大括号

```html
<div class="#app">{{content}}</div>
<script> new Vue({
        el:"#app",
        data:{
            content:"内容"
        }
    })</script>
```

双大括号里面可以写表达式

```js
{{true?name:age}}
```



## Vue里的数据

### data

一般数据来源后端(通过ajax请求)

```js
var app=new Vue({
    el:"#app",
    data:{
        content:"内容"
    }
})
```

data里的数据可以与标签进行绑定

```html
<div id="app">{{content}}</div>
```

建议写函数形式
用脚手架需要

```js
let app = new Vue({
    el:"#app",
    data(){
        return{
            //数据
        }
    }
})
```



### methods事件

**里面存放的都是函数事件**

```js
var app=new Vue({
    el:"#app",
    data:{
        content:""
    },
    methods:{
        foo:function(){//}
    }
})
```

**methods事件**里面通过**this**可以访问到data里面的数据也可以访问到methods

```js
let app=new Vue({
    el:"#app",
    data:{
        content:"内容"
    },
    methods:{
        foo:function(){
            this.content = "更改后的内容"
        }
    }
})
```

### filters过滤

差值符号里面加上**竖线** 就是进行数据的判断
二次渲染

```html
<p v-for="item in arr" :key:"item.name">
    {{item.name | goudan}}
</p>
<script>
	let app=new Vue({
    el:"#app",
    data:{
        arr:"数据"
    },
    filters:{
        goudan(v){//这个v就是差值符号里面的item
            return  "加的东西"+v //过滤后的数据
        }
    }
})
</script>
```

### computed  简化差值符号

不能先定义在data里
将数据进行一次处理

```html
<div id="app">
    <p>{{funl}}</p>
</div>
<script>
	let app=new Vue({
    el:"#app",
    data:{
        arr:"数据"
        ,o:"bb"
    },
    computed:{
        funl(){
            return this.arr+"."+this.o
        }
    }
})
</script>
```

#### 可以写set和get

```js
computed:{
    msg:{
        get(){
        return 2
        }
        ,set(){
            this.lie ++
        }
    }
    
}
```

### 监听数据的变化watch

要先在data里面定义
监听的数据发生变化之后这个函数会触发

```js
data:{
    a:10
},
watch:{
    a(newVal,oldVale){//两个参数一个新值 一个旧值
        console.log(1)
    }
}
```



## Vue的标签方式

### v-text

```html
<div id="app" v-text="content"></div>
```

```js
let app=new Vue({
    el:"#app",
    data:{
        content:"内容"
    }
})
```

不能解析标签名，可以用字符串拼接
无论内容是什么只会解析为文本
可以用模板字符串

```html
<div id="app" v-text=`${name}`></div>
```



### v-html

```html
<div id="app" v-html="content"></div>
```

```js
let app=new Vue({
    el:"#app",
    data:{
        content:"<a helf="">内容</a>"
    }
})
```

设置元素的innerHTML
内容有html结构会被解析为标签

### v-on事件/@

v-on:事件名="方法"

```html
<input type="button" value="事件绑定" v-on:click="foo">
<input type="button" value="事件绑定" v-on:mouseenter="foo">
<input type="button" value="事件绑定" v-on:dblclick="foo">
<input type="button" value="事件绑定" v-on:click="foo">
```

```js
let app=new Vue({
    el:"#app",
    data:{
        content:"1234"
    },
    methods:{
        foo:function(){}
    }
})
```

methods里面写事件
v-on可以简写为@

#### 自定义参数和事件修饰符

在方法里面**传入参数**
v-on:click="foo(x)"

```js
let app=new Vue({
    el:"#app",
    methods:{
        foo:function(x){}//这里接受参数
    }
})
```

#### 键盘按下事件

@keydown.enter="方法"
enter回车键

```html
<div @keyup.k="方法"></div><!--按K键触发事件-->
```

可以串联修饰

```html
<div @keyup.k.enter.space="方法"></div>
```

#### @click.once只触发一次

#### 只有左键触发@click.left

#### 只有右键触发@click.right

#### 只有中键触发@click.middle

#### 阻止冒泡

```html
<div @click="方法">
    <button @click.stop="方法"></button>
</div>
```

#### 阻止默认事件

##### @click.right.prevent

```html
<div @click.right.prevent="方法"></div>
<a href="地址"  @click.right.prevent="方法"></a><!--阻止a标签跳转-->
```

传入两个事件需要传对象

```html
<div v-on="{click:方法,mouseenter:方法}"></div>
```

#### 接触事件

变相取消

```html
<div @click="ifClick && clickAdd()"></div>
<!--判断ifClick的值决定执不执行clickAdd-->
```



### v-model

设置和获取**表单元素**的值(双向数据绑定)
在表单元素里面添加v-model指令在指令里面添加data里面的数据

```html
<div id="app">
	<input type="text" v-model="content">
</div>
<script>
	let app=new Vue({
        el:"#app",
        data:{
            content:"绑定的数据"
        }
    })
</script>
```

无论是修改表单元素里的值还是数据里的值都会互相更改

### v-show

根据表达式的真假来显示或者隐藏
true表示显示
false表示隐藏

```html
<img v-show="true"><!--显示-->
<img v-show="12<11"><!--隐藏-->
```

原理是修改元素的**display**实现显示隐藏
指令后面的内容最终都会解析为布尔值
数据改变之后,对应元素的显示状态会同步更新

### v-if

根据表达式的真假来显示或者隐藏操作的是dom元素
直接删除dom元素
性能消耗比较大
如果频繁切换用v-show
为false时从dom树中移出

#### v-else

**配合v-if**使用
如果if是false  ,else就是显示
必须要**紧跟**v-if使用中间不能有东西

#### v-else-if

根据上一个v-if进行再次判断

### v-bind设置元素的属性

v-bind:属性名=表达式
可以用冒号简写:

```html
<img v-bind:src="imgSrc">
<img :src="imgSrc">
<img :class="imgClass?类名:''"><!--判断imgClass的值如果为假类名为空-->
<img :class="{类名:imgClass}">
<script>
	var app=new Vue({
        el:"#app",
        data:{
            imgSrc:"地址",
            imgClass:false
        }
    })
</script>
```

#### 更改class操作

```html
<div :class="{red:ifRed}"></div>判断ifRed的值来确定class添不添加red值
ifRed是真class就有red值
<div :class="[
             {'red':ifRed},
             'green'
             ]"></div>数组里面必须有引号不加引号就会去data里面找
```

#### style操作

```html
<div :style="{font-size:12px}"></div>
```



### v-for生成列表结构

根据数据生成列表结构

```html
<ul>
    <li v-for="(item,index) in arr"> {{index}} {{item}}</li>
</ul>
<h3 v-for="item in obj"> {{item.name}} </h3>
<div v-for="(value,key,index) in o">value{{value}}key{{key}}index{{index}}</div>value是键key是值index是序号
<script>
	var app=new Vue({
        el:"#app",
        data:{
            arr:[1,2,3,4,5],
            obj:[
                {name:"张三"},
                {name:"李四"},
                {name:"王五"}
            ],
            o:{user:"名字",age:18,sex:"男"}
        }
    })
</script>
```

li标签里item是数组的每一项 arr是数组本身
数组的长度的更新会同步到页面上去,是响应式的

#### v-key顺序绑定

根v-for一块使用

```html
<div v-for="item in arr" :key="item"></div>生成的每个div与item绑定
数组在后期进行打乱那么div也会随着数据进行移动
```

如果数据是对象数组就选取对象里面独一无二的属性

### v-once渲染单次

#### v-pre不渲染

## 全局API

### 自定义指令directive

```js
Vue.directive("goudan",(node,data)=>{//节点,数据
    //里面进行的操作
})
```

标签里面添加v-goudan
指令里面传一个名字和函数
函数里面有两个参数
绑定的节点 , 带来的数据

### Vue.set

在Vue里面操作数据**数组没办法改**其中**一个**或几个值(除了更改全部或重新赋值)
只要是数组就不行对象可以
改变数组里的其中一项

```js
methods:{
    fn(){
        Vue.set(this.arr,0,"goudan")//把arr的第0项改成goudan
    }
}
```

#### this.$set改变数组里的其中一项

```js
methods:{
    fn(){
        this.$set(this.arr,0,"goudan")//把arr的第0项改成goudan
    }
}
```

### this.$delete删除数组特定的某一项

```js
this.$delete(this.arr,1)//删除下标是1的值
```

或者用JS splice

```js
this.arr.splice(1,1)
```

### DOM更新之后进行操作nextTick

DOM进行更新之后进行操作
但是你写在那个方法里面那个才触发

```js
this.$nextTick(function(){
    console.log("DOM更新了")
})
```

### 查看版本 Vue.version

```js
console.log(Vue.version)
```



## 组件

放在new Vue之前定义组件
组件中间不要有任何的东西

### component全局组件

全局组件可以被任意组件所调用的

```js
Vue.component(
	//组件名 , 在html里面就是用这个标签来渲染 标签里面不写东西
    "goudan",//还必须一些选项参数
    {
        //对应要生成的DOM结构
        template:`<p>内容</p>`
        ,data(){//data必须是函数
            return {
                msg:""
                ,num ++
            }
        }
        ,methods:{
            add(){
                this.num ++
            }
        }
    }
)
```

#### template 生成DOM结构

生成对应的结构
但是结构只能有一个跟标签
起的名字不能与原有的标签名重复
驼峰命名的时候在标签里面用横杠显示-
**但是在组件里面不是**单词第一个大写

```js
Vue.component("goudan",{
    template:`<goudan>123456</goudan>`
})
```

```html
<div>
    <goudan></goudan>
</div>
```

### 子组件

在实例里面定义

#### components

属性就是**组件名**
根组件**可以**调用全局组件
全局组件**不能**调用根组件

#### template

```js
new Vue({
    el:"#app",
    components(){
        aaa:{//首先是用什么标签包起来
            template:`<div><p>组件</p></div>`
        }
    }
})
```

##### 在标签里面引入子组件

###### is

component标签是vue自带的

```html
<component is="aaa"></component>
<component :is="x"></component>
<script>
	new Vue({
        el:"#app",
        data:{
            x:"aaa"
        },
        components:{
            aaa:{
                template:`<div>这是组件</div>`
            }
        }
    })
</script>
```

##### template vue标签 

**不能写在**绑定**Vue实例的标签**里面

```html
<template id="f"></template>
<script>
new Vue({
    el:"#app",
    components:{
        aaa:{
            template:"#f"//和标签进行绑定
        }
    }
})
</script>
```

##### 组件之间的传值

###### 父组件给子组件传值

父组件传过去的值改变 子组件也改变

```html
<div id="app">
   <aaaa :goudan="arr"></aaaa>
</div>
```

通过绑定标签属性传值
子组件接受

###### props 子组件接受

```js
componente:{
    aaaa:{
        template:"#aaa"
        ,data(){
            return {}
        },
        props:["goudan"]//这里数组方式接受数据
    }
}
```

###### 接受可以用对象接受

```js
componente:{
    aaa:{
        temolate:"#aaa"
        ,data(){
            return {}
        }
        ,prop:{//对象非常像mongodb里面的表
            goudan:Array
            ,m:{
                type:String
                ,default:"这是默认值"
            }
            ,o:{
                type:String
                ,required:true//这个值是必须的
            }
        }
    }
}
```

###### 子组件给父组件传值 `$emit`

事件里的自定义事件传值
设置的自定义事件写在组件的标签上面

```html
<aaa @goudan="fun"></aaa>fun在父组件里写函数 ,父组件函数接受值
<script>
methods:{
    fun(){
       this.$emit("goudan",this.msg)//自定义事件名 ,传过来的数据
    }
}
</script>
```

### 绑定组件ref

```html
<h1 ref="goudan"></h1>
```

在`Vue`实例里面使用`this.$refs`获取此节点
如果在组件里使用`ref`那么`this.$refs`返回的是这个组件的实例方法

## Axios

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

引入axios的地址
必须**先导入再使用**
使用get和set方法

```js
axios.get("地址")//如果要查询具体的数值后面加上问号在添加属性名,等号属性值
    .then((response)=>{
    //请求数据成功的函数
    console.log(response)
    //response就是后端返回的数据
	})
    .catch(err=>{
    //请求数据失败的函数
	})
```

不同的地址获取的数据不同查询的方法不同
如果是表单元素(post)要在地址后面加逗号,在用对象的方式输入数值

```js
    axios.post("地址",{username:"名称"})
    .then((response)=>{
        //请求数据成功的函数
    }).catch((err)=>{
        //请求数据失败的函数
    })
```

### 组件里面调用

下载`axios`包
`npm i axios -S`

把`Axios`单独放一个`js`文件里

```js
import axios from "axios";
//配置默认的参数
axios.defaults.baseURL = 'http://localhost:3000';//默认访问地址
axios.defaults.withCredentials = true;//跨域允许携带cookie
axios.defaults.headers.post["Content-Type"] = "application/x-www-from-urlencoded";//设置post请求格式
```

使用`axios`
一种是全部引用
将所有的接口都引用

```js
export default axios
```

使用

```js
import request from '../api/index'
request.post("/articleInfo").then(data=>{console.log(data);}//articleInfo是地址
//post是请求方法
```

另一种方法是按需引用
导出的时候导出一个对象

```js
export default {
  goudan(){//标签
    return axios.post("/articleInfo")//articleInfo是地址post是请求方法
  }
};
```

使用
不支持解构

```js
import axios from '../../api';
let goudan = axios.goudan;
created() {
      goudan()
          .then(res=>{
            res.data.data;//data.data就是返回的数据
          })
    }
```

支持解构

```js
export function goudan(){
    return axios.get("地址")
}
```

使用

```js
import {goudan} from '../../api';
```





## new vue

new vue返回一个实例化后的东西

```js
let vm = new Vue({
    el:"#app",
    data:{
        content:"123"
    }
})
//
```

created渲染DOM之前执行函数

### 使用JQuery

```js
npm i jquery -S//安装jquery
```

再导入

```js
import $ from 'jquery'
//原型里添加$方法
Vue.prototype.$ = $
```

### 引入`css`文件

```js
@import url("地址")
```

### 引入`js`文件

```js
import "地址"//不用命名
```



## 脚手架

### 建议用cmd启动脚手架

```js
npm i @vue/cli -g
```

检测版本

```js
vue -V//斜杠后面是大写的v
```

### 创建

```js
vue create 项目名 //创建项目文件
```

多选 选择是空格

或者是`vue ui`一个ui界面

在js里面导入

```js
import "名字" from "地址"
```

导出

```js
export default "导出的东西"
```

### 启动项目

```js
npm run sever
```

### 打包项目

```js
npm run build
```

#### 打包注意事项

如果打包后放到路由的子路径
需要注意
在根目录创建`vue.config.js` 文件
写上如下代码

```js
module.exports = {
    publicPath:'./'
}
```

如果安装了前端路由请参照
https://www.cnblogs.com/zsg88/articles/12557862.html 进行更改

### 插槽

在你的组件写上slot标签
他不是一个正常的html标签所以插槽本身不会渲染

```html
<slot></slot>
```

使用插槽之后 组件中间可以写东西了
顺序按照设置的属性
在插槽之后用差值符号数据就是App的数据/根组件的数据
如果同个插槽显示不同内容 给插槽起名字

```html
<slot name="defalut"></slot>默认是defalut
<slot name="goudan"></slot>
<slot name="dachui"></slot>
```

显示内容用template标签

#### v-slot/#

简写是#号

```html
<template v-slot:goudan>
	<p>我是第一段内容</p>
</template>
<template #dachui>
	<p>我是第二段内容</p>
</template>
```

可以用于传值

```html
<slot :goudan="msg" :dachu="gg" name="goudan"></slot>
/////////////////////////////////使用
<template v-slot:goudan="{msg,gg}">
	<p>我是第一段内容</p>
</template>
///////////////////或者是
<template #goudan="{msg,gg}">
	<p>我是第一段内容</p>
</template>
```



## 生命周期函数

一个组件的生命周期里做的一些事情

### beforeCreate() 实例化之后 观测数据之前

### created()开始检测数据

### beforeMount()在页面即将渲染之前

在渲染和实例挂载之间 去调用子组件 完成子组件的生命周期

### mounted()实例被挂载之后

### beforeUpdate()数据更新之前

### update()数据更新之后

### activated()路由激活

```html
<keyy-alive>
	将组建写在这里 保存到缓存里面
    节省性能
</keyy-alive>
```

### deactivated()注销

上面两个需要`keyy-alive`标签才会触发

### beforeDestroy()组件消失

### destroyed()组件重新显示

## UI组件

下载

引入

```js
//全局
impot {Button} from "Vant"
Vue.use(Button)
//局部
impot {Button} from "Vant"
export default {
    components:{
        [Button.name]:Button//用它组件里面的name
    }
}
```

```js
Vue add element-ui
```



## 前端路由

需要Router

有两种
一个是默认的hash路由
一个是history
默认的路由地址上多一个#号
目的是判断是否是前端路由

history路由
路径就没有#号
但是他的路由容易跟后端冲突
比如 前端有一个/adou路由  后端有一个/adou路由 一旦刷新页面就出错
后端需要设置get路由返回一个文件

### 配置路由

先引用
在router文件里面的index引用你写的页面

```js
router = [
    path:"/",
    name:"Home",
    component:import("页面文件")
]
```

404页面就是星号 找不到路由

```js
path:"*",
name:"404"
```

然后在页面里面引入标签
to就是你跳转的链接

```html
<router-link to="/goudan">跳转</router-link>跳转的标签
<router-view/>跳转时渲染的地方
```

### 编程式路由 $router

#### push go replace

```js
this.$router.push("/")//添加一个当前的新历史 浏览记录
this.$router.go(-1)//当前页面向前访问 正数是向后
this.$router.replace("/")//替换当前浏览的记录
```

### 子路由children

在配置路由的地方需要的地方写上属性
children
是一个数组

```js
[
    {
        path:"/",
        name:"Home",
        component:""
    },{
        path:"/about",
        name:"about",
        component:"",
        children:[//拥有子路由
            {
                path:"all",
                name:"All",
                component:"文件路径"
            }
        ]
    }
]
```

渲染就跟原来的一样 
**但是**在写router-link标签的时候注意
里面的to属性浏览器里的地址怎么写你就怎么写

```html
<router-link to="/about/all"></router-link>
```

如果想默认就出现一个子路由
他的路由里面的path就为空`path:""`

在router-link标签里面的to可以进行筛选路由

```html
<router-link :to={name:"All"}></router-link>
找到路由里面name是All的路由
```

但是路由的命名时会冲突的

#### 别名

路由里面path有一个**别名**
他既可以有这个名字又可以有另一个名字

```js
{
    path:"",//在子路由里path不写意思指默认显示这个页面
    alias:"all",
    name:"All",
    component:()=>import("路径")
}
```

### 路由传参$ruote

参数在`query`里面

```js
mounted(){
    this.$route.query
}
```

#### 动态路由params

在路由里面设置

```js
{
    path:"about/:id"
}
```

请求链接的时候可以带上`about/2222`

获取用params

```js
mounted(){
    this.$route.params
}
```

## 路由是守卫

next括号里面可以写false

### 全局守卫

在**main.js里**面写

#### 全局前置守卫

**切换完成之前**

监听前端所有**路由的变化**
触发内部的**函数**
只要路由切换就**触发**函数

```js
router.beforeEach((to,from,next)=>{
    //to从哪那个路由来
    //from到那个路由去
    //next放行(相当于保安放行)
    router.path("/")
    next()
})
```

#### 全局后置守卫

**切换路由后**
没有next因为你**己经进入了**那个页面

```js
router.afterEach((to,from)=>{
    //to从哪那个路由来
    //from到那个路由去
})
```

### 局部守卫

**在路由配置里面添加**在你想要**添加**的页面

在某个**单独**的页面**设置**守卫
beforeEnter

```js
{
    path:"/about",
    beforeEnter(to,from,next){
        //to从哪那个路由来
        //from到那个路由去
    }
}
```

### 组件内的守卫

能够监听到**路由的变化**

#### 监听路由的进入

beforeRouteEnter
因为在**渲染之前**执行所以**监听不到this**
需要使用到this的话在**next里写函数**
但是注意每次进入到路由里会**重新渲染数据**

```js
data(){
    return{
        msg:0
    }
}
,beforeRouterEnter(to,from,next){
    next(vm={
        vm.msg++
    })
}
```

#### 监听路由的变化

beforeRouteUpdate
路由传入的**参数**变化触发函数

```js
data(){
    return{
        msg:0
    }
}
,beforeRouterUpdate(to,from,next){
    next(vm={
        vm.msg++
    })
}
```

#### 监听路由离开

beforeRouteLeave
离开此页面触发

```js
data(){
    return{
        msg:0
    }
}
,beforeRouterLeave(to,from,next){
    
}
```

## 路由切换动画

transition标签

```html
<transition name="goudan">
	<router-view class='dachui'/>
</transition>
```

设定一个name在style里面写样式

```html
<style>
    .dachui{
        transsition: 2s;
    }
    进入的状态
    .goudan-enter{
        进入的初始状态
        opacity:0;
    }
    .goudan-enter-active{
        进入动画过程中
    }
    .goudan-enter-to{
        进入的结束状态
        opacity:1;
    }
    离开的状态
    .goudan-leave{
        离开的初始状态
        opacity:1;
    }
    .goudan-leave-to{
        离开的结束状态
        opacity:0;
    }
</style>
```

## Vuex

多了一个store文件
相当于一个**仓库,** 存储变量
方便**组件之间**进行**通讯**

### state: 状态 

组件都能使用的一些数据
使用方法:

```html
<h2>
    {{$store.state.num}}
</h2>
<script>
	export default {
        name:"Home",
        methods:{
            fn(){//不要这么写 仓库只能使用不能更改 
                //需要更改就写 方法
                this.$store.state.num ++
            }
        }
    }
</script>
```

但是一般这个使用方法名字太长了
可以使用**computed**方法

```js
computed:{
    num(){
        return this.$store.state.num
    }
}
```

这样可以直接使用`{{num}}`来书写

如果还是麻烦可以用**vuex里的mapState**

#### mapState

他是一个**函数**需要执行
函数执行需要**传入参数** ,传入你**需要的变量** 以**数组**的形式传入

```js
import {mapState} from 'Vuex';
export default {
    name:"Home",
    computed:mapState(['num','goudan'])
}
```

mpaState执行之后**返回一个对象** ,对象**里面是你需要的数据** 但是
每个数据**是一个函数**
所以要写到**computed**里面
computed里面的**变量都是一个函数**形式

但是如果你要在computed里写自己的方法就不好写了
可以**使用**ES6的...**解构**

```js
computed:{
    dachui(){
        return 2+"";
    },
    ...mapState(['num','goudan'])
}
```

### getters

相当于computed

```js
getters:{
    goudan(state){
        return state.num +''//state是上面的vuex里的state
    }
}
```

getters和state的关系相当于computed和data的关系

### mutations 定义方法

定义操作state的方法 (里面写同步方法)

```js
mutations:{
    addN(state){
        state.num ++
    }
}
```

#### 使用方法`$store.commit`

```html
<button @click='$store.commit("addN")'>按钮</button>
```

如果觉得名字太长可以调用`mapMutations`
在mathods里面挂载

```js
mathods:{
    ...mapMutations(['addN'])
}
```

使用:

```html
<button @click='addN(2)'></button>
```

```js
mutations:{
    addN(state,n){
        state.num += n
    }
}
```

### actions 异步的方法

存放异步操作

```js
actions:{
    addAsync(context){
        new Promise(req=>{
            setTimeout(req,1000);
        }).then(()=>{
            context.commit('addN')
        })
    }
}
```

### modules  模块

将一些状态模块化
将一些定义的变量和相关的额方法写到一个对象里面

```js
const num = {
    namespaced:true,
    state:{
        num:1
    },
    mutations:{},
    actions:{}
}
```

namespaced创建一个**命名空间**
可以用一个变量名去接受他

然后添加到`modules`里面

```js
modules:{
    num:num
}
```

在导入数据的时候加上名字
`mapState('num',['num'])`



## APP里路由的变化监听

```js
watch:{
    $route(){//watch监听
        //监听route的变化
    }
}
```


