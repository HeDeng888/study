### vue基础：

#### 1,Vue 的基本认识:

​      1.0，官网:

​		1) 英文官网: https://vuejs.org/ 

​		2) 中文官网: https://cn.vuejs.org/



​      1.1，介绍描述:

​	         1) 渐进式 JavaScript 框架.

​		 2) 作者: 尤雨溪(一位华裔前 Google 工程师).

​    		 3) 作用: 动态构建用户界面.

​         

​       1.2，Vue 的特点:

​		 1) 遵循 MVVM 模式.

​		 2) 编码简洁, 体积小, 运行效率高, 适合移动/PC 端开发.

​		 3) 它本身只关注 UI, 可以轻松引入 vue 插件或其它第三库开发项目 .

​     

​       1.3，与其它前端 JS 框架的关联 

​		1) 借鉴 angular 的模板和数据绑定技术

​		2) 借鉴 react 的组件化和虚拟 DOM 技术

​      

​       1.4，Vue 扩展插件

​		1) vue-cli: vue 脚手架 

​		2) vue-resource(axios): ajax 请求 

​		3) vue-router: 路由 

​		4) vuex: 状态管理 

​		5) vue-lazyload: 图片懒加载 

​		6) vue-scroller: 页面滑动相关 

​		7) mint-ui: 基于 vue 的 UI 组件库(移动端) 

​		8) element-ui: 基于 vue 的 UI 组件库(PC 端)



#### 2，Vue的基本使用

​	2.1,案例编码：

​		<div id="app"> 

​			<input type="text" v-model="username"> 

​			<p>Hello, {{username}}</p> 

​		</div> 

​		<script type="text/javascript" src="../js/vue.js"></script> 

​		<script type="text/javascript"> 

​			new Vue({ 

​				el: '#app', 

​				data: { 

​					username: 'atguigu' 

​					} 

​				{

​			}) 

​              </script>

​     

​     # 注意：现在的这种写法是单纯的用来练习知识点使用，每一个案例都需要创建一个Vue对象



​	

​       2.2，理解 Vue 的 MVVM	 



​       MVVM：是一种前端设计遵循的模式。

​		M：Model数据源。

​		 V： 页面的视图。

​		 VM：是一个vue的实例对象用来接收Model和处理View分发请求。

#### 3.模板语法

Vue模板语法有2大类:

##### 1.插值语法:

语法:{{}}由两对大括号组成，称为"Mustache"语法

作用:用于在页面标签中插入值，进行数据的绑定显示，且当值发生变化时,标签会重新渲染加载，即实现了数据状态同步操作，称为*响应式特性*。

共性:**响应式实时变化（**页面排版、宽度、数据模型，都能适用其中)

插值表达式的用法:<标签>{{变量|JS表达式|JS内置对象}}</标签> 只能用在标签中间的内容位置 

插值表达式可以绑定三种数据: 

a.Vue对象的数据仓库中的变量

b.简单的JS表达式

c.JS内置对象

插值表达式的内部原理:

Vue底层调用的是DOM对象的textContent属性向标签中插入内容，作用与DOM中的innerText、inertHtml类似



```
  第一种写法
  const x = new Vue({
    el: '#root',
    //data的对象式
    data: {
      name: 'world',
      text: '请输入'
    }
  })
  
    //第二种写法
  const vm = new Vue({
  //data的函数式，组件必须要用
    data() {
      return {
        name: 'world',
        text: '请输入'
      }
    }
  })
  vm.$mount('#root')
```

功能:用于解析标签体内容。

写法:xxx，xxx是js表达式，且可以直接读取到data中的所有属性。

##### 2.指令语法:

功能:

用于解析标签（包括:标签属性、标签体内容、绑定事件.....）。

举例:

 v-bind :href="xxx”或简写为:href="xxx"，xxx同样要写js表达式，I|且可以直接读取到data中的所有属性。

备注：vue中有很多指令，且形式都是v-？？？形式

