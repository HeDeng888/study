# Vue3

## 一、开发环境

vue@cli，脚手架命令行

vue ui图形化界面

## 二、vue3新特性

### （一）响应式API

包括响应式基础API，比如，Refs ，computed，watch

#### 1、reactive方法

```javascript
1/reactive函数，实现创建响应式对象。
2/导入ractive函数;
3/通过reactive方法定义响应式对象
const data = reactive({
    name:'tom'
    age:18,
})
cosole.log(data)
```

#### 2、readonly方法

```javascript
只读模式，不允许修改
setup(){
    const obj=reactive({
        name:'zhang san'
    })
    const proxy =readonly(obj)
    //console.log(obj)
    //console.log(proxy);返回proxy{name:tom}代理对象
    
    //proxy 是只读的，不允许修改
    //proxy.name='li si'
    obj.name='mike'
    console.log(proxy)
}
```

#### 3、ref方法

```javascript
1)/定义一个响应式数据（简单数据类型）
2)/通过value属性获取定义的值
3)/在模板中，ref对象中的值，无需使用value获取

setup(){
   const count =ref(1)
   console.log(count.value);//通过count.value获取函数值
    const change=()=>{
        count.value=100
    }
    return{
        count,
        change
    }
}

ref获取DOM节点？
<div ref='wrap'>hello vue3</div>
//refs 获取DOM节点
const warp =ref(1);
console.log('warp',warp.value);//打印div元素

案例：设计一个场景？调用子组件中的方法
子组件中：
<input type='checkbox' ref='warp'/>
    const warp =ref(null);
    const gerDoms=()=>{
    return warp.value.checked=true;
};
在父组件中调用子组件：<Article ref='articleComp'></Article>
通过ref调用子组件的方法，让勾选选中。
const articleComp=ref(null);
articleComp.value.gerDoms()

案例：修改变量后，不能立刻获取更新后的DOM的文本值，通过nestTick获取到DOM下一次更新后的值。利用ref实现。
import {ref,nextTick} from 'vue'
export default{
    setup(){
        let count=ref(0);
        let doms=ref(null);
        const changeCount=async()=>{
            count.value+=1
            //通过nextTick（）获取元素更新后的状态
            await nextTick()
            console.log(doms.value.innerText);
        }
    }
}
```

#### 4、computed方法

```javascript
1 /类似计算属性，接收一个getter函数，并根据getter的返回值返回一个不可变的响应式ref对象

const msg = ref( "welcome to vue3 ")
const reverseMsg = computed(() => msg.value.toUpperCase().split(' ').reverse().join(' '));

const count=ref(1)
const plusCount = computed(()=>count.value+1)
// plusCount.value++

2/接收一个具有get和set函数的对象，创建一个可写的ref对象

const nums = ref(2)
const plusNums = computed({
     get:()=>count.value +1,
     set:val=>{
     nums.value = val-1，
   }
})

plusNums.value=1
//console.log(num.value) 0 
```

#### 5、watch方法

```javascript
1、//侦听单一源:侦听数据源可以是一个具有返回值的 getter函数，也可以直接是一个ref;单一属性（单一变量、单一属性)
const count = ref(0)
watch(count,(nowval,oldval)=>{
//
})

const state = reactive({count: 0})
watch(
    ()=>state. count,
    (newval,oldval)=>{
        // ....
})


2、侦听多个源,侦听数据还可以是数组或对象;
const userInfo = reactive({
   fooArr : "abc",
   barArr : "efg "
})
watch([ ()=>fooArr,()=>barArr ],([newfoo,newbar], [oldfoo,oldbar])=>{
    //...
})

3/取消监视
const unwatch = watch()
unwatch()


4/深度监听
深度嵌套对象或数组中的 property变化时，仍然需要deep 选项设置为 true

watch(()=>message , (newVal,oldVal)=>{
    console.log("新值" , newVal, '旧值' ,oldVal);
}, {
    deep:true
})


对象中的堆内存被修改的解决方法:
侦听一个响应式对象或数组将始终返回该对象的当前值和上一个状态值的引用。为了完全侦听深度嵌套的对象和数组，可能需要对值进行深拷贝。

import _ from 'lodash'
watch(
   ()=>_.cloneDeep(state),
        (state.prevState)=>{
           console.log(state.attributes.name,prevState.attributes.name)
     }
)
```

#### 6、watchEffect

```javascript
//首先侦听并执行1次,侦听的数据发生变化时，触发。
watchEffect(() =>{
    console.log(count.value);
})

```



### （二）组合式API

#### 1、setup函数

