# Webpack 4 学习04（配置webpack-dev-server）

> 前提： [ Webpack 4  学习01（基础配置）](https://www.jianshu.com/p/5b849114fe89)
>
> ​             [Webpack 4  学习02（通过配置文件打包）](https://www.jianshu.com/p/eda747a146d9)

## 一、了解 webpack-dev-server

- `webpack-dev-server`用来配置本地服务器
- 为 `webpack` 打包生成的文件提供web服务
- 自动刷新和热替换（HMR）



## 二、安装webpack-dev-server

``` 
npm install --save-dev webpack-dev-server
```





## 三、 配置webpack.config.js文件

 

```javascript
devServer:{
		contentBase:'./dist',  //设置服务器访问的基本目录
		host:'localhost', //服务器的ip地址
		port:8080,  //端口
		open:true  //自动打开页面
}
```

 

## 四、配置package.json



```json
"scripts": {
    "start": "webpack-dev-server --mode development"
 }
```





## 五、运行命令

`npm run dev` 打包文件

`npm run start `打开服务器

