# docker在windows10下安装

> 前提

- windows 专业版
- 打开`Hyper-v`功能

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123231858.png)





1. **下载软件**   `https://www.docker.com/get-started`

![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123232020.png)

2. **安装**

   步骤就是默认的，不写了

3. **配置**

   - **右击任务栏的小鲸鱼图标**

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123225255.png)

   - **点击setting进入界面**   显示正在运行

     ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123225416.png)

     

   - **设置在国内友好的镜像源**，否则要科学上网从docker hub 上下载镜像

     `https://registry.docker-cn.com`

     ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123225718.png)

   

4. 开始使用

   - `win + X`

   ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123230006.png)

   

   - 选择其中一个 `windows PowerShell`

   - `docker -v`查看版本

     ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123230255.png)

   - 下载一个镜像，比如搜索一个 `ubuntu` 镜像

     `docker search ubuntu`

     会列出很多镜像资源

     ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123230825.png)

     

     我们选择star多的项目进行下载

     `docker pull ubuntu`       pull 后面接的是镜像名称

     ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123231259.png)

   - 查看自己的所有镜像

     `docker images`   下面图示标记的极为刚刚下载的镜像

     ![](https://raw.githubusercontent.com/HunterXing/resourse/master/images/20190123231429.png)

     

   

   

   