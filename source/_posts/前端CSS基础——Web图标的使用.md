---
title: 前端CSS基础——Web图标使用
---
网页中一些特殊的小组件，比如购物车图标、用户图标、图片的左右滑轮图标等可以用背景图实现，但是背景图缓存大，加载速度会比较慢，而且不利于开发者修改图标的样式，所以可以采用另一种方式**Web图标**来实现在网页中的一些小图标开发。

> 一些网页中的常见小图标

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421192846749.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421193228254.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421193236920.png)

 1. **先寻找对应图标**
登录网站阿里巴巴矢量图标库（https://www.iconfont.cn/），注册登录后，搜索需要的图标。加入购物车。
例如搜索用户、登录、放大镜、左、右，依次加入购物车。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421194133482.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)

 2. **添加新项目**
打开右上角的购物车，确定好图标后，添加进项目里面。
例如：新建项目test>加入新项目。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421194354917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
注意：在项目名称test下面有三个选项可以选择**Unicode** 、**Font class**、**Symbol**，前两个对应配合css使用，也是比较常用开发方式，第三种属于js方式使用。这里介绍**Font class**的使用，这也是比较符合css语义化的一种方式。


 3. 查看在线链接
 生成链接代码，并copy代码，新建一个html页面，引入css样式。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421201932749.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
 

```
 <link rel="stylesheet" href="https://at.alicdn.com/t/font_1770892_j0hv3zt3xd8.css">
```

 4. 新建一个span元素，引入class="iconfont className"
calssName = "对应图标的类名"，例如我们使用用户图标，用户图标对应的类名为：icon-yonhu，则class = "iconfont icon-yonhu"
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421202218898.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421202226110.png)

```
<body>
    <span class = "iconfont icon-yonhu"></span>
</body>
```
效果图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421202412731.png)

注意：这个图标属性是字体属性，不是图片属性。它有字体元素的所有属性，例如字体大小、加粗、颜色等等，**并且它是个行盒。**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421202600388.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
这是线上的图标应用方法，一般在开发中我们用线上来配对图标看适不适用，但确定好图标好后，我们需要把图标下载到本地，并引入我们网页的根目录中。

 

 1. 下载至本地
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421203118639.png)
 2. 下载完成后解压，打开加压后的文件夹，选择下列文件。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200421203528923.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
 3. 将文件放至html项目根目录并引入样式就可以了。
例如放置css文件夹中

```
<link rel="stylesheet" href="css/iconfont.css">//填写文件放置位置路径即可
```