##### 1.v-text 

只能渲染文本，不能解析内容 

##### 2.v-html 

可以渲染文本，可以解析内容，节点也可以解析渲染出来 

##### 3.v-if(重点)

写法:

(1).v-if="表达式"

(2).v-else-if="表达式”

(3) ,v-else="表达式"

适用于:切换频率较低的场景。

特点:不展示的DOM元素直接被移除。

注意:v-if可以和:v-else-if、v-else一起使用，但要求结构不能被"打断”。

**template：模板，套在内容外面，不会破坏结构，只能配合v-if使用**

##### 4.v-show(重点)

写法:v-show="表达式"

适用于:切换频率较高的场景。通过css的display属性，控制元素的显示或隐藏，

 取值：取值为any类型，任意值，如果将该值转为布尔值，true,那么就会显示当前元素，0、空字符串、null、undefined,false 都会转为false,=>隐藏元素除了以上，其他都是true,

特点:不展示的DOM元素未被移除，仅仅是使用样式隐藏掉

3.备注:使用v-if的时，元素可能无法获取到，而使用v-show一定可以获取到。

##### 5.v-pre

写法:v-pre(后面没有取值)

作用：跳过当前元素和子元素的编译过程，不对vue语法进行编译执行

##### 6.v-once

写法：v-once（后面没有取值)

作用：对当前元素和子元素的vue功能只执行一次

##### 7.v-cloak

写法：v-cloak（后面没有取值）

作用：在vue实例构建完成前，隐藏未编译的vue语法，**需要配合css样式一起使用**

css样式如下：[v-cloak]{

​	display:none;

}

##### 8.v-for

取值：对象，数组，数字，字符串

1. v-for循环对象时，第一个参数是属性值， 第二参数是属性名；

2. v-for循环数字时，第一个参数是：依次循环所有的数字,第二个参数表示索引；

3. v-for循环字符串时，第一个参数是：依次循环所有的字符, 第二个参数表示索引；

4. v-for循环数组时，第一个参数是：依次循环所有内容, 第二个参数表示索引；

   **注意：**

   当更新v-for渲染的元素列表时，默认是'就地更新'每个元素的内容，效率高，但无法跟踪每个节点的身份。

   解决办法：可以为每一项提供一个唯一的key属性，更新时元素会移动位置，能够跟踪每个节点的身份，从而重用和重新排序现有元素（推荐 ）   

##### 9.v-on

v-on事件监听指令：

​        绑定事件，触发一下操作功能

​        v-on:click=“事件名”

例如：v-on="{'mouseover':over,'mouseout':out,'click':kit}" 

​        如果方法中没有参数，那么，函数名()小括号可以省去，

​        简写：@事件名=方法名,例如：@click="方法名"

##### $event:

事件对象，不同于js

​        $event.target：事件源、节点

​        $event.target.value，获取节点的值；相当于value属性值

​        this:windows

例如：<input type="text"  @input="getEvent($event.target.value)"> 

##### 按键修饰符：

​      事件名.修饰符

​      可以写多个

​      系统修饰键（ctrl/shift/alt）+普通修饰符(a，b,n,)，必须同时触发

例如：<input type="text" @keyup.enter="KEYDOWN($event)"> 

#### 4.数据绑定

##### **1.v-bind:**

**单向绑(v-bind):数据只能从data流向页面。**

**简写：       ：value=''**

单项数据绑定：<input type="text" v-bind:value="text"> 

绑定多个属性：{属性名1：属性值1，属性名2：属性值2 } 

1.普通属性 ：

<img v-bind:src="urls" alt=""> 

2.boolean类型属性 

<input type="radio" name="user" :checked="flag"> 

3.绑定class类选择器属性 

<p v-bind:class="aaa">安徽省合肥市</p> 

<input type="text" :class="{ok:flag,error:!flag}"  @input="getVal($event.target.value)"> ok是类名，写在style里面的

4.绑定style属性 

<p :style="linestyle">今天是6月16日</p> 

