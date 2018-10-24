# Bootstrap 学习(v3)

## 一、基本知识

### 1.认识Bootstrap

#### 什么是bootstrap？

Bootstrap 是一个用于快速开发 Web 应用程序和网站的前端框架。Bootstrap 是基于 HTML、CSS、JAVASCRIPT 的。

#### 为什么使用Bootstrap？

- **移动设备优先**：自Bootstrap3起，框架包含了贯穿于整个库的移动设备优先的样式。
- 浏览器支持：所有主流浏览器都支持Bootstrap。
- 容易上手：只要有html、css的基础，就可以开始学习。
-  响应式设计：Bootstrap的响应式css能够自适应台式机、平板电脑和手机。

#### GitHub上这样介绍 bootstrap：

- 简单灵活可用于架构流行的用户界面和交互接口的html、css、javascript工具集。
- 基于html5、css3的bootstrap，具有大量的诱人特性：友好的学习曲线，卓越的兼容性，响应式设计，12列格网，样式向导文档。
- 自定义JQuery插件，完整的类库，基于Less等。



### 2.Bootstrap的大概内容

- 栅格系统——就是将屏幕平分12份（列）。使用行(row)来组织元素（每一行都包括12个列，保留15位精度），然后将内容放在列内。通过col-offset-*来控制列偏移。Bootstrap的核心功能。

- CSS组件——Bootstrap为我们预实现了很多CSS组件。如排版、代码、表格、按钮、表单等。也就是说Bootstrap内容帮我们定义好了很多CSS样式，你可以将这些样式直接应用到下拉框等元素里。

- 基础布局组件——Bootstrap提供了多种基础布局组件。如下拉框、按钮组、导航等。

- JavaScript插件——Bootstrap也为我们实现了一些JS插件，我们可以用其提供的插件要完成一些常用功能，而不需要我们再重新写JS代码来实现像提示框，模态窗口这样的效果了。

- Jquery——Bootstrap所有的JavaScript插件都依赖于Jquery的。如果要使用这些JS插件，就必须引用Jquery库。这也是为什么我们在除了要引用Bootstrap的JS文件和CSS文件外，还需要引用Jquery库的原因，两者是依赖关系。Bootstrap插件的基础。

- 响应式设计——这就是一个设计理念。响应式的意思就是它会根据屏幕尺寸来自动调整页面，使得前端页面在不同尺寸的屏幕上都可以表现很好。兼容多个终端，这是bootstrap的终极理念。



![](https://raw.githubusercontent.com/HunterXing/resourse/master/6362810929040656613017229.png)



### 3.Bootstrap获取

- ### **官网获取：**

[Bootstrap中文官网  ]: https://v3.bootcss.com/

- **Bootstrap 基本的HTML模板**

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap</title>

    <!-- Bootstrap -->
    <link href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">

    <!-- HTML5 shim 和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 -->
    <!-- 警告：通过 file:// 协议（就是直接将 html 页面拖拽到浏览器中）访问页面时 Respond.js 不起作用 -->
    <!--[if lt IE 9]>
    <script src="lib/html5shiv/html5shiv.min.js"></script>
    <script src="lib/respond/respond.min.js"></script>
    <![endif]-->
    <!--自己的css文件放在后面用来覆盖-->
    <link rel="stylesheet" href="public/css/main.css">
</head>
<body>




<!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
<script src="https://cdn.bootcss.com/jquery/1.12.4/jquery.min.js"></script>
<!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
<script src="https://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>

<!--自己的js文件放在后面用以覆盖-->
<script src="public/js/main.js"></script>
</body>
</html>
```

## 二、栅格系统

### 1.响应式设计

- 什么是响应式设计？
  - 让一个网站可兼容不同分辨率的设备，给用户更好的视觉使用体验

- 响应式设计的优缺点？

  - 优点：解决了设备可见的差异化展示

  - 缺点：兼容性代码多，工作量大，加载速度受影响。



- 启动响应式：
  - 通过在文档中的 <head> 标签里添加合适的meta标签并引入一个额外的样式表即可启用响应式CSS。如果你已经在定制页面编译好一个Bootstrap, 那么只需添加一个meta标签。

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="assets/css/bootstrap-responsive.css" rel="stylesheet">
```

- 响应式设计的原则：

  -  移动优先，在设计初期就要考虑到页面如何在多终端展示；

  - 渐进增强，充分发挥硬件设备的最大功能。   



- 各种媒介的分类：

>  xs：extra small 特别窄屏幕，默认指浏览器像素宽度小于768px
>
> sm：small 窄屏幕，默认指浏览器像素宽度大于等于768px
>
> md：middle 中等宽度屏幕，默认值指浏览器像素宽度大于等于992px
>
> lg：large 大屏幕，默认值指浏览器像素宽度大于等于1200px



- 结合屏幕宽度时，栅格系统显示：

>xs:col-xs-1~ col-xs-12，多列始终在一行内。
>
>sm：col-sm-1 ~ col-sm-12，多列在浏览器像素宽度大于等于768px时才在一行内。
>
>md：col-md-1 ~ col-md-12，多列在浏览器像素宽度大于等于992px时才在一行内。
>
>lg：col-lg-1~ col-lg-12，多列在浏览器像素宽度大于等于1200px时才在一行内。

注：在处理不同像素宽度的时候，大宽度的适配优先于窄宽度（lg>md>sm>xs）。



### 2.布局

Bootstrap 需要为页面内容和栅格系统包裹一个 `.container` 容器。我们提供了两个作此用处的类。注意，由于 `padding` 等属性的原因，这两种 容器类不能互相嵌套。

`.container` 类用于固定宽度并支持响应式布局的容器。

```h&#39;t
<div class="container">
  ...
</div>
```

`.container-fluid` 类用于 100% 宽度，占据全部视口（viewport）的容器。

```html
<div class="container-fluid">
  ...
</div>
```



### 3.基本栅格

```html
<div class="container">
    <div class="row">
        <div class="col-md-4">...</div>
        <div class="col-md-8">...</div>
    </div>
</div>
```

![](https://raw.githubusercontent.com/HunterXing/resourse/master/20180926191709.png)

- #### **偏移列**

  - 偏移有以下几种：
    - offset：左外边距（margin-left）；
    - pull：右位移（right）；
    - push：左位移（left）。

  **其中`offset`使用的频率最高。**

  - 使用 `.col-md-offset-*` 类可以将列向右侧偏移。这些类实际是通过使用 `*` 选择器为当前元素增加了左侧的边距（margin）。例如，`.col-md-offset-4` 类将 `.col-md-4` 元素向右侧偏移了4个列（column）的宽度。

  ```html
  <div class="row">
    <div class="col-md-4">...</div>
    <div class="col-md-3 offset2">...</div>
  </div>
  ```

  效果：

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20180926195136.png)

- #### **嵌套列**

  - 在默认的栅格系统里，在已有的`.col-xx-yy`里添加一个新的`.row`并加入`.col-xx-yy`列（xx可以是lg、md、sm、xs，yy可以是1~12），就可以实现嵌套。**被嵌套的每列列数总和不可以超过12。**

  - 案例代码：

    ```html
    <div class="row">
      <div class="col-sm-9">
        Level 1: .col-sm-9
        <div class="row">
          <div class="col-xs-8 col-sm-6">
            Level 2: .col-xs-8 .col-sm-6
          </div>
          <div class="col-xs-4 col-sm-6">
            Level 2: .col-xs-4 .col-sm-6
          </div>
        </div>
      </div>
    </div>
    ```

    ![](https://raw.githubusercontent.com/HunterXing/resourse/master/20180927102842.png)

4.实现响应式