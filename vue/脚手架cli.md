# Vue高级

## 一、回顾组件化与模块化

### 1、组件化

        组件化，是从UI界面的角度进行划分的，将页面构成拆分为一个个组件，方便UI组件的重用

        组件包含：页面构成(template)、样式（css）、功能（js）

### 2、模块化

模块化，是从代码逻辑的角度进行划分的，将项目按照一定的规则拆分成一个个模块，进行组合使用

方便代码的分层开发，保证每个功能模块的职能单一

### 3、模块化和组件化的关系?

模块和组件是相互依赖的，是模块化依赖组件的模板，组件依赖模块的功能，是项目的基本组成部分。

疑问?

**为什么推荐模块化开发，而不是直接用vue.js包去新建项目?**

通过vue.js生成的项目为普通项目，该方法创建的项目很零散、代码量偏大，一般依靠后端的强大支持。

**缺点：**

       庞大，没有实现工程化，不利于压缩。

       容易出现卡顿、响应时间慢等问题。

**然而，模块化开发的优点:**

       代码逻辑清晰，有层次，易分解，解耦性好;

       保证各个模块功能单一;

       项目管理的需要。

## 二、模块化开发

### 1.1开发环境

模块化开发一般需要独立的开发环境，一般都基于Node.js和 webpack进行环境搭建

- Node.js 独立JS运行环境和模块系统支持
- webpack 是自动化的前端构建工作流的工具，属于打包工具和编译工具之一;
- 在vue中构建模块化环境

       Vue模块化项目环境搭建，可以通过官方提供的环境构建工具 Vue cLI，称为Vue脚手架

### 1.2工具预安装

```
1、安装node
    node官网; http://nodejs.cn/
    查看:node -v
    widow+R
    node管理工具
https://blog.csdn.net/qq_30376375/article/details/115877446
 
    npm      node package management.Node包管理器;国外
2、npm安装cnpm    国内镜像cnpm命令行工具
                 npm install -g cnpm registry=https://registry.npm.taobao.org

3.@vue/cli脚手架

```

### 2.Vue脚手架

**安装**：**npm install  @vue/cli -g**

#### 2.1简介

        @vue/cli是一个Vue脚手架，用来快速构建模块化项目结构

- cli: command line interface命令行接口
- 通过命令行的方式快速构建Vue模块化项目运行环境

```
安装vue-cli脚手架      npm install  @vue/cli -g   
版本查询               @vue/cli -V  等价于   vue --version
                      vue --help 

```

#### 2.2创建项目

- 创建项目: **vue create  项目名    或   vue ui**
- 为项目增加扩展插件:     vue  add  插件名

### 3.使用脚手架创建项目

切换到项目的存放目录，执行vue create项目名称，进入交互模式

### 4.启动项目  **npm run serve**

切换到项目的根目录，执行   **npm run serve**    启动开发服务器，然后根据提示url访问

npm run    命令名称  是 npm 内置的脚本执行命令，该命令会自动搜索执行目录下package.json文件中的scripts对应的命令并执行

## 三、项目结构

### 1.文件结构

通过多个关联文件构成模块化开发环境，最终由webpack工具进行打包合并

```javascript
|-项目名称
|-node_modules         #项目运行所依赖的模块，内容较多，文件较大，拷贝项目时一般不拷贝此目录，可通过npm install自动下载安装
|-public               #项目的静态资源目录，如html、css. js、 image等．服务器访问的根目录,对外公开的资源
|-index.html           #跌认访问的页面文件
|-src                  #源代码目录
|-assets               #静态资源目录,和public目录的作用相同
|-components           #自定义组件目录
|-App.vue              #项目的主组件，组件都是以vue结尾的
|-main.js              #项目的启动文件
|-.browserslistrc      #项目的浏览器适配版本
|-.eslintrc.js         #eslint配置文件,定义语法校验规则
|-.gitignore           #gi社配置文件,定义忽略文件列表
|-babel.config.js      #babel配置文件，定义ES语法转换规则
|-package-lock.json    #对项目的安装模块信息进行本地记录

|-package.json         #node项目的描述文件,定义项目的相关描述信息
                       #dependencies:生产环境、线上环境;
                       #devDependencies:开发环境;
                       
|-vue.config.js        #webpack配置                 
|-README.md            #项目的说明文件,对项目进行说明介绍
```