##### **2.v-model：**

**双向绑定(v-model):数据不仅能从data流向页面，还可以从页面流向data.**

**简写：   v-model=''**

**原理**：vue将模型数据，渲染到页面中，基于数据劫持Object.defineProperty，  当页面发生变化时，通过事件监听，触发JsDOM操作，更改了模型，从而实现了双向数据绑定；即响应式效果。

双项数据绑定：<input type="text" v-model:value="text"> 

备注：

1.双向绑定一般都应用在表单类元素上(如:input、 select等)

2.v-model:value 可以简写为v-model，因为v-model默认收集的就是value值。

**不同input表单对应：**

单选框：v-model单选框中，绑定单选框的value值时，表示选中状态

多选框  v-model在多选框中，所绑定的数据，就是多选框被选中的value值所组成的数组；

下拉列表:  v-model所绑定的数据是下拉列表选中的每项对应的value值;

注意：多选框的data初始值如果是空，那所有的选框都同步，一般适用于一个选框，初始值为数组，可以实现每个选框的选中



###   指令总结(重点提问)

- **v-if:根据表达式的真假来插入和删除元素**
- **v-else指令为v-if添加一个"else块”**
- **v-show:控制切换一个元素的显示和隐藏**
- **v-on:为 HTML元素绑定事件监听**
- **v-model:将用户的输入同步到视图上**
- **v-bind:绑定 HTML元素的属性**
- **v-for:遍历data中的数据，并在页面进行数据展示**
- **v-pre:跳过当前元素和子元素的编译过程，不对vue语法进行编译执行**
- **v-cloak:在vue实例构建完成前，隐藏未编译的vue语法,需要配合css样式一起使用**
- **v-once:对当前元素和子元素的vue功能只执行一次**
- **v-text:更新元素的textContent**
- **v-html:更新元素的innerHTML**

共性：响应式特性。指令无痕迹特性

### 响应式原理

{{ }}、v-,model等指令响应式特性。

响应式的概念:实际上就是所谓的数据状态同步操作，当内存中变量数据发生变化时，页面会及时做出响应，进行页面重构渲染

响应式的基础:0bject.defineProperty(obj，prop，descriptor)用于定义一个对象上的属性以及这个属性的描述符

- obj  : 操作的目标对象
- prop  :  操作的属性名称
- descriptor  :  属性的详细定义

get (function):拦截属性的取值操作，为取值操作提供扩展功能

set(function):拦截属性的赋值操作，为赋值操作提供扩展功能

响应式的原理:

- 数据劫持
- 使用Object.defineProperty()实现，称为JS的数据劫持

![1655389072371](C:\Users\86132\AppData\Local\Temp\1655389072371.png)

注意：Vue不支持IE8以及更低版本浏览器

#### 5.MVVM和MVC模型

##### 1.MVVM框架

![1655104562045](C:\Users\hd\AppData\Local\Temp\1655104562045.png)





M  模型（model）：对应data里面的数据

V  视图（view）：模板

VM 视图模型（ViewModel）：Vue实例对象

观察发现：



1.data中的所有属性，最后都出现在了vm身上

2.vm身上所有的属性及vue原型上的属性，在vue模板中都可以使用

前端框架的重要的底层设计思想。编写代码、视图展示、数据响应的参考依据。

Model - View - ViewModel 模型-视图-视图模型

核心内容：

Model模型（数据）:构成页面内容的相关数据

View视图:展示数据的页面

ViewModel视图模型:介于模型和视图之间，它是连接view和model的桥梁，也是mvvm设计模式的核心思想。

为什么要使用MVM模型?

实现MVVM设计思想的**框架优点:**

- 开发者几乎不用操作DOM就可以完成页面和数据的关联交换
- 基本上都高度封装了view-model的交互过程，完成对DOM功能的封装
- 开发者**只需关心页面的构成和数据的构成**，无需关心页面和数据的状态关系
- **Vue、React、Angular**等就是实现MVVM设计思想的前端框架（典型代表: **vue**）

