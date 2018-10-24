# Ajax

## 一、 javaScript原生使用Ajax

### 1.get方法

```javascript
//1.创建对象 兼容处理
var xhr = null;
//处理低版本IE不兼容问题
if(window.XMLHttpRequest){
    xhr = new XMLHttpRequest();
}else{
    xhr = new ActiveXObject("Microsoft.XMLHTTP");
}
//2.准备发送
xhr.open('get','xxx.php?username=' + usernameValue ,true);
//3.执行发送
xhr.send(null);
//4.回调
xhr.onreadystatechange = function () {
    /*xhr.readyState == 4  是表示数据解析完成，后台处理完成了。
       xhr.status == 200 是表示处理的结果是OK的。响应成功*/
    if (xhr.readyState == 4){
        if(xhr.status == 200){
            //返回结果
            var result = xhr.responseText;
            console.log(result); 
        }
    }
};
```

### 2.post方法

```javascript
//#1.创建对象 兼容性
var xhr = null;
//处理低版本IE不兼容问题
if(window.XMLHttpRequest){
    xhr = new XMLHttpRequest();
}else{
    xhr = new ActiveXObject("Microsoft.XMLHTTP")
}
//#2.准备发送
xhr.open('post','xxx.php',true);

var param = 'phone=' + phoneValue;
//设置响应头
xhr.setRequestHeader('Content-type','application/x-www-form-urlencoded');
//#3.执行发送
xhr.send(param);

//#4.回调函数
xhr.onreadystatechange = function () {
    if(xhr.readyState == 4){
        if(xhr.status ==200){
            var result = xhr.responseText;
            console.log(result);
        }
    }
}
```



> `open()方法`后面的参数`true`和`false`,表示异步和同步，**同步(`false`)就是先吃完饭才能看电视，异步(`true`)就是边吃饭边看电视****

## 二、 jQuery中的Ajax

### 1.基本使用方法

```javascript
$.ajax({
    url: 'xxx.php',
    type: 'get',
    beforeSend: function(xhr){
        console.log(xhr);
    },
    success: function (res) {
        console.log(res);
    },
    error:function (xhr) {
        console.log(xhr);
    },
    complete:function (xhr) {
        console.log(xhr);
    }
});
```

`post`方式只需把`type`值改成	`get`就行

### 2.快捷方式

```javascript
$.get('xxx.php',{id:1},function (res) {
	console.log(res);
});

$.post('xxx.php',{id:1},function (res) {
	console.log(res);
});
```

> **以上是`get`和`post`两种方式**

### 3.解析Json格式

```javascript
$.getJSON('xxx.php',{id:1},function (res) {
	console.log(res);
});
```

> **或者在放置json格式文件的php中进行申明头部**

```p&#39;h&#39;p
<?php
$zhangsan = array(
    'name' =>'张三',
    'age'  =>18
);
//格式
header('Content-Type:application/json');
echo json_encode($zhangsan);
?>
```