### 2.核心文件详解

Vue模块化项目启动时会自动查找两个核心文件:index.html和 main.js

### 2.1index.html

index.html是访问应用时默认显示的页面文件，也是Vue项目的容器定义文件

### 2.2main.js

main.js是项目的启动文件，也是Vue模块化项目的整合入口文件

```javascript
/使用ES6提供的模块导入导出功能
import模块名 from文件路径  //导入模块，模块名可自定义
//全局配置
Vue.config.productionTip = false;
/可以注册插件
Vue.use()

//实例化Vue,关联页面容器
new Vue({
render: h=>h(App)}). $mount( " #app " )
```

### 2.3单文件组件

以.vue结尾的文件，是Vue.js自定义的一种文件格式，称为单文件组件

一个.vue文件就是一个单独的组件，在文件内封装了该组件相关的html、css和js，实现了对一个组件的封装

.vue文件由三部分组成:

```javascript
<template>
    <!-- html.组件的页面结构-->
</template>

<script>
    // js，组件的功能配置
</script>

<style>
    /*css．组件的样式*/
</style>
```

### 2.4、App.vue主组件

App.vue是Vue中提供的一种特殊的组件定义文件，这类文件用于描述模块化项目中的组件

App.vue是项目的主组件，其他组件都是在该组件下加载的

vue组件以.vue为后缀名;

```javascript
1/静态资源图片加载方式,允许使用相对路径
<img alt="vue logo" src=" ./ assets/logo.png"/>
    
2/主组件中，包含其他组件;通过模块化导入方法，将其他组件引入到APP.vue中
import UserList from "./components/UserList.vue" ;

3/创建组件的方式
注意: 1、创建
      2、注册

4/可以导入第三方模块
    import "animate.css";

/通过模块化方法导入文件
     import './css/aaa.css'
     import less文件
```

### 2.5动态样式Less

less是一种动态样式寓言，可以在多种语言环境中使用，包括浏览器端，桌面移动端，服务端；

less用法：

1.less中可以通过@变量名，来定义值、选择器、url、样式属性、支持变量嵌套写法;

```javascript
1、定义选择器:@prop: color;
   p{
      @{prop} :red;
    }

2、定义属性值:@ddd : underline;
   p3{
      text-decoration:@ddd;
   }

3、定义路径:@imageurl : '../assets/ ' ;
 d1{
    background : url( '@{imageurl}logo.png ' );//路径必须用引号;
  }

4、支持嵌套规则! ! !
div{
    .par{
        .p{} 
    } 
}

```

## 四、模块化开发

包括以下几个方面:

### 1.组件样式

- 全局样式:在style标签中定义的样式，默认为全局样式，在所有组件中都有效;
- 局部样式:可以为style标签指定scoped属性，此时定义的样式为局部样式，只在当前组件中有效用法:<style scoped> ，可以定义多个style标签;
- 动态样式:为style标签指定lang属性，设置当前使用的样式语言，如: css、less、sass、scss、stylus等，用法:<style lang="动态样式语言less"> ;

注意，如果使用动态样式，可以通过配置全局插件;

### 2.配置插件

创建或编辑vue.config.is文件

```javascript
1/下载vue add style-resources-loader;
    devDependencies
        "style-resources-loader" : "^1.4.1",
        "vue-cli-plugin-style-resources-loader" : "~0.1.5",

2、全局配置通过vue.config.js
 pluginoptions: {
         'style-resources-loader " : {
           preProcessor: 'less',
           patterns:[
           '. / src/less/var.less'
           ]
      }
   }
```

    修改vue.config.js文件后，需要重启项目才生效

注:除了变量的样式文件外，其他普通样式文件都可以直接以全局样式方式引入即可

### 3.错误提示

三个地方：

- 浏览器的页面
- 浏览器的控制台
- 系统的命令行

### 4.路径问题

在style标签中定义样式指定路径时，以当前文件所在位置作为参照路径，路径会被Vue解析编译，编译后使用baseUrl值进行替换设置