##### 2.MVC框架

模型（Model) :数据

视图(View) :用户界面

控制器(Controller） :业务逻辑

#### 6.obj.defineProperty

Object.defineProperty(person, 'age', {

​    // value: 30,

​    // enumerable: true,//控制属性是否可以枚举

​    // writeable: true,//控制

​    // configurable: true,

 

​    //有人读取person值时

​    get() {

​      console.log('有人读取数据了')

​      return num

​    },

​    set(value) {

​      console.log('有人修改数据了')

​      return num = value

​    }

  })

#### 7.vue中的数据代理

![1655120213140](D:\1前端\vue\文件\vue课件\课件\vue相关备课资料图\1655120213140.png)

通过vm对象来代理data对象中属性的操作(读/写)

2. Vue中数据代理的好处:

更加方便的操作data中的数据

3.基本原理:

通过object.defineProperty()把data对象中所有属性添加到vm上。为每一个添加到vm上的属性，都指定一个getter/setter。

在getter/setter内部去操作（读/写）data中对应的属性。

#### 8.事件处理

事件的基本使用:

1.使用v-on :xxx或@xxx绑定事件，其中xxx是事件名;

2.事件的回调需要配置在methods对象中，最终会在vm上;

3.methods中配置的函数,不要用箭头函数!否则this就不是vm了;

4.methods中配置的函数，都是被Vue所管理的函数，this的指向是vm或组件实例对象;

5.@click="demo”和@click=demo(event)”效果一致，但后者可以传参;

#### 9.事件修饰符

1.prevent:阻止默认事件（常用）；

2.stop:阻止事件冒泡（常用）;

3.once:事件只触发一次（常用）;

4.capture:当一个元素上的事件触发时，事件从页面的根元素开始，往下直到事件目标元素，这一过程称为事件捕获;

5.self:只有event.target是当前操作的元素时才触发事件;

6.passive:事件的默认行为立即执行，无需等待事件回调执行完毕;

v-model修饰符：

7.lazy:懒加载,一般用在表单中，类似于change，状态改变时才显示数据

8.number：一般用在表单中，改变输入框的值类型例如：v-model.number

9.trim :一般用在表单中,清除开头结尾的空格

#### 10.键盘事件

1.Vue中常用的按键别名：

回车=> enter

删除=> delete（捕获"删除”和“退格”健)

退出=> esc

空格=> space

换行=> tab(特殊，必须配合keydown去使用)

上 => up

下=> down

左=> left

右=> right

2.Vue未提供别名的按键，可以使用按健原始的key值去绑定，但注意要转为kebab-case（短横线命名)

3.系统修饰键（用法特殊）: ctrl、 alt、 shift、 meta

​	(1).配合keyup使用:按下修饰键的同时，再按下其他键，随后释放其他				   	键，事件才被触发。

​	(2).配合keydown使用:正常触发事件。

4.也可以使用keyCode去指定具体的按键（不推荐)

5.Vue.config.keyCodes.自定义键名=键码，可以去定制按键别名

#### 11.计算属性computed

计算属性（computed）也是用来存储属性数据的，但具有以下特点:

1）该函数必须有返回值，用来获取属性

2)可以对数据进行逻辑处理操作，实现数据包装

3)计算属性通常依赖于当前Vue对象中的普通属性，

4)当依赖的普通属性发生变化时计算属性也会变化，实现数据监控（比如方向盘变化，车轮也会转动方向)

5)计算属性由两部分组成:

get用来获取计算属性.

set用来设置计算属性

6)默认计算属性只有get，如果需要set，可以自己添加，此时需要以对象的形式配置

1.定义:要用的属性不存在，要通过已有属性计算得来。

2.原理:底层借助了objcet.defineproperty方法提供的getter和setter.

3.get函数什么时候执行?

(1).初次读取时会执行一次。

(2).当依赖的数据发生改变时会被再次调用。

