
# cssSkills
> 一些常见的css技巧
## 前言
> 欢迎添加

<!--more-->

## 1、清除浮动
> 浮动给我们的代码带来的麻烦，想必不需要多说，我们会用很多方式来避免这种麻烦，其中我觉得最方便也是兼容性最好的一种是....

```css
// 清除浮动
.clearfix{
  zoom: 1;
}
.clearfix:after{
  display: block;
  content: '';
  clear: both;
}
```

## 2、垂直水平居中
> 三种常见的方式

`绝对定位方式且已知宽高`​

```
position: absolute;
top: 50%;
left: 50%;
margin-top: -3em;
margin-left: -7em;
width: 14em;
height: 6em;
```

`绝对定位 ＋ 未知宽高 ＋ translate`

```
position: absolute;
left: 50%;
top: 50%;
transform: translate(-50%, -50%);
//需要补充浏览器前缀
```


`flex 轻松搞定水平垂直居中( 未知宽高)`

```
display: flex;
align-items: center;
justify-content: center;
```



## 3、 文本末尾添加省略号
> 当文本的内容超出容器的宽度的时候，我们希望在其默认添加省略号以达到提示用户内容省略显示的效果。

`宽度固定，适合单行显示...`

```css
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
```

`宽度不固定，适合多行以及移动端显示`

```css
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 3;  // 行数
-webkit-box-orient: vertical;
```





## 4、制造文本的模糊效果
> 当我们希望给文本制造一种模糊效果感觉的时候，可以这样做

```
color: transparent;
text-shadow:0 0 2px rgba(0,0,0,.5);
```



## 5、自定义文本选中样式
> 默认情况下，我们在网页上选中文字的时候，会给选中的部分一个深蓝色背景颜色(可以自己拿起鼠标试试)，如果我们想自己定制被选中的部分的样式呢？

```css
// 注意只能修改这两个属性 字体颜色 选中背景颜色

element::selection{
  color: green;
  background-color: pink;
}
element::-moz-selection{
  color: green;
  background-color: pink;
}
```



## 6、input占位符
> 当我们给部分input类型的设置placeholder属性的时候，有的时候需要修改其默认的样式。



```css
input::-webkit-input-placeholder{
  color: green;
  background-color: #F9F7F7;
  font-size: 14px;
}
input::-moz-input-placeholder{
  color: green;
  background-color: #F9F7F7;
  font-size: 14px;
}
input::-ms-input-placeholder{
  color: green;
  background-color: #F9F7F7;
  font-size: 14px;
}
```



## 7、首字下沉
> 要实现类似word中首字下沉的效果可以使用以下代码

​```
element:first-letter{
  float:left;
  color:green;
  font-size:30px;
}
​```


​```

## 8、 一端数值宽度  一端百分比进行动态计算  保持整行

```css
width: calc(100% - 80px);  // 其中80px可变
```



## 9、固定宽高比

```css
padding-bottom : 50%
```

