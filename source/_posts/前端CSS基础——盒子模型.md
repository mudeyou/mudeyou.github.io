盒模型基础
### 盒子模型的重要性
盒子模型是CSS中最重要的知识点之一，它是一个非常重要的知识点，如果没有理解好盒子模型的概念，那么在以后的网页设计开发中没有办法布局出一个优美的网页，它是你接下来学习布局的基础。
### 什么是盒模型
盒模型是CSS中的一个概念,每个元素在页面中都会生成一个矩形的空间，这个矩形的空间就叫做盒子。盒子可以分为两种：一种是**行盒**，一种是**块盒**。

 - 行盒：display属性为inline的元素。
 - 块盒：display属性为block的元素。

行盒在页面显示中不换行，类似于行级元素（span、a、img、video、audio等）
块盒在页面显示中独占一行，类似于块级元素（div、h1~h6、p等）
### 盒子的组成部分
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408160414934.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70#pic_center)
#### 1.内容

 - content部分为盒子的内容部分，它的属性有width、height，用于定义内容部分的宽高。
```javascript
  width：10px;
  height：10px;
```

 - 只包含content部分的叫做盒子的**内容盒：ontent-box**

#### 2.内边距

 - padding为内边距，表示内容部分离边框的距离，它有四个属性：padding-left(左边距)、padding-right(右边距)、padding-top(上边距)、padding-bottom(下边距)，也可以简写成：padding
```javascript
  padding-top:10px;
  padding-right:10px;
  padding-bottom:10px;
  padding-left:10px;
```

   等于
   

```javascript
padding:10px;（上 右 下 左）
```

等于
```javascript
 padding:10px 10px;(上下 右左)
```

- 包含内容（content）跟内边距（padding）的部分称为盒子的**填充盒：padding-box**
#### 3.边框
 - border表示边框，即图中padding周围的黑色部分，它有三个属性：border-style（边框样式，即实线还是虚线等）、border-width（边框宽度）、border-color（边框颜色）

```javascript
border-width:1px（宽度为1px）
border-style:solid（实线）
border-color:red（红色）
也可简写成
border:1px solid red
```
- 包含内容（content）、内边距（padding）和边框（border）的部分称为**边框盒：border-box**

#### 4.外边距

 - margin为外边距，表示边框盒与其他盒子之间的距离，它有四个属性：margin-left(左边距)、margin-right(右边距)、margin-top(上边距)、margin-bottom(下边距)，也可以简写成：margin

```javascript
  margin-top:10px;
  margin-right:10px;
  margin-bottom:10px;
  margin-left:10px;
```

   等于
```javascript
  margin:10px;（上 右 下 左）
```
等于
```javascript
 margin:10px 10px;(上下 右左)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408163149440.png#pic_center)
### 开发实用技巧

#### 1）div的宽高问题
 当你想定义一个宽为100px，高为30px的div时，你会用`width：100px;  height:30px;`定义一个符合要求的div，这没问题，页面显示的也确实是宽高为**100px**和**30px**的div，但是当你添加一个边框或者内边距时，整体的div宽高都会发生变化，比如添加一个宽度为1px的边框`border-width:1px`时或者添加一个内边距**10px** `padding-left:10px`时，你的div宽高不再是**100px**、**30px**，而是**102px**,**32px**或者**110px**,**30px**,这是为什么呢，因为一开始width跟height定义的是内容content的宽高而不是div的宽高，所以加入其他宽度的时候div自然会发生变化，那么该如何解决呢，这里引入一个CSS3的属性： box-sizing，可以有效解决上面的问题。
`box-sizing：border-box（表示width、height指定边框盒）`

#### 2）背景的覆盖问题
在默认情况下，元素的默认背景覆盖范围为边框盒，当你不想要元素的背景覆盖边框或者内边距时，可以使用属性**background-clip**修改背景的覆盖范围
```javascript
background-clip：border-box（默认值）
background-clip：content-box（内容盒）
background-clip：padding-box（填充盒）
```

#### 3）溢出处理
当你定义的div里面的内容超出div设置的宽高时，内容就会溢出，显示出的内容就会很难看
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408171808952.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70#pic_center)
这时候可以引入属性**overflow**处理
```javascript
overflow:hidden（隐藏溢出部分）;
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408172016448.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
```javascript
overflow:scroll（包含overflow-x：scroll和overflow-y：scroll,表示在x、y方向生成滚动条，也可单独只在x、y方向生成滚动条）
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408172313284.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
```javascript
overflow:auto（最常用，当内容溢出的时候生成滚动条）
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408172458723.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
#### 4）溢出处理的简单应用
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020040817402849.png#pic_center)
上图所示的图片表示当文本溢出的时候不显示溢出部分，只显示三个点...
该如何实现这个功能呢
定义一个无序列表，显示样式
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408174257936.png)
```javascript
white-space: nowrap;（表示不换行）
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408174352947.png)
```javascript
overflow: hidden;（溢出部分隐藏）
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408174514144.png)
```javascript
text-overflow: ellipsis;（将溢出的内容显示三个点）
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200408174612306.png)
OK，该功能就完成了。
