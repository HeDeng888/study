### **NODEJS简介**

简介，不是一门语言，也不是JavaScript框架，也没有一个叫node.js的文件

**node.js是一个可以让JavaScript在服务器端运行的系统环境，即运行JavaScript不在依赖于浏览器**

Node.js是一个基于Chrome（谷歌）的js引擎（V8）所开发的软件程序，可以执行ECMAScript，但不支持DOM和BOM的操作

V8：是一个由Google开源的采用C++编写的高性能JavaScript和WebAssembly引擎，应用在Chrome和Node.js等中。它实现了ECMAScript和WebAssembly，运行在windows 7 及以上、macoS 10.12+以及使用x64、IA-32、ARM或MIPS处理器的Linux系统上。V8可以独立运行，也可以嵌入到任何C++应用程序中。

V8的内部组成：

Parser:解析器，负责将源代码解析成AST

Ignition:解析器，负责将AST转换成字节码并执行，同时会标记热点代码

TurboFan：编译器，负责将热点代码编译成机器码并执行

Orinoco：编译器，负责进行内存空间回收

#### 1.Node作用

是前端开发的重要工具

（1）、开发动态网站；

（2）、服务端API；

（3）、支持模块化开发；

（4）、提供包管理工具

#### 2.REPL环境

Node.js提供了一个交互式运行环境，即REPL，在命令行窗口中，输入node命令并按下回车键，即可进入REPL运行环境

在REPL运行环境中，我们可以完成: JavaScript代码的输入、解释、执行、结果输出等操作。

REPL:Read-Eval-Print-Loop,即 ：  读-计算-写-循环

退出REPL环境:连续按两下ctrl+c

##### #浏览器和Node区别

1、共同特点:解析编译环境，

2、不同点:

浏览器是客户端的运行环境;Node.js是服务端运行环境

浏览器的JS引擎不同，存在兼容性问题，Nodejs基于V8引擎稳定

浏览器可以DOM操作BOM操作，而Node.s无法使用

浏览器无法执行Node.js中的文件操作等功能

#### 3.服务器

服务器，对外提供资源服务;通过接口，或者访问地址，给用户获取信息。

一般，安装了服务器软件的电脑就是一台服务器;

在命令行中执行.js文件：node js文件路径

示例:服务器响应

```javascript
# node支持服务器API
var http = require( "http");
let server = http.createServer(function (request,response){
    //响应头对象，其中content-type表示响应内容的数据类型，text/html;charset=utf-8表示当前返回的数据类型为html，并且以utf-8编码格式返回
    res.writeHead(200, {
        'content-type ' : 'text/html;charset=utf-8'
    })
    response.write( "welcome");
    response.end();
    });
    server.listen(8888，function（) {
      console.log("服务器启动");
     });
```

### 模块化

（一）简介

模块化是前端开发重要的思想!!

模块化是指将一个复杂的项目按照一定的规则拆分成一个个模块，降低程序复杂性，提高代码重用性，方便开发。

模块具有独立作用域，保证每个功能模块的职能单一

项目开发时会使用到许多模块，模块间可能会存在依赖关系



#### 在Node中，模块的几个特点:

1）一个模块,可以是一个独立文件，也可以是一个文件夹，但都需要符合特定的要求

2）模块中提供的数据和功能，需要进行导出才能被外部所使用，

3）模块需要被其他文件使用，必须先对外暴露接口，



思考：组件是不是模块？

答：模块由组件构成的，组件不能理解为模块



### 模块的发展历史

#### 1.模块产生的原因？

传统方式出现的问题：

（1）可读性差。

（2）文件依赖高

（3）命名冲突、变量污染

（4）由于前端项目文件依赖关系，而产生了模块化

#### 2.过程

（1）AMD-require.js和CMD-sea.js

**AMD叫做异步模块定义规范**(Asynchronous  Module  Definition)，用require.config()指定引用路径等，用define()定义模块，用require()加载模块。