4.优势:与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。

5.备注:

1）.计算属性最终会出现在vm上I直接读取使用即可。

2）.如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生i

```
  <div id="root">
    <p>姓：<input type="text" v-model="firstName"></p>
    <p>名：<input type="text" v-model="lastName"></p>
    <p>姓名：{{firstName.slice(0,3)+'-'+lastName}}</p>
    <p>姓名：{{fullName()}}</p>
    <p>姓名：{{fullName2}}</p>
  </div>
  
   Vue.config.productionTip = false;
  const vm = new Vue({
    el: '#root',
    data() {
      return {
        firstName: '张',
        lastName: '三'
      }
    },
    methods: {
      fullName() {
        // console.log(this)
        return this.firstName.slice(0, 3) + '-' + this.lastName
      }
    },
    computed: {
      //完整写法
      // fullName2: {
      //   //读取数据
      //   get() {
      //     return this.firstName.slice(0, 3) + '-' + this.lastName
      //   },
      //   //如果有修改的情况
      //   set(value) {
      //     let arr = value.split('-');
      //     this.firstName = arr[0];
      //     this.lastName = arr[1]
      //   }
      // }
      //如果确定只会用get，不会用set,可以简写
      fullName2() {
        return this.firstName.slice(0, 3) + '-' + this.lastName
      }
    }
  }
  )
```

#### 12.监视属性watch:

##### 监视属性：

1.当被监视的属性变化时,回调函数自动调用,进行相关操作

2.监视的属性必须存在,才能进行监视!!

3.监视的两种写法:

(1).new Vue时传入watch配置

(2).通过vm.$watch监视

**immediate: true,//初始化的时候先调用handler**（简写不可用）

##### 深度监视:

(1).vue中的watch默认不监测对象内部值的改变

(2).配置deep:true可以监测对象内部值改变（多层）。（简写不可用）

备注:

(1).Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以!(2).使用watch时根据数据的具体结构,决定是否采用深度监视。

```
 <div id="root">
    <p>今天天气很{{info}}</p>
    <button @click="change">切换天气</button>
    <p>数字为：{{nums.a}}</p>
    <button @click="num">点我</button>
  </div>
  
  Vue.config.productionTip = false;
  new Vue({
    el: '#root',
    data() {
      return {
        isHot: true,
        nums: {
          a: 1
        }
      }
    },
    computed: {
      info() {
        return this.isHot ? '炎热' : '凉爽';
      }
    },
    methods: {
      change() {
        this.isHot = !this.isHot
      },
      num() {
        this.nums.a++
      }
    },
    watch: {
      info: {
        immediate: true,//初始化的时候先调用handler
        deep: true,//允许深度监视
        handler(newValue,oldValue ) {
          console.log(newValue,oldValue )
        }
      },
      nums: {
        // immediate: true,//初始化的时候先调用handler
        deep: true,//允许深度监视
        handler(newValue,oldValue ) {
          console.log(newValue,oldValue )
        }
      }
    }
  })
```

#### 13.computed和watch区别

1.computed能完成的功能,watch都可以完成。

2.watch能完成的功能，computed不一定能完成，例如: watch可以进行异步操作。两个重要的小原则:

1）所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm或组件实例对象.

2）所有不被Vue所管理的函数（定时器的回调函数、ajax的回调函数，promise的回调函数等)，最好写成箭头函数,这样this的指向才是vm或组件实例对象。

#### 14.绑定style样式

1.class样式

写法:class="xx" xxx可以是字符串、对象、数组。

字符串写法适用于:类名不确定，要动态获取。

对象写法适用于:要绑定多个样式,个数不确定，名字也不确定。

数组写法适用于:要绑定多个样式，个数确定，名字也确定，但不确定用不用。

2. style样式

:style="{fontSize: xXx}"其中xxx是动态值。:style="[a,b]"其中a、b是样式对象。

#### 

#### 16.key值（面试题）！重要

