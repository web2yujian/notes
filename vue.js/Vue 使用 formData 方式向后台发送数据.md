## Vue 使用 formData 方式向后台发送数据

> 用户点击头像实现更换头像



#### 一、基本使用方式

`template`

```html
 <input class="file" name="file" type="file" accept="image/png,image/gif,image/jpeg" @change="update"/>
```

`JavaScript`

```javascript
update (e) {
    let file = e.target.files[0]
    // console.log(file)
    let param = new FormData() // 创建form对象
    param.append('file', file, file.name) // 通过append向form对象添加数据
    param.append('id', this.$store.state.userId) // 添加form表单中其他数据
  	// withCredentials: true 使得后台可以接收表单数据  跨域请求
    const instance = axios.create({
        withCredentials: true
    })
    // url为后台接口
    instance.post('url', param)
        .then(this.succ) // 成功返回信息 调用函数  函数需自己定义，此处后面省略
        .catch(this.serverError) // 服务器错误 调用对应函数  函数需自己定义，此处后面省略
}
```



#### 二、美化 input file 按钮

> 思路：

1. 简单粗暴地隐藏：opacity: 0;
2. 在 `<input class="file"> ` 元素节点的位置上创建一个好看的元素节点,比如`img`
3. 将 `<input class="file"> ` 元素的z轴变高，使得其覆盖`<img/>`  :z-index: 5;
4. 因为 `<input class="file"> `  是透明的，那么我们就只看见它同xy上的好看的`<img />`
5. 点击这个好看的`<img />` 其实是点击了它上层的表单

以上思路可以实现点击用户头像，**通过表单上传更换头像**

