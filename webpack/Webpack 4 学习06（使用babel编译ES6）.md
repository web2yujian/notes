# Webpack 4 学习06（使用babel编译ES6）

> 目前，ES6（ES2015）这样的语法已经得到很大规模的应用，它具有更加简洁、功能更加强大的特点，实际项目中很可能会使用采用了ES6语法的模块，但浏览器对于ES6语法的支持并不完善。为了实现兼容，就需要使用转换工具对ES6语法转换为ES5语法，babel就是最常用的一个工具

- **babel转化语法所需依赖项**：
  - `babel-loader`： 负责 `es6 `语法转化
  - `babel-core`： `babel`核心包
  - `babel-preset-env`：告诉`babel`使用哪种转码规则进行文件处理

- **安装依赖**

  ```
  npm install babel-loader @babel/core @babel/preset-env --save-dev
  ```

- **配置`webpack.config.js`文件**

  ```javascript
    	{
        test:/\.js$/,
        exclude:/node_modules/,
        use:'babel-loader'
      }
  ```

  

- **新建 `.babelrc `文件配置转换规则**

  ```
  {
    "presets":["@babel/preset-env"]
  }
  ```

  

- 或者直接在`webpack.config.js`文件中配置规则

  ```javascript
    	{
        test:/\.js$/,
        exclude:/node_modules/,
        use:{
        	loader:'babel-loader',
        	options:{
              presets:['@babel/preset-env']
        	}
        }
      }
  ```

  