```javascript
1、/setup接收两个参数: props和context props表示props对象，context表示context对象;打印props和context;
2、/在setup中输出this
3、/return返回，数据、方法;
4、/案例演示
setup(props, context) {
        console.log( 'setup . . ... ");
        /**
        *0、普通数据的定义，不具有响应式
        */
        var name = 'tom'
        var user = {
            username:'admin',
            password:'123'
         }
                    const study=()=>{
            name='zhang san'
            console.log('修改name:'+name);
        }
        /**
        *1、在setup函数中，无法访问this，输出undefined；
        */
        //console.log(this);
        //2、setup的第一个参数，输出为props对象，
        //即父组件给自己传递的数据；
        console.log(props);
        const getAge=()=>console.log(props.age);
        //3、setup函数的第二个参数，输出为一个对象，可以触发事件；
        //console.log(context);
        //4、setup内要使用return返会值，暴露给模板，在模板中才可以访问；
        return{
            name,
            user,
            stu,
            study,
            getAge
        }
    },
        
        //父子通信
        1、父------>子
        父组件通过属性绑定的形式，将需要传递的数据绑定到标签上，
        同时在子组件中，setup函数接收两个参数，子组件通过props，获取父组件传递的属性值。
        
        2、子------>父
        子组件向父组件传值，通过setup函数中的参数，context，通过context.emit('自定义事件名'，数据)
        父组件在调用子组件标签上，通过事件监听子组件的事件名，获取到子组件传递的值
```

#### 2、生命周期函数钩子函数

```javascript
/选项式API的生命周期钩子函数和组合式API生命周期钩子不同
import { onMounted，onUpdated，onUnmounted } from "vue'
const MyComponent = {
  setup() {
    onMounted(() =>{
      console.log('mounted!')
    })
    onUpdated(() =>{
       console.log('updated!')
    })
    onUnmounted(() =>{
       console.log("unmounted!")
    })
  }
}


beforeCreate ->                       使用setup()
created ->                           使用setup()
beforeMount -> onBeforeMount          挂载前
mounted -> onMounted                  挂载完成
beforeUpdate -> onBeforeUpdate        更新前
updated -> onUpdated                  更新完成
beforeUnmount -> onBeforeUnmount      卸载前
unmounted -> onUmounted              卸载完成

卸载(main.js)
const app= createApp(App).use( store).use(router)
setTimeout()=>{
    app. unmount()
},2000)
```

#### 3、指令

以v-model为例：

```javascript
v-model :
    <input type="text" v-mode1.lazy.trim.number="num">
        
    //案例防抖
    <input type="text" v-model="keyword" />
        
    //防抖(官网)
    import { customRef } from "vue" ;
    const myRef= function (value，delay) {
         let timer;
         return customRef((track, trigger) =>{
            return {
                get( ) {
                  track(); //通知Vue追踪value的变化
                    console.log(`读取数据了`);
                    return value;
                }，
                set(newvalue){
                   clearTimeout(timer);
                   timer = setTimeout(() =>{
                      value = newValue;
                      trigger();//通知Vue去重新解析模板
                }, delay);
             },
         };
       });
    }
    let keyWord=myRef('',1500);//使用程序员自定义的ref
return{
    keyWord
}
```

### （三）单文件组件

组件初始化的三种写法:

#### 1、setup方法

```javascript
方式一:
<script>
   export default{
     setup(){
    }
  }
</script>
```



2、<script  setup>嵌套写法

```javascript
方式二:
<script setup></script>
//省略export default
//省略return

1、父----->子
父组件中，在子组件标签上通过属性绑定
    <layout-child :gift="present" @sent_event="getMsg"></layout-child>
在子组件中，通过定义defineProps来接收父组件传来的属性值。
    const props = defineProps(
        gift:{
            type:String,
        }
    }
2、子------->父
//自定义一个事件（向父组件传递)比如点击按钮触发
在子组件中,使用defineEmits定义一个自定义事件，同时，触发自定义事件，并传递数据、
   emit = defineEmits(['sent_event'])
       const sendMsg = ()=>{
          emit('sent_event',msg)
     }
//简写：defineEmits(['sent_event'])('sent_event,msg)
       
3.非父子组件通信
provide/inject
mitt库
   emit.js
      import mitt from 'mitt'
      const emitter =new mitt()
      export default emitter;


方式三、
import {defineComponent} from '@vue/runtime-core';

export default defineComponent({
    
})
```

### （四）vue3优势

#### 1、数据劫持

vue2响应式原理。

#### 2、proxy代理对象

```javascript
1、//写法上更加优雅:
2、//丰富的响应式API功能;
3、//响应式原理，Vue3的数据响应与劫持是基于现代浏览器所支持的代理对象Proxy实现的，弥补了vue2数据劫持方式的缺陷;
  1)/ vue3源码内部，设置了track函数来保存数据，通过new Map/new weakMap等数据结构，来形成key/value的映射关系，以及业务的执行函数;

  2)/设置effect函数来执行具体的业务；

  3）/设置trigger函数来遍历和执行effect；
//源码createReactive函数
const initData={value:1}
const proxy =new Proxy(
    initData,
    {
        get(target,key){
            return target[key]
        },
        set(target,key,value){
            console.log(Reflect);
            return Reflect.set(target,key,value)
        }
    }
)
proxy.value=2
console.log(proxy.value);

console.log(initData.value);

参考 http://t.zoukankan.com/goloving-p-15483805.html
http://segmentfault.com/a/1190000041540939
```











