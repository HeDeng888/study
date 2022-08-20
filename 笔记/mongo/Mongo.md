# Mongo

### 安装下载

下载地址 ：https://www.mongodb.com/try/download/community 

安装教程：https://www.runoob.com/mongodb/mongodb-window-install.html 

### vscode连接数据库

#### 方法一：mongodb 

```
step1:导入模块

const monogs = require('mongodb')
const mgclient = monogs.MongoClient;
//async await 表示异步加载，await修饰的方法是一个promise对象，
//async必须放在await方法当前作用域的第一个函数前面， es6新增的语法糖。

step2:立即执行函数

(async function(){
    //创建服务器，连接主机
	var client= new mgclient('mongodb://127.0.0.1:27017')
   	//连接数据库系统
    var res = await client.connect()
	console.log('数据连接成功');
    const db = client.db("kgc");//连接数据库名称
    const names = db.collection('student')  //连接集合
    
    /*插入数据*/
   let res = names.insertMany([
      {
        name: "郭富城",
        age: 30,
        score: 80,
      },
      {
        name: "梁朝伟",
        age: 32,
        score: 68,
      },
    ])
    console.log('新增数据成功',res);
    
    /*更新数据*/
    let r = await names.updateOne(
      {name: '张学友' },
      {
        $set: {    
          name: '周润发',
        },
      }
    );

    console.log('更新成功', r);
    
    /*删除数据*/
    let m = await names.deleteOne({
        name:'张学友',
        // name:'刘德华',
     })
     console.log('删除成功',m);
})()
```

如果要模块化导出：module.exports=names; （写在index文件里面不用立即执行函数即可）；

#### 方法二：mongoose

```
step1: 导入mongoose模块
var mongoose = require('mongoose')

step2: 连接数据库
mongoose.connect('mongodb://127.0.0.1:27017/kgc2')

//on方法，监听不同事件，error，表示连接失败，open,表示连接成功
//disconnected
mongoose.connection.on('error',function(err){
    console.log('连接失败',+ err);
})
mongoose.connection.on('open',function(){
    console.log('连接成功');
})
mongoose.connection.on('disconnected',function(){
    console.log('断开数据库');
})

step3: 定义架构
let schema = new mongoose.Schema({name:String,age:String,hobby:String})
var Model = mongoose.model('class',schema)

step4: 创建数据
Model.create([
    {
        name:'李白',
        age:'20',
        hobby:'写诗'
  }, {
    name:'杜甫',
    age:'20',
    hobby:'写诗'
  }],function(err,doc){
      if(err){
          console.error(err);
      }else{
         console.log('success');
         console.log(doc);
      }
  })
  
  step5: 更新数据
   Model.updateOne({name:'李白'},{age:120},function(err,res){
        if(err){
           console.log('error'+err);
        }else{
            console.log('res'+res)
       }
	})
  step6: 查询数据
  Model.findOne({name:'杜甫'},function(err,res){
        if(err){
            console.log(err);
        }else{
            console.log(res);
        }
	})
  step7: 删除数据
  Model.deleteOne({name:'李白'},function(err,res){
        if(err){
            console.log(err);
        }else{
            console.log(res);
        }
	})
```

如果要模块化导出：module.exports=Model; 

插入数据文件接收：

```
var m = require('./app')
m.create([
   {
       name:'李白',
       age:'20',
      hobby:'写诗'
  }, {
   name:'杜甫',
   age:'20',
   hobby:'写诗'
  }],function(err,doc){
     if(err){        
     	console.error(err);
     }else{         
     	console.log('success');
     	console.log(doc);
     }
})
```

其他模块操作同上；

### 一、mongodb语法