![1655179845288](D:\1前端\vue\文件\vue课件\课件\vue相关备课资料图\1655179845288.png)



![1655180049450](D:\1前端\vue\文件\vue课件\课件\vue相关备课资料图\1655180049450.png)

面试题:react、vue中的key有什么作用?(key的内部原理)

1.虚拟DOM中key的作用:

key是虚拟DOM对象的标识，当状态中的数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】,随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下:

2.对比规则:

(1).旧虚拟DOM中找到了与新虚拟DOM相同的key:

a.若虚拟DOM中内容没变,直接使用之前的真实DOM !

b.若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM.

(2).旧虚拟DOM中未找到与新虚拟DOM相同的key创建新的真实DOM，随后渲染到到页面。

3．用index作为key可能会引发的问题:

a.若对数据进行:逆序添加、逆序删除等破坏顺序操作:会产生没有必要的真实DOM更新==>界面效果没问题,但效率低。

b.如果结构中还包含输入类的DOM:会产生错误DOM更新==>界面有问题。

4.开发中如何选择key? :|

a.最好使用每条数据的唯一标识作为key，比如id、手机号、身份证号、学号等唯一值。

b.如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示,使用index作为key是没有问题的。

#### 17.Vue监视数据的原理

1.vue会监视data中所有层次的数据。
2.如何监测对象中的数据？
通过setter实现监视，且要在new Vue时就传入要监测的数据。
(1).对象中后追加的属性，Vue默认不做响应式处理
(2),如需给后添加的属性做响应式，请使用如下API:
**Vue.set(target,propertyName/index,value)**
**vm.$set(target,propertyName/index,value)**
3,如何监测数组中的数据？
通过包裹数组更新元素的方法实现，本质就是做了两件事：
(1).调用原生对应的方法对数组进行更新。
(2).重新解析模板，进而更新页面。
**4.在Vue修改数组中的某个元素一定要用如下方法：**
1.使用这些API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()
2.Vue.set()  vm.$set()
**特别注意：Vue.set()和vm.$set()不能给vm或vm的根数据对象添加属性！！**

#### 18.过滤器filters

定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）
语法：
1.注册过滤器（全局）：Vue.filter(name,callback)或new Vue(fi1ters:()}
2.局部过滤器：{(xxx|过滤器名}}或v-bind:属性="xxx|过滤器名"

         <p> {{ num | aaa }} </p> 

 filters:{ 

​        "aaa":function(target，p){ 

​          return target<10?'0'+target:target;

​        }

其中target代表|左边的内容，p代表aaa的参数

​      }备注：
1.过滤器也可以接收额外参数、多个过滤器也可以串联
2.并没有改变原本的数据，是产生新的对应的数据

#### 19.实例属性

 vue实例属性

 $el：表示页面容器 （dom节点）

 $data：表示数据仓库；

 $options :获取用户自定义选项；

$refs：将vue中页面元素变成dom元素；

#### 20.实例方法

1 $mount 手动挂载Vue实例,关联页面容器，渲染到页面，

2.$destroy销毁vue实例   

#### $nextTick()

在DOM更新完成后，再执行回调函数，一般在修改数据之后使用该方法，以便获取更新后的DOM,并可以进行相关操作 

vue的响应式原理是按照内部的一定策略执行，当页面更新，dom并没有及时更新，   需要一定时间

4.$set()

vue默认无法为新增的属性，添加劫持，无法实现响应式？

​         * 解决办法：$set()

​         *  this.$set()为对象动态添加属性，让后添加的属性具有响应式；

​	  * this.$delete()，动态删除属性，使对象删除具有响应式；

 变异方法：

​         * Vue 将被侦听的数组的变更方法进行了包裹，所以它们也将会触发视图更新。这些被包裹过的方法包括：

​          push()

​          pop()

​          shift()

​          unshift()

​          splice()

​          sort()

​          reverse() 

5.$delete

删除对象属性；delete方法 

this.$delete obj.id; 

#### 21.模板

