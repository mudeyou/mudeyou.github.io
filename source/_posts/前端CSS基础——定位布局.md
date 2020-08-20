### 定位布局

 - 定位布局：手动控制元素在包含块中的精准位置
 - 定位布局的属性：position
 
 - position：static（默认值，不定位）
 - position：relative（相对定位）
- position：absolute（绝对定位）
- position：fixed：（固定定位）

只要元素加上属性position（排除static），那么这个元素就是个**定位元素**，定位元素在排列时会脱离常规流排列，即类似于常规流在排列时无视浮动盒子一样。总结起来就是
**一个脱离了常规流的元素，在常规流的排列时会无视脱离了常规流的元素，并且常规流在计算高度时会忽略脱离常规流的元素高度。**

#### 相对定位
在**position**的属性中，**relative**（相对定位）比较特殊，相对定位不会脱离常规流排列，只是让元素在原来的位置上产生偏移而不影响其他元素的位置。

 - left：左偏移
 - right：右偏移
 - top：上偏移
 - bottom：下偏移

举例说明
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412221623465.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
偏移并不会对其他元素造成影响
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020041222133777.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)

小细节：

 1. 当relative取值出现冲突时，例如  
```javascript
  left:30px;  right:30px; || top:30px;  bottom:30px; 
```
     在这种情况下，默认取**left、top**的值，在实际开发中需要尽量避免这种情况的发生。
     
 2. 在未设置宽度的情况下，**margin-left**与**left**看起来同样是左偏移，但是margin-left会缩短**边框盒的宽度**，而相对定位不会。
 3. 在一般情况中，很少用relative来确定元素的位置，relative通常用来作为**absolute**（绝对定位）或者**fixed**（固定定位）的包含块

#### 绝对定位
绝对定位与其他定位最大的不同点是包含块的不同，绝对定位的包含块是其祖先元素的第一个定位元素的**填充盒**（向上找祖先元素），若祖先元素没有定位元素，则绝对定位的包含块为整个网页（也称为初始化包含块）
例如

```
	 .relative{
        background-color: skyblue;
        width: 500px;
        height: 300px;
        border: 1px solid;
        margin: 20px;
        position: relative;
    }

    .test{
        background-color: #008c8c;
        width: 300px;
        height: 200px;
        border: 1px solid;
        margin: 20px;
    }
    
    .absolute{
        background-color: #fff;
        width: 50px;
        height: 50px;
        border: 1px solid;
        position: absolute;
        left:0;
        top: 0;
    }
    
	<div class="relative">//祖先第一个定位元素
        <div class="test">
            <div class="absolute"></div>
        </div>
    </div>
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412232655209.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)

```
 	.relative{
        background-color: skyblue;
        width: 500px;
        height: 300px;
        border: 1px solid;
        margin: 20px;
        position: relative;
        /* position: relative; */ //去掉祖先元素的定位元素
    }

    .test{
        background-color: #008c8c;
        width: 300px;
        height: 200px;
        border: 1px solid;
        margin: 20px;
    }
    
    .absolute{
        background-color: #fff;
        width: 50px;
        height: 50px;
        border: 1px solid;
        position: absolute;
        left:0;
        top: 0;
    }
    
	<div class="relative">//祖先元素无定位元素
        <div class="test">
            <div class="absolute"></div>
        </div>
    </div>
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020041223284541.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
#### 固定定位
固定定位和绝对定位完全一样，只有一点不同：**包含块的不同**

 - 固定定位的包含块是整个浏览器的可视化窗口
 - 需要注意的是，绝对定位的初始化包含块与浏览器可视化窗口的不同在于可视化窗口可以随着页面的滚动而滚动，从而保持在浏览器窗口的位置不变，而初始化包含块不会随着页面的滚动，它只能保持在页面中的位置不变。
 - 固定定位多数应用于导航栏或者回到顶部标签等需要随着页面滚动而滚动的

#### 固定定位与绝对定位的居中
居中的设置

 1. 若要水平方向居中，需要定宽；若要垂直方向居中，需要定高
 2. 在水平方向居中：将left、right距离设置为0，margin设置为auto
 3. 在垂直方向居中：将top、bottom距离设置为0，margin设置为auto
 4. 在水平垂直方向居中：将left、right、top、bottom距离设置为0，margin设置为auto

