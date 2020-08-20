---
title: 前端CSS基础——通俗理解什么是BFC
---
### 常规流布局

 - 常规流块盒独占一行
 - 常规流块盒在垂直方向依次摆放
 - 常规流块盒父子元素外边距合并
 - 常规流块盒排列无视浮动元素或者脱离常规流布局的元素
 - 常规流块盒高度不计算浮动元素

### BFC的概念
理解完常规流后，我们介绍下BFC，什么是BFC？BFC全称为：Block **Formatting Context——块级格式化布局，简称BFC**，**它是一块独立的渲染区域，这个区域决定了常规流块盒的布局。** 也就是说，BFC是一块区域，作用是决定常规流块盒的布局。

### BFC的创建
BFC由某个HTML元素创建，下列元素会在其内部创建BFC区域。

 - 根元素（<HTML\>元素，<HTML\>元素创建的BFC区域覆盖了所有网页的元素）
 - 浮动定位或者绝对定位元素（**float** 和 **position：absolute**）
 - **overflow**属性不为默认值（visible）的块盒元素

如图所示
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020042201420239.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
注意到没有，每个元素创建的BFC都是互相独立的，元素A、B、C的BFC跟其他元素创建的BFC或者根元素创建的BFC都是相互独立。

### BFC的特性

 1. 不同的BFC在进行渲染时互不干扰
 2. 创建BFC的元素隔绝了它内部BFC与外部BFC的联系，内部的渲染不会影响到外部


### BFC的应用

 #### 解决高度坍塌的问题
在前面发布过的文章中，有提到解决高度坍塌的方法，那就是清除浮动（clear:botn）。现在我们了解BFC后，也能用BFC来解决高度坍塌问题。

```javascript
 	.container{
            width: 100%;
            background-color: skyblue;
            margin-top: 20px;
        }

        .float{
            float: left;
            width: 200px;
            height: 100px;
            background-color: #008c8c;
        }
<body>
    <div class="container">
        <div class="float"></div>
    </div>
</body>
```
效果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200422060047864.png)
如图所示，父类元素的背景颜色并没有显示，我们打开浏览器的开发者模式，找到父类元素，可以看到高度为0，高度坍塌了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200422060253809.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
在父类元素的样式中添加下列三种属性之一使其生成BFC

 - 浮动元素
 - 绝对定位
 - overflow（最常用，可不改变父类元素的布局方式）

```javascript
	.container{
            width: 100%;
            background-color: skyblue;
            margin-top: 20px;
            overflow: hidden;//添加属性
        }
```
得到效果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/202004220608131.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
这里就是因为BFC的特性，互相独立的BFC互不干扰。当子类元素超出父类元素时会造成对其他BFC的干扰，所以需要将子类元素包含在自己的BFC中，所以自动扩展了高度。


#### 相邻父子元素外边距合并问题

```javascript
 	.container{
            width: 100%;
            height: 300px;
            background-color: skyblue;
            margin-top: 20px;
        }

        .float{
            width: 200px;
            height: 100px;
            background-color: #008c8c;
            margin: 30px;
        }
        
		<div class="container">
	        <div class="float"></div>
	    </div>
```
运行上面代码
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200422061706243.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
可以看到，子元素的左右下外边距都能显示出效果，但是子类元素不显示上外边距效果，这是因为子类的上外边距跟父类元素的上外边距合并了，这里用BFC处理，在父类中创建BFC。

```javascript
	.container{
            width: 100%;
            height: 300px;
            background-color: skyblue;
            margin-top: 20px;
            overflow: hidden;
        }
```
运行得到
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200422061911861.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
这是因为父类元素处于根元素创建的BFC里，而子类元素处于父类元素创建的BFC里，所以尽管它们外边距相邻，但是它们所处BFC不同，所以它们的渲染是互不干扰。

#### 无视浮动盒子排序问题
我们先来运行下面代码

```javascript
 		.container{
            height: 300px;
            background-color: skyblue;
            margin-top: 20px;
            /* overflow: hidden; */
        }

        .float{
            float: left;
            width: 200px;
            height: 100px;
            background-color: #008c8c;
            margin: 30px;
        }
        
		<div class="float"></div>
 	  	<div class="container"></div>
```
得到如下效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200422062657594.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
因为container元素是常规流盒子，而float元素是浮动盒子，**常规流盒子排列会无视浮动盒子。** 在container元素创建BFC，再看看效果。

```javascript
	 .container{
            height: 300px;
            background-color: skyblue;
            margin-top: 20px;
            overflow: hidden;
        }
```
运行
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200422062920468.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
这是因为BFC是一块独立的区域，它一定不能跟外部环境（float）互相干扰，所以在排列的时候一定会避开浮动盒子float。


### 总结

 - **创建BFC的元素，它的自动高度会计算浮动元素**
 - **创建BFC的元素不会和它的子元素进行相邻外边距合并**
 - **创建BFC的元素，它的边框盒不会与浮动元素重叠。**
