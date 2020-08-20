### 水平居中
水平居中分为三种，一种是行盒（行块盒）模型居中，一种是常规流块盒模型居中，一种是定位元素的水平居中

#### 行盒（行块盒）水平居中

> 在父级元素添加属性 text-align: center（行块盒同理）

```javascript
	div{
            height: 100px;
            background-color: aqua;
            text-align: center;//
        }
    <div>
        <span>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Rem, distinctio?</span>
    </div>
```
实现效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508155514179.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)

#### 常规流块盒水平居中

> 给定宽，设定margin左右两边的值为auto

```javascript
		div{
            height: 100px;
            background-color: aqua;
        }
        span{
            display: block;
            width: 50px;
            height: 50px;
            background-color: #008c8c;
            margin: 0 auto;
        }
     <div>
        <span></span>
    </div>
```
实现效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508160152892.png)

#### 定位元素的水平居中

> 设定父类元素position：relative，设定子类元素position:absolute，left,right都为零，margin左右的值设定为auto（fixed同理）

```javascript
		div{
            height: 100px;
            background-color: aqua;
            position: relative;
        }
        span{
            display: block;
            width: 50px;
            height: 50px;
            background-color: #053131;
            position: absolute;
            left: 0;
            right: 0;
            margin: 0 auto;
        }
	<div>
        <span></span>
    </div>
```
效果如图
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020050816240282.png)

### 垂直定位
在CSS中，完美的垂直居中方式比较有限，较为完美的就是利用定位元素实现垂直居中，在CSS3中有更好的居中方式，目前只讨论CSS的垂直居中方式。
#### 单行文本的垂直居中

> 在单行文本中，可以设定行高跟整个区域的高度相等

```javascript
	div{
            height: 50px;
            line-height: 50px;
            background-color: aqua;
        }
        
    <div>
        <span>Lorem ipsum dolor sit amet.</span>
    </div>
```
实现效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508163209336.png)

#### 多行文本的垂直居中（在块盒或者行块盒模型内）

> 不设置父元素的高度，在父元素中添加相同的top，bottom的padding实现视觉效果上的垂直居中

```javascript
 	div{
            width: 200px;
            background-color: aqua;
            padding: 30px 0;
        }
	<div>
        <span>多行文本的垂直居中多行文本的垂直居中多行文本的垂直居中</span>
    </div>
```
实现效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508163952725.png)

#### 定位元素的垂直居中

> 定高，设定父类元素position：relative；子类元素position：absolute；（固定定位同理）设定top，bottom的值为0，再设定margin上下的值为auto

```javascript
		div{
            width: 200px;
            height: 300px;
            background-color: aqua;
            position: relative;
        }
        span{
            height: 65px;
            background-color: #008c8c;
            position: absolute;
            top: 0;
            bottom: 0;
            margin: auto 0;
        }
	<div>
        <span>多行文本的垂直居中多行文本的垂直居中多行文本的垂直居中</span>
    </div>
```
效果如图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508165147322.png)