```javascript
:style='{backgroundImage:"url("+require("../assets/logo.png")+")"}'
```

在img标签中通过src属性指定路径时，以当前文件所在位置作为参照路径，路径会被Vue解析编译，编译后使用baseUrl值进行替换设置

```javascript
<imgsrc="./assets/logo.png"/>
```

### 5.项目打包

      当项目要部署上线时，需要先对开发环境的项目进行打包构建操作，生成一个由纯静态文件构成的项目

     切换到项目的根目录，执行npm run build对项目进行打包构建操作

- 默认会在项目的根目录下生成一个dist目录，该目录中存放打包后的项目静态文件，可直接部署到生产环境中
- 打包后可将dist目录中的静态文件拷贝到任意Web服务器中部署运行，生产环境和开发环境;
- 由于生产环境和开发环境可能会有所不同，有时会导致资源无法访问，此时需要对环境进行配置
- 编辑vue.config.js文件

```javascript
module.exports = {
//项目的基础url，所有静态资源在加载时的基础路径BASE_URL
//publicPath:'/film/',
//判断环境，分别指定生成环境production和开发环境development的地址
publicPath: process.env.NODE_ENV === 'production'? '/film/' :'/',
//开发服务器的配置
devserver: {
     port: '8888'//使用的端口
   }，
//打包时是否生成map文件，主要用于生成环境下调试js源代码，建议改为false
   productionSourceMap: false,
}
```

## 五、全局功能定义

### 1.简介

用于统一定义全局的功能，如:全局组件、全局插件、全局过滤器、全局指令等