```mysql
mongo.exe  运行
show dbs 查看当前所有数据库
use dbtext  创建当前数据库 //有则使用无则创建
show collections  //查看当前数据库下面的表
db.user.find()  查询表内容
db.student.findOne({'name':'张飞'})  查询某个   
db.createCollection('user')  创建表
db.student.insertOne({name:'张飞'})  插入数据
db.student.update({name:'张飞'},{name:'关羽'})  更新数据
db.student.remove({name:'张飞'})  删除数据
db.getCollection('表名').find({})  查看表


1.mongo.exe         运行
2.show dbs          查看当前所有数据库
3.use 数据库名       启用数据库
4.show collections  查看当前数据库下面的所有表
5.db.表名.find()    查看当前输入的表的内容
```

### 二、node连接mongodb数据库

```javascript
1.新建项目文件夹，初始化
2.创建数据库
/*
 *导入模块
 */
const monogs = require('mongodb')

const mgclient = monogs.MongoClient;


//async await 表示异步加载，await修饰的方法是一个promise对象，
//；async必须放在await方法当前作用域的第一个函数前面， es6新增的语法糖。

(async function() {
    //创建服务器，连接主机
    var client = new mgclient('mongodb://127.0.0.1:27017')
        //连接数据库系统
    await client.connect()
    console.log('数据连接成功');
    const db = client.db("kgc"); //连接数据库名称
    const names = db.collection('student') //连接集合


    //新增表中的数据
    // let res = names.insertMany([{
    //         name: "张飞",
    //         age: 25,
    //         score: 80,
    //     },
    //     {
    //         name: "赵子龙",
    //         age: 25,
    //         score: 90,
    //     },
    // ])
    // console.log('新增数据成功', res);

    //更新数据
    // let r = await names.updateOne({ name: '张飞' }, {
    //     $set: {
    //         name: '马超',
    //     },
    // });
    // console.log('更新成功', r);


    //确认是否要删除 deleteOne()
    //  let r = await names.deleteOne({
    //      name: '马超'
    //  })
    //  console.log('删除成功', r);

   var r = await names.find().toArray()
   console.log("查询成功", r);

})()
```

### 三、定义schema架构

```javascript
var Schema = new mongoose.Schema({  //字段
    username:{type:String},
    password:{type:Number,default:123456},
    time:{type:Date}
}) 
//由schema构造生成model
var Model =mongoose.model('表名字',Schema)

//完整代码
//导入mongoose模块
const { default: mongoose } = require('mongoose');
var monogs = require('mongoose')
mongoose.connect('mongodb://127.0.0.1:27017/kgc2')

//on方法，监听不同事件，error，表示连接失败，open，表示连接成功
mongoose.connection.on('error', function(err) {
    console.log('连接失败', +err);
})

mongoose.connection.on("open", function() {
    console.log('连接成功');
})
mongoose.connection.on("disconnected", function() {
    console.log('断开数据库');
})

// var schema = new mongoose.Schema({name:'string',size:'string'});
// var Tank = mongoose.model('Tank',schema);

//定义架构
let schema = new mongoose.Schema({ name: String, age: String, hobby: String })
var Model = mongoose.model('class', schema)
```

### 四、定义模型数据

根据架构的数据，来设计模型和创建表

```javascript
/以下内容放在schema架构下面使用
//创建数据
Mode1.create([
    {
    username:'李白',
    password:123321
    },{
        username: '杜甫',
        password:78901,
    }],function(err,doc){
    if(err){
        console.error(err);
    }else{
        console.log('successs');
        console.log(doc);
    }
})

//更新数据
Model.updateOne({name :'李白'},{age:123456},function(err,res){
   if(err){
       console.1og( 'error'+err);
   }else{
       console.log("res"+res)
   }
})
//更新
Model.updateMany(username:""})
// { 'name': {$in:['李白','杜甫']}},{$set: {"age" :25]


//删除数据
Model.deleteOne({name:'杜甫'},function(err,res){
    if(err){
        console.log(err);
    }else{
        console.log(res);
    }
})

//查找数据
Model.findOne({name:'李白'},function(err,res){
    if(err){
        console.log(err);
    }else{
        console.log(res0;)
    }
})
```





















