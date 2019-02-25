> 很多时候因为快捷键冲突，我们得自定义` atom`编辑器的快捷键

- 打开`keymap.cson` 
  ![打开`keymap.cson`](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225123946.png)

- 自定义格式如下

  ```json
  'selector':
    'Keystroke':'Command'
  ```

  ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190225124620.png)



- 将上述格式替换成上图箭头所指的数值，快捷键可更换。即：

  ```json
  'atom-workspace':
    'ctrl-alt-q':'ask-stack:ask-question'
  ```

- 这时候使用`ctrl-alt-q`就可以完成命令了