- 使用Vue提供的全局方法 vue.use()，一般在main.js文件中使用
- Vue.use(0bject）参数Object是一个必须提供install方法的对象，Vue.use会自动调用执行install方法

### 2.用法

```javascript
(一)全局过滤器
install()

(二）创建全局组件的方式
   ->1)定义一个全局组件;

   ->2)使用install方法将全局组件注册为全局插件，并且导出;
       export default{ install :function(Vue){
       Vue.component( ' GlobalComp ' ,GlobalComp)}}

   ->3)在main.js核心文件中，通过全局方法 Vue.use(）使用插件
                                    
   ->4）全局调用
    //import CompGiobal from './components/TimeClock.vue' 
    //vue.component('CompG1obal',CompGiobal)
                                    //(二)定义全局指令
自定义指令是什么？       
   v-“指令名字”，表示自定义指令
   vue.directive( '指令名",指令方法)
1、自定义颜色指令v-color
                                    
->1）新建一个decolor.js文件
                                    
export default {
   //el参数表示节点
     inserted(el){
   }
}       

->2)在入口文件引入。
import { 模块名 } from "./directive/index.js'

->3）在vue中注册使用
    Vue.use()

//（三）全局指令
/*自定义防抖指令*/
自定义一个v-debounce指令的过程

-->1、什么是防抖?
     防抖是通过定时器执行一个事件，在定时器时间内,用户连续去重复执行该事件，定时器会自动将事件清除,重新执行一次事件。
     优点:避免重复发送数据请求，造成页面重复加载问题，是前端重要的性能优化方法之一。

-->2、使用场景
点击搜索按钮;用户输入搜索等;

-->3、思路;
  export default{
       inserted(el,binding){
           let timer;
           el.addEventListener('click',()=>{
               if(time){
                   clearTimeout(time)
               }
            time = setTimeout(()=>{
                binding.value();
             },1000);
           })
       }
  }

（五）、全局插件main.js全局注册使用

import axios from 'axios'
Vue.prototype.$http = axios
// $http这个名字可以修改，此时在组件中无需引入axios模块，直接使用
this.$http.get()/post()调用;
this.$axios.get()
```

## 六、Vue中的数据交互

### 1.简介

Vue模块化项目的数据交互，使用的就是AJAX技术，发送异步请求

- 实现异步请求的模块有很多，官方推荐使用axios模块
- axios是一个基于Promise的HTTP请求客户端，用来发送AJAX请求

### 2.安装axios

      切换到项目的根目录，执行npm install axios --save安装模块

      在需要使用axios的文件中，通过import axios from 'axios'导入模块

      导入模块后，可以使用axios对象提供的方法:

- axios(config)                               默认
- axios.get(url[, config])                 获取信息
- axios.delete(url[, config])            删除信息
- axios.post(url[, data[, config]])    添加信息
- axios.put(url[, data[, config])       更新

       补充:Restful请求，根据HTTP请求方式来区分对资源的操作

- GET           获取资源
- POST         新建资源
- PUT           更新资源
- DELETE     删除资源  

### 3.用法

#### 3.1基本用法

      使用axios( [config])，传入相关配置项

      使用axios.get(ur1[ , config])，传参方式:

      使用axios.post(ur1[ ,data , [ config]])，传参方式:

#### 3.2全局引入

全局引入axios并添加到Vue原型中，避免在组件中重复引用axios,简化使用

- 在main.js中导入axios模块
- 为Vue函数添加一个原型属性$http,指向axios对象
- 在组件中无需再引入axios模块，直接使用this.$http即可

### 4.跨域访问

发送请求时，如果协议、主机或端口，只要有任何一个不同，则为跨域访问

两种情况:

- 生产环境跨域dev开发中，，，
- 开发环境跨域dep上线，，

#### 4.1生产环境跨域

在项目上线时，当前后端代码分别部署在不同的服务器上，此时在生产环境下存在跨越访问的问题

解决方式:

- 后端处理:设置响应头为Access-Control-Allow-Origin，允许跨越访问
- 前后端配置处理:采用JSONP模式，前端发送JSONP请求

       axios不支持jsonp，没有提供发送jsonp请求的方法，推荐使用vue-jsonp模块，步骤:

1.安装模块

       npm install vue-jsonp --save

2.导入模块

      import VueJsonp from 'vue-jsonp'

      Vue.use(Vue]sonp)

3.基本用法

this.$jsonp(url, data0bj, timeout)

```javascript
前端向蘑菇街发送跨域请求。
      1）在main.js中全局导入安装vue-jsonp模块功能
           import { Vuejsonp } from 'vue-jsonp'

2)  sendJsonp() {
     this.$jsonp( 'http://mce.mogucdn.com/jsonp/multiget/3',{
          appPlat:'m',
          pids: 140378
       })
           .then(res => {
              console.log(res);
          })
     }
```

#### 4.2开发环境跨域

      前端在开发环境下会存在跨域访问的问题

      解决方式:在前端构建代理服务器，进行请求的转发

      配置代理服务器的步骤:

1.编辑vue.config.js文件,添加代理服务器配置

```javascript
//配置代理服务器，解决开发阶段的跨域问题(只在开发阶段有效)
devServer:{
port:8080,
proxy: {
     "/toutiao" :{所有以/toutiao开头的请求都需要被代理转发
           target:" http://v.juhe.cn",
           logLevel:'debug‘,
        }
}}
```

2.重启开发服务器，查看日志输出

```javascript
1向今日头条发送新闻请求
   1) main.js中
        //5全局引入axios模块,添加为Vue构造函数的原型属性
             import axios from 'axios'
             Vue.prototype.$http = axios

   2）在.vue组件中，
   sendNews() {
          this.$http.get( " / toutiao/index"，t
              params:{
                 key: "b7cfd84383296b8284dc98ee70ac253e"
               }
         }).then(res => {
             console.log(res);
          })
      }
```

## 七、路由

联想:路由器

做什么?

将网络分发到每一户;

根据每户的位置，来匹配资源;

### 1.简介

vue组件，即SPA应用程序:Single Page Application单页应用程序，SPA

- 就是只有一个Web页面的1.应，所有的操作都在这个页面上完成（容器页面)
- 浏览器一开始会加载相应的HTML、CSS和JavaScript，然后将所有的活动都局限在该Web页面中
- 当用户与应用程序交互时通过JavaScript动态更新页面中的内容

        在开发SPA单页应用时，需要在不同的组件间切换，从而实现在一个容器页面中显示不同的内容

       根据spa单页应用程序的特性，因此，

       我们可以使用Vue Router来开发单页应用，根据不同的url地址，路由跳转到不同的组件

