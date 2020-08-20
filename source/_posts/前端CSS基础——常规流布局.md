### 常规流
常规流又称为文档流，是页面布局规则之一，所有元素在默认情况下都是常规流布局，它的总体规则是块盒独占一行，行盒水平依次排列。在了解常规流布局前，需要引入一个概念，**包含块**。

 1. **包含块**
在绝大部分情况下，包含块指父类元素的内容盒**content-box**,每个盒子都有它的包含块，包含块决定了盒子之间的排列次序.

 2. **块盒**
 块盒一般指子元素的整个盒子模型，块盒的总宽度必须刚好等于包含块的宽度。
 

```
<div class="father">//content-box为包含块
	<div class="child">//整个盒子模型为块盒
	</div>
</div>
```
#### 块盒的取值问题

 1. 块盒的宽度
块盒的宽度取值默认是auto,表示**将剩余空间填充**。例如包含块的宽度为1000px，而块盒的宽度未设定，则块盒的总宽度为1000px。
当没有设置宽度时，块盒宽度等于包含块宽度。
当设置宽度时，若块盒宽度不等于包含块宽度，则剩下空间由margin-right填充。
margin的默认值为0，可以设定为auto。**可以在设定宽度后，将margin的左右值设定为auto实现块盒的居中。**

```javascript
包含块宽度（父类content-box宽度）= 块盒总宽度（块盒margin宽度+块盒border宽度+块盒padding宽度+块盒content宽度）
```

 2. 块盒的高度
块盒的高度适应于包含块的高度，若包含块没有设定高度，则块盒的高度随内容变化而变化，包含块高度=块盒高度（默认取值auto）

 1. 百分比取值
padding、margin的取值可以设定为百分比取值，但是它们所有百分比都相对于包含块的宽度。例如：

```javascript
.father{
	width:100px;
	padding:200px;
	margin:300px;
}
.child{
	padding:50%;//等于50px，而不是100px
	margin:50%;//等于50px，而不是150px
}
<div class= "father">
	<div class = "child"></div>
</div>
```

 4. 高度的百分比取值
1）当包含块未设置固定高度时，包含块的高度取决于块盒的高度，设置百分比无效
2）当包含块设置固定高度时，块盒的高度百分比取决于包含块的高度。


#### 上下边距的合并问题

 1. 两个常规流块盒，不管是兄弟元素还是父子元素，只要外边距相邻，就会进行合并。
例如：

```javascript
.father{
	background:skyblue;//背景颜色
	width:200px;//宽200px
	height:200px;//高200px
	margin-top:30px;//外边距30px
}
.child{
	background:red;//背景颜色
	width:50px;//宽度
	height:30px//高度
	margin-top:30px;//外边距30px
}
<div class= "father">
	<div class = "child"></div>
</div>
```
上图代码想表示的结果是父元素上外边距30px，子元素距离父元素上外边距30px，运行的理想效果是这样的：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020040921114073.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
但实际运行是这样的
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020040921121755.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
这就是因为**father**的**margin-top**与**child**的**margin-top**的外边距相邻导致合并了，这也是我们在开发中经常遇到的问题，那么该如何解决呢，我们只需要在相邻边距中间加个**border**或者将**块盒的margin属性转化成包含块的padding属性**，就可以实现了。