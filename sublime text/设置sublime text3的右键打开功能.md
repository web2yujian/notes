# 设置sublime text3的右键打开功能

1. 第一步，win + R 输入命令 `regedit`

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123211651.png)

2. 第二步，打开注册表编辑器，在所指路径创建`sublime text3`的项，并且在右侧将数据修改为合适的语句。如下图所示

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123212317.png)

3. **第三步 （重点）**：在刚刚新建的`sublime text3`的项下面再新建一个项`command`,修改他的数据，`%1`前面为sublime text3 软件的可执行文件的路径。`D:\Sublime Text\sublime_text.exe %1`    根据自己的情况自行修改

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123212525.png)

4. 第四步，效果：

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123213016.png)

   

   