路由的实质：

- 路由是一种组件动态分发机制，通过url路径进行组件的切换
- 根据url路径查找对应的组件，然后将组件显示到指定的页面位置

### 2.基本用法

```javascript
vue-router.js源码地址;
    https : //www. csdn.net/tags/NtDakg2sNjgxMDgtYmxvZw0000000080.html
简而言之:
    定义路由routes
    创建路由实例new VueRouter(0)，传入路由routers
    挂载到vue根实例中，router:router

```



使用场景

创建项目时选择Router路由功能

```javascript
|-项目名称
     |-node_modules
         |-vue-router       #路由模块
  |-src
     | -router
         |-index.js         #路由配置文件
     |-views                #视图组件目录
     |-App.vue
     |-main.js
```

核心文件详解:main.js、index.js、App.vue

- 提供了两个路由组件

      `<router-link>`组件:用来定义导航，默认会创建<a>标签，根据指定的url路径跳转到组件

      `<router-view>`组件:用来渲染url路径对应的组件，将组件显示到当前定义的位置

当前激活路由的样式:

- 默认的class样式名为: .router-link-exact-active
- 样式会随着激活路由的变化而自动被定义在<router-link>标签上
- 可以通过路由配置项linkExactActiveclass重写激活样式的class类名

```javascript
new VueRouter(i
   linkExactActiveclass : "active",
});
```

### 3.路由嵌套

当应用由多层嵌套的组件构成时，需要使用嵌套路由

       关于url路径的定义:

- 根路径

       根路径就是/，默认访问项目时显示的就是根路径对应的组件，即默认显示的组件

- 嵌套路由的路径

      子级路由可以使用相对路径或绝对路径

- 通配路径

       可以使用通配符*来设置当url路径不存在时显示的组件

### 4.路由传参

     通过<router-link>的to属性传递参数

     两种方式:

#### 1.查询字符串传参

   传递参数:

- **字符串形式进行拼接**

             语法:to="路径?参数名=参数值&参数名=参数值”

- **对象形式动态绑定to，里面的qurey是对象，还可以用name名进行绑定**

             语法:   :to="{path: '组件的url路径'，query: {key : value, key : value}}”或

                      :to="{name:‘组件的路由名称’，query : {key : value,key : value}}"

       **获取参数:**

- 使用路由对象vm.$route.query 获取参数信息

#### 2.Rest风格传参

传递参数：

- **字符串形式**

语法:    to="/路径/参数/参数"     将参数伪装成请求地址的一部分

使用上面这种方法需要index.js中的参数前面加上冒号    **'  ：'**

![1656598291354](C:\Users\86132\AppData\Local\Temp\1656598291354.png)

在定义路由时需要在url路径中通过  **:参数名**   指定参数

- **对象形式**

语法:   :to="{name : '组件的路由名称', params : {key : value,key : value}}"

对于Rest风格的对象形式传参，只能使用路由名称的形式,而且**会隐藏搜索框中的信息**

      **获取参数：**

- 使用路由对象vm.$route.params 获取参数信息

### 5.路由对象

路由对象$route，表示当前激活的路由的状态信息，称为**激活路由信息对象**

- 该对象为所有组件共享的实例属性，在所有组件中都可以通过this.$route访问，且访问的都是同一个对象
- 该对象中存储着当前激活路由的相关信息

```javascript
$route.path             //当前激活路由的路径
$route.fullPath         //当前激活路由的完整路径
$route.name             //当前激活路由的名称，即命名路由的name
$route.query            //当前激活路由的字符串查询传递的参数
$route.params           //当前激活路由的rest方式传递的参数
$route.meta             //当前激活路由的元信息
```

路由元信息：   

- 在定义路由时，可以通过meta属性为当前路由指定一些自定义配置项，称为元信息
- 在组件中可以通过$route.meta获取到这些元信息

### 6.路由守卫

也称为路由导航守卫，用来对路由导航进行守卫，控制导航的跳转，可以进行权限的控制

全局前置守卫:使用router .beforeEach