el模板：el:'#app'，同时指定挂载位置

 template定义模板，可以渲染到页面上，优先级大于el ，依赖根容器 

 render渲染函数，加载页面模板，渲染到容器中，优先级最高

#### 22.虚拟DOM

1.template编译成渲染函数render,执行渲染函数就可以得到一个虚拟节点树，即虚拟DOM,虚拟节点树转换为真实DOM,映射到视图上,数据更新时，Vue能够智能地计算出需要重新渲染的节点并对虚拟DOM进行修改（打
然后再更新到视图上

**DOM是什么？**
DOM(vdom)是一个用javaScript对象方式描述的页面节点结构树，通过对象的属性来生成节点，它只是对真实DOM的抽象，最终会通过一系列操作使这个虚拟DOM变为真实的DOM,

**使用虚拟DOM(优点)：**
提高DOM更新效率，提升渲染性能
提高快速的DOM变化比较
减少页面中的DOM重新渲染的次数，基于diff算法，找出本次DOM需要更新的节点来更新，其他的不用更新

#### 23.深入响应式原理

当你把一个普通的 JavaScript 对象传入 Vue 实例作为 `data` 选项，Vue 将遍历此对象所有的 property，并使用 [`Object.defineProperty`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 把这些 property 全部转为 [getter/setter](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Working_with_Objects#定义_getters_与_setters)。`Object.defineProperty` 是 ES5 中一个无法 shim 的特性，这也就是 Vue 不支持 IE8 以及更低版本浏览器的原因。

这些 getter/setter 对用户来说是不可见的，但是在内部它们让 Vue 能够追踪依赖，在 property 被访问和修改时通知变更。这里需要注意的是不同浏览器在控制台打印数据对象时对 getter/setter 的格式化并不同，所以建议安装 [vue-devtools](https://github.com/vuejs/vue-devtools) 来获取对检查数据更加友好的用户界面。

每个组件实例都对应一个 **watcher** 实例，它会在组件渲染的过程中把“接触”过的数据 property 记录为依赖。之后当依赖项的 setter 触发时，会通知 watcher，从而使它关联的组件重新渲染。

#### 24.axios

  使用axios.get方法方式请求：

​         trycatch:try后面表示请求成功的处理，catch表示拦截错误； 

```
  sendData() {
        // console.log(axios);
        // 使用axios.get方法方式请求；
        /** 
        * trycatch:try后面表示请求成功的处理，catch表示拦截错误； 
        */
        axios.get(
          "http://route.showapi.com/90-87?showapi_appid=45300&showapi_sign=c28de9d6f79e44369a9abcd40fa3e277"
        )
          .then((res) => {
            try {
              if (res.status == 200) {
                //   console.log(res);
                const { data: resd } = res
                //   console.log(resd.showapi_res_body.pagebean.contentlist);
                this.Msg = resd.showapi_res_body.pagebean.contentlist
                console.log(this.Msg)
              }
            } catch (error) {
              console.log(error);
            }
          });
      },
```

​        */

​          async和await是es7提出的异步解决方法，

​         * async和await配合使用，

​         * await后面修饰的方法，大多数都是异步方法；

​         * async加在await修饰的异步方法的最外层函数前面；

```
async init() {
          // 请求之前拦截
          axios.interceptors.request.use(
            function (config) {
              (config.data = "星期二"),
                (config.headers.Accept = "application/json,javascript/html");
              console.log("config", config);

              return config;
            },
            function (error) {
              return Promise.reject(error);
            }
          );

          let res = await axios.get("https://cnodejs.org/api/v1/topics");
          if (res.status == 200) {
            const { data: resd } = res;
            console.log("resd", resd.data);
            this.Msg = resd.data;
          }

          axios.interceptors.response.use(
            function (response) {
              console.log("response", response);
              return response;
            },
            function (error) {
              // Any status codes that falls outside the range of 2xx cause this function to trigger
              // Do something with response error
              return Promise.reject(error);
            }
          );

```

