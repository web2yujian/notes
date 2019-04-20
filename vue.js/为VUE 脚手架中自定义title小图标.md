# 为VUE 脚手架中自定义title标签页小图标

![小图标效果如图所示](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190417092043.png)



## 1. 在项目`index.html`同级目录下添加`favicon.ico`文件

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190417092335.png)

## 2. 在项目`index.html`中引入

```html
<link rel="shortcut icon" type="image/x-icon" href="./favicon.ico"  />
```

## 3. 配置`webpack`配置文件(build文件夹下面)

在下面两个配置文件中加入:

```javascript
favicon: path.resolve('./favicon.ico')
```

具体位置：

### 1.`webpack.prod.conf.js `

```javascript
new HtmlWebpackPlugin({ 
    filename: config.build.index, 
    template: 'index.html', 
    favicon: path.resolve('./favicon.ico'), 
    inject: true, 
}), 

```

### 2. `webpack.prod.dev.js`

```javascript
new HtmlWebpackPlugin({
      filename: process.env.NODE_ENV === 'testing'
        ? 'index.html'
        : config.build.index,
      template: 'index.html',
      favicon: path.resolve('./favicon.ico'),
      inject: true,
      minify: {
        removeComments: true,
        collapseWhitespace: true,
        removeAttributeQuotes: true
        // more options:
        // https://github.com/kangax/html-minifier#options-quick-reference
 }
```