```javascript
const router = new vueRouter({ ... })
//当一个导航触发时,全局前置守卫将被调用
router. beforeEach((to，from，next) =>{ 
  //to 即将要访问的目标路由对象
  // from来源于哪个路由对象
  //next是一个函数，表示下一步怎么做，如: next()表示放行，next('/login')表示跳转到/login路径
})

router.beforeEach((to,from, next)=>{
    if(to.path=== '/'){
      next()
 }
const user = sessionstorage.getItem( " user ")
  if( !user){
     next( '/')
  }
next()
})
```

全局解析守卫：

```javascript
router.beforeResolve((to,from, next)=>{
    if(to.path!='/ '){
           console.log( 路由解析');
                next()
    }
  if(to.path== '/'){
     console.log("/解析首页");
      next()
   }
})
```

全局后置钩子：

```javascript
//全局后置钩子
router.agterEach((to)=>{
    if(to.path=='/'){
        console.log('后置钩子，路由时事件发生后')；
    }else{
console.log('后置钩子，路由事件发生后。。。。。');
    }
})
```

组件内部守卫：

1、进入组件前beforeRouteEnter

```javascript{
beforeRouteEnter(to,from,next){
    console.log('进入组件前');
    next()
}
//在渲染该组件的对应路由被confirm前调用
//不能获取组件实例`this`
//因为当守卫执行前，组件实例还没被创建
```

2、离开组件前beforeRouteLeave

```javascript
//组件内部的守卫：离开当前的组件之前执行：
beforeRouteLeave(to,from,next){
    console.log('离开页面');
    let radomNum=Math.random();
    if(radomNum>0.5){
        next();
    }else{
        return false;
    }
}
```

3.更新: beforeRouteUpdate

当前组件存在更新时：

```javascript
//在一个组件内部更新的时候执行；
beforeRouteUpdate(to,from,nexte){
    console.log('更新',to,from);
    next()
}
```

路由钩子函数执行的顺序?

1  全局守卫:使用router.beforeEach( )

2  全局解析守卫:使用router.beforeResolve

3  全局后置钩子:使用router.afterEach

组件内部的钩子函数

进入当前组件前:使用beforeRouteEnter)

离开当前组件前:使用beforeRouteLeave()

当前组件更新时:使用beforeRouteUpdate()

离开旧组件之前--->进入新组件之前-->更新当前页面（有)-->全局守卫---->全局解析守卫----->全局后置钩子

### 7.路由模式

通过mode选项可以修改路由的模式

两种模式:

- hash模式（默认值)

      原理:使用HTML的锚点技术，实现路由匹配和跳转

                通过history . pushState完成url跳转,且不会重新加载页面

      缺点:在生产环境下，如果用户在浏览器中直接访问url路径，则会报错 Not Found

               所以，在生产环境下，需要后台服务器的配置支持才行（在开发环境下是没问题的)

### 8.编程式导航

        除了使用<router-1ink>组件来定义导航链接，还可以通过编写js代码，调用路由实例$router的方法来实现路由跳转，称为编程式导航

       路由实例$router，表示构建路由时的实例对象，主要用来对路由进行控制，称为路由控制对象

- 该对象为所有组件共享的实例属性，在所有组件中都可以通过this .$router访问，且访问的都是同一个对象

- 该对象中包含控制路由的相关方法

  ```javascript
  $router.push(location)   //跳转到指定页面，参数location可以为字符串或对象
  $router.forward()        //向前一步
  $router.back()           //后退一步
  $router.go(n)            //向前或后退多少步
  ```

  

  

## 八、Vuex

### 1、简介

          Vuex是一个专为Vue.js应用程序开发的状态管理模式

          采用集中式存储管理应用中所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化

          简单来说，就是用来集中管理数据的，统一维护项目中的数据状态，相当于是一个全局的数据存储对象store，在所有组件中都可以访问

           应用场景:适合于大型的单页应用程序

**原理：**

**1.组件通过Dispatch触发异步请求，通过Actions拿到数据，通过Commit提交到Mutations，然后通过Mutations更改State，最后渲染到页面中**

**2.同步组件直接提交Mutations，然后更改State，最后渲染页面**

### 2.基本用法

创建项目时选择Vuex功能

