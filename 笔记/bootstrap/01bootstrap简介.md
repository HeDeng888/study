下载后按照顺序添加至文件中

```
    <link rel="stylesheet" href="./btsource/bootstrap.css">

    <script src="./btsource/jquery-3.6.0.js"></script>
    <script src="./btsource/bootstrap.js"></script>
    <script src="./btsource/bootstrap.bundle.js"></script>
    <style>
```

# （一）Bootstrap

## 1、Bootstrap简介

1.Bootstrap 是一个前端开源工具库，它支持Sass变量和mixin、用于构建响应式、移动设备优先的布局，以及响应式栅格系统、自带大量组件和众多强大的 JavaScript 插件。基于 Bootstrap 提供的强大功能，可以快速设计并适配不同大小的窗口的网页。

2.使用时需要先引用框架代码包，并且必须放到所有CSS样式的前面。

```css
<link rel="stylesheet" href="路径">
```

3.Bootstrap自带的大部分组件都需要依赖 JavaScript 才能起作用。所以同样需要引用jQuery框架代码包。

4.[官方网站](https://www.bootcss.com/)

5.[中文网站](https://getbootstrap.net/)



------



## 2、布局

### 1、container

#### 1、固定语法

```html
<!-- .container，固定关键词，常规容器布局 -->
<div class="container" id="">
	<!-- row ：代表行，固定关键词 -->
    <div class="row">
        <!-- col ：代表列，固定关键词 -->
        <div class="col"></div>
    </div>
</div>
```

代码示例

```html
<body>
    <!-- 布局 -->
    <!-- .container，固定关键词，常规容器布局 -->
    <div class="container" id="">
        <!-- row ：代表行，固定关键词 -->
        <div class="row">
            <!-- 网站页面宽度	≥1200px	时执行	-xl	宽度为1140px -->
            <!-- 网站页面宽度	≥992px	时执行	-lg	宽度为960px -->
            <!-- 网站页面宽度	≥768px	时执行	-md	宽度为720px -->
            <!-- 网站页面宽度	≥576px	时执行	-sm	宽度为540px -->
            <!-- 网站页面宽度	<576px	时	宽度占100% -->
            <!-- col ：代表列，固定关键词 -->
            <div class="col col-xl-12 col-lg-3 col-md-6 col-sm-12 col1 "></div>
            <div class="col col-xl-12 col-lg-3 col-md-4 col-sm-12 col2 "></div>
            <div class="col col-xl-12 col-lg-3 col-md-1 col-sm-12 col3 "></div>
            <div class="col col-xl-12 col-lg-3 col-md-1 col-sm-12 col4 "></div>
        </div>
    </div>
</body>
```



#### 2、窗口大小临界值

|       代码       | 超小窗口 | 小号窗口 | 中号窗口 | 大号窗口 | 超大窗口 |
| :--------------: | :------: | :------: | :------: | :------: | :------: |
| 达到临界值时执行 |  <576px  |  ≥576px  |  ≥768px  |  ≥992px  | ≥1200px  |
|    .container    |   100%   | 540像素  | 720像素  | 960像素  | 1140像素 |
|  .container-sm   |   100%   | 540像素  | 720像素  | 960像素  | 1140像素 |
|  .container-md   |   100%   |   100%   | 720像素  | 960像素  | 1140像素 |
|  .container-lg   |   100%   |   100%   |   100%   | 960像素  | 1140像素 |
|  .container-xl   |   100%   |   100%   |   100%   |   100%   | 1140像素 |
| .container-fluid |   100%   |   100%   |   100%   |   100%   |   100%   |

#### 3.栅格注意点

<!-- 使用栅格布局来布局时如果只设置了较小屏幕的尺寸，没有设置大屏幕的尺寸时，大屏幕也会沿用小屏幕的样式。 --> 		

<!-- 使用栅格布局来布局时如果只设置了较大屏幕的尺寸，没有设置小屏幕的尺寸时，小屏幕会铺满12格。 --> 

<!-- 使用栅格布局来布局时如果一行内超过12列，会自动换行。 --> 

## 3.快捷类名用法

### 特殊：引用字体图标

第一步：引入项目下面生成的 fontclass 代码：

第二步：挑选相应图标并获取类名，应用于页面：

<span class="iconfont icon-xxx"></span>

### 1.h标签

```
	<p class="h1">h1. Bootstrap heading</p>
    <p class="h2">h2. Bootstrap heading</p>
    <p class="h3">h3. Bootstrap heading</p>
    <p class="h4">h4. Bootstrap heading</p>
    <p class="h5">h5. Bootstrap heading</p>
    <p class="h6">h6. Bootstrap heading</p>
```

### 2.列表水平对齐

```
  <ul class="list-inline">
      <li class="list-inline-item">列表之一</li>
      <li class="list-inline-item">列表之二</li>
      <li class="list-inline-item">列表之三</li>
    </ul>
```

### 3.列表规整组（上下）

```
 <ul class="list-group">
      <li class="list-group-item">窗前明月光</li>
      <li class="list-group-item">疑是地上霜</li>
      <li class="list-group-item">举头望明月</li>
      <li class="list-group-item">低头思故乡</li>
    </ul>
```

### 4.按钮组合（颜色）

```
   <button type="button" class="btn btn-primary">Primary</button>
    <button type="button" class="btn btn-secondary">Secondary</button>
    <button type="button" class="btn btn-success">Success</button>
    <button type="button" class="btn btn-danger">Danger</button>
    <button type="button" class="btn btn-warning">Warning</button>
    <button type="button" class="btn btn-info">Info</button>
    <button type="button" class="btn btn-light">Light</button>
    <button type="button" class="btn btn-dark">Dark</button>
    <button type="button" class="btn btn-link">Link</button>
```



### 5.表单

```
   <form>
            <div class="form-group row">
              <label for="inputPassword" class="col-sm-3 col-form-label">普通用户</label>

            </div>
            <div class="form-group row">
              <label for="inputPassword" class="col-sm-3 col-form-label">用户名：</label>
              <div class="col-sm-9">
                <input type="password" class="form-control" id="inputPassword" placeholder="请输入用户名">
              </div>
            </div>
            <div class="form-group row">
              <label for="inputPassword" class="col-sm-3 col-form-label">密码：</label>
              <div class="col-sm-9">
                <input type="password" class="form-control" id="inputPassword" placeholder="请输入密码">
              </div>
            </div>
            <div class="form-group row">
              <div class="col-sm-3"></div>
              <div class="col-sm-9 chek">
                <input type="checkbox">
                <label>记住密码</label>
              </div>
            </div>
            <div class="form-group row ">
              <div class="col-sm-3"></div>
              <div class="col-sm-9">
                <button type="submit" class="btn btn-danger">登录</button>
              </div>
            </div>
          </form>
          
```





### 6.导航栏

#### 1.导航栏背景

```
<nav class="navbar navbar-dark bg-dark">
  <!-- Navbar content -->
</nav>
```

![1653554010232](C:\Users\hd\AppData\Local\Temp\1653554010232.png)

dark / primary / light

#### 2.整体内容

```
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Navbar</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link</a>
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Dropdown
        </a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <div class="dropdown-divider"></div>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </li>
      <li class="nav-item">
        <a class="nav-link disabled" href="#">Disabled</a>
      </li>
    </ul>
    <form class="form-inline my-2 my-lg-0">
      <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
      <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
    </form>
  </div>
</nav>
```

#### 3.搜索框1

![1653554153370](C:\Users\hd\AppData\Local\Temp\1653554153370.png)

```
<nav class="navbar navbar-light bg-light">
  <form class="form-inline">
    <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
    <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
  </form>
</nav>
```

#### 4.搜索框2

![1653554191103](C:\Users\hd\AppData\Local\Temp\1653554191103.png)

```
<nav class="navbar navbar-light bg-light justify-content-between">
  <a class="navbar-brand">Navbar</a>
  <form class="form-inline">
    <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
    <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
  </form>
</nav>
```

#### 5.搜索框3

![1653554213434](C:\Users\hd\AppData\Local\Temp\1653554213434.png)

```
<nav class="navbar navbar-light bg-light">
  <form class="form-inline">
    <div class="input-group">
      <div class="input-group-prepend">
        <span class="input-group-text" id="basic-addon1">@</span>
      </div>
      <input type="text" class="form-control" placeholder="Username" aria-label="Username" aria-describedby="basic-addon1">
    </div>
  </form>
</nav>
```

### 7.左右排版

居中对齐或右对齐，使用`.text-center`、`.text-right`方法配合即可 

```
<blockquote class="blockquote text-center">
  <p class="mb-0">爱上一个地方，就应该背上包去旅行，走得更远。</p>
  <footer class="blockquote-footer">出自商务印书馆的 <cite title="Source Title">《新华字典》</cite></footer>
</blockquote>
```

### 8.下拉菜单

```
<div class="dropdown">
  <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
    Dropdown button
  </button>
  <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
    <a class="dropdown-item" href="#">Action</a>
    <a class="dropdown-item" href="#">Another action</a>
    <a class="dropdown-item" href="#">Something else here</a>
  </div>
</div>
```

### 9.导航滑动门

![1653555114238](C:\Users\hd\AppData\Local\Temp\1653555114238.png)

```
<nav>
  <div class="nav nav-tabs" id="nav-tab" role="tablist">
    <a class="nav-item nav-link active" id="nav-home-tab" data-toggle="tab" href="#nav-home" role="tab" aria-controls="nav-home" aria-selected="true">Home</a>
    <a class="nav-item nav-link" id="nav-profile-tab" data-toggle="tab" href="#nav-profile" role="tab" aria-controls="nav-profile" aria-selected="false">Profile</a>
    <a class="nav-item nav-link" id="nav-contact-tab" data-toggle="tab" href="#nav-contact" role="tab" aria-controls="nav-contact" aria-selected="false">Contact</a>
  </div>
</nav>
<div class="tab-content" id="nav-tabContent">
  <div class="tab-pane fade show active" id="nav-home" role="tabpanel" aria-labelledby="nav-home-tab">...</div>
  <div class="tab-pane fade" id="nav-profile" role="tabpanel" aria-labelledby="nav-profile-tab">...</div>
  <div class="tab-pane fade" id="nav-contact" role="tabpanel" aria-labelledby="nav-contact-tab">...</div>
</div>
```

### 10.弹出框

```
<button type="button" class="btn btn-lg btn-danger" data-toggle="popover" title="Popover title" data-content="And here's some amazing content. It's very engaging. Right?">点击体验 popover提示框效果</button>
```

```
$('.popover-dismiss').popover({
  trigger: 'focus'
})
```

### 11.水平排列

![1653555600304](C:\Users\hd\AppData\Local\Temp\1653555600304.png)

```
<div class="card mb-3" style="max-width: 540px;">
  <div class="row no-gutters">
    <div class="col-md-4">
      <img src="..." class="card-img" alt="...">
    </div>
    <div class="col-md-8">
      <div class="card-body">
        <h5 class="card-title">Card title</h5>
        <p class="card-text">This is a wider card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
        <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
      </div>
    </div>
  </div>
</div>
```

### 12.图片加边框

```
<img src="..." alt="..." class="img-thumbnail">
```

### 13.图片对齐处理

![1653555685492](C:\Users\hd\AppData\Local\Temp\1653555685492.png)

```
<img src="..." class="rounded float-left" alt="...">
<img src="..." class="rounded float-right" alt="...">
```

14.