参考AMD   [https://github.com/]()

**CMD**公共模块定义规范(Common  Module  Definition )，用**define()**定义模块， seajs.use引用模块。

```javascript
1/使用AMD异步模块定义规范方式，定义模块化，练习导入导出功能;
# a.js
define(()=>{
    return {
        a(){
            console.log('这里是a模块中的a方法')；
        }
    }
})
#index.js
//1.传入依赖数组方式,模块作为参数;
define(['a'],(a)=>{
a.a()
});

//2.通过require实现类似cjs规范引入
define((require)=>{
    const a = require('a')
    a.a()
    });

#index.html
    <script src="https://cdn.bootcdn.net/ajax/libs/require.js/2.3.6/require.min.js" data-main=" ./js/index.js "></script>

CMD-sea.js
https://blog.csdn.net/zj1199303/article/details/70049296
https://github.com/seajs/seajs/issues/266
```

#### 3.ESM模块

Es6模块系统,是集AMD和 CommonJs之大成者。

ECMA推出了官方标准的模块化解决方案，使用**export**导出，**import**导入，编码简洁，从语义上更加通俗易懂。ES6支持异步加载模块，在编译的时候就完成模块的引用，所以是编译时才加载的。**(避免同步阻塞问题)**

**注意1：通过给script添加 type = module 的属性,就可以以ESM的标准执行其中的JS代码了**

**注意2：导入文件时必须加文件后缀**

```javascript
#  export default  模块默认导出
#  import  模块名 from 模块路径  默认引入

1、mod1.js
export default function mod( ){
    console.log( '这是mod方法')
}

2、mod2.js
import mod from './mod1.js'

3、index.html
<script></script>

#  export  模块  多导出
#  import {模块名}  from  模块路径  模块名必须等同于导出模块名  可以通过as重新命名:
```

#### 4.CommonJs规范(本章重点)!!!

1.伴随node.js，而诞生。本专题所讲解的模块都以commonJs规范为准。

2.模块就是独立的文件、或者独立的文件夹

3.每个模块内部都有一个module对象，模块中使用的方法或属性，都来自于module对象的内部属性或方法

## 定义模块

#### 1.定义模块并导出

模块具体指的是文件模块和文件夹模块

##### 1.文件模块

独立文件模块有三种形式:

**都是通过module.exports进行模块功能导出，通过require导入**

1.js文件模块，使用js语法方式进行定义，并通过module.exports进行模块功能导出

 2.json 文件模块，使用json对象定义数据，当通过require导入模块时，会自动导出定义的json数据

3.node文件模块，使用node.js编译后的二进制文件，不能自行定义

在Node.js环境中使用module.exports进行模块的导出：

在模块中都有一个module对象。



##### 2.文件夹模块

**文件夹模块，要求根目录下必须存在`index.js`或`package.json`文件，即必须有入口文件**

模块加载顺序:

1、如果存在index.js,那么优先加载index.js。

2.如果存在package.json会查找main中的入口文件!(一般都有它)

3.如果文件名和文件夹名一样，省略后缀名，那么，优先加载文件模块。

## npm第三方模块

#### 1.npm简介

全称node package manager (Node包管理工具)

1. npm是随同Node.js一起安装的包管理工具，用来安装、卸载、更新软件包/模块等，同时能够解决软件包之间的依赖关系

2. 官网:https://www.npmjs.com

   #### 2.npm用法：

   1.npm init -y：初始化项目/模块，在项目根目录生成package.json文件

   2.npm install模块名：下载并安装模块，下载后的模块文件存储在node_modules文件夹中

   3.npm install模块名@版本：下载并安装指定版本的模块，默认安装模块的最新版本

   4.npm install 模块名 -S：下载并以生产依赖的方式安装，将模块信息添加到package.json中的dependencies(**生产依赖**)

   5.npm install 模块名 -D：下载并以开发依赖的依赖的方式安装，将模块信息添加到package.json中的devDependencies（**开发依赖**)

   6.npm run 执行指定命令

   执行package.json中的scripts里面的start命令

   #### 3.全局模块nrm

   该模块为node的全局扩展模块，提供系统命令，nrm是一个npm源管理器，用于实现快速npm源地址切换。

   执行npm install nrm -g 进行全局安装：

    nrm ls：查看地址列表

   nrm use 地址名：参数切换地址

   nrm test ：参数测试速度

   