```javascript
|-项目名称
   |-node_modules
       |-vuex            #vuex
   |-src
       |-store
           |-index.js    #vuex配置文件
       |-main.js
```

Vuex的核心时store（存储），相当于是一个容器，核心概念：

- State定义属性，用来存储状态数据
- Getter定义属性，用来获取从state派生出的状态数据，类似于计算属性
- Mutation定义变化，用来改变状态数据（突变)，只能是同步操作，需要通过commit来提交变化mutations
- Action定义方法，用来改变状态数据，可以包含异步操作，类似于mutations，但mutations只能是同步操作
- Module 用来分模块组织Vuex

#### 2.1在Vuex中定义状态

配置store对象：

- 定义   state
- 定义   getters
- 定义   mutations
- 定义   actions
- 定义   modules

#### 2.2在组件中访问状态

在组件中访问store对象，两种方式:

- 方式1:通过存储对象$store访问

      存储对象$store，表示Vuex中定义的数据存储对象store，包含Vuex中的所有数据信息

      该对象为所有组件共亨的实例属性，在所有组件中都可以通过this.$store访问，且访问的都是同一个对象

```javascript
//获取state状态树中的数据
this.$store.state;
```

- 方式2：通过辅助函数访问

Vuex中提供了一些辅助函数，用于获取Vuex中的数据信息，如：

mapState()              获取state

mapGetters()          获取getters

mapMutations()      获取mutations

mapActions()          获取actions

注:需要先导入辅助函数import {mapState,mapGetters,mapActions} from 'vuex’

```javascript
新建store/index.js文件
import vue from  'vue'
import Vuex from 'vuex'
Vue.use(Vuex)

// vuex实例;
export default new Vuex.Store({
    state:{},
    getters: {},
    mutations: {},
    actions: {},
    modules: {}
})

//新建模块：
modules/user.js/product.js

user.js文件中

// import axios from 'axios'
//state状态;
const state = {
    member: '李白',
    num:4,
    leader: '杜甫'
}

//getters派发状态
const getters = {
    membName(state){
    return state.member
   }
}

// mutations处理函数（它是一个同步操作过程)
const mutations = {
// 同步，修改statesetMeb(state,nv){i
state.member=nv
},
//修改state
setLeader(state,nv){
      state.leader=nv
      console.log(nv);
     }
}

//actions处理函数（它是一个异步操作过程)

const actions ={
changeName( {commit} , name){
     setTimeout(()=>{
         commit('setMeb' ,name)
     }, 2000)
},
changLeader(icommit} ,name){
     setTimeout(()=>{
         commit( 'setLeader ' ,name)
     },2000)
//axios发送请求
   axios.get( `https://gitee.com/api/v5/user/${uid}`).then((res)=>{
       //使用commit提交mutation,
       commit('setLeader',res.data.name)
    })
  }
}
export default {
   state,
   getters,
   mutations,
   actions,
}
```



原理？

action直接修改state？

答案是否定的。

        同一个类型的action不止一个生明，在action内部有时，存在多个promise异步方法，vuex为了保证异步方法的结果，就会依次执行promise，但是多个promise的执行顺序是无法预测的，所以如果在多个action中修改同一个state，会导致state状态不明确，结果无法预测。

因此，state修改后的值有可能是错误的。

       同时，vuex作为状态管理工具，有着严格的语法规范，通过提交mutation，来统一修改state会将更加合理规范化管理数据。

#### 2.3模块化

      当应用变得非常复杂时，store对象会变得相当臃肿，store.js文件内容会非常多

      此时可以将store分成多个模块，每个模块拥有自己的state、getters、mutations、actions

- 可以根据业务分模块。如：用户数据、产品数据、购物车数据、订单数据等
- 可以根据页面分模块，如：主页数据、搜索页数据、详情页数据等

Vuex模块化的项目结构

```javascript
|-src
   |-store
       |-index.js
            |-state.js              //根级别的state
            |-getters.js            //根级别的getters
            |-mutations.js          //根级别的mutations
       |-actions.js                 //根级别的actions
       |-moudles     
            |-cart.js              //购物车模块
            |-products。js         //产品模块
```

































































