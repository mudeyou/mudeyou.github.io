---
title: 深入理解JS预编译——AO对象及GO对象
---
### JS预编译
JS有两个特性，一个是单线程，一个是解释性语言。不同于编译性语言，解释性语言通常理解为不整体编译，由解释器解释一句执行一句。但JS不是直接对着代码解释执行，在解释执行之前，需要进行其他的步骤。

JS运行步骤：

 1. 语法分析
 2. 预编译
 3. 解释执行

预编译有个特点：**任何变量，如果未声明就赋值，那该变量为全局变量，**即**暗示全局变量（imply global）**。并且所有的全局变量都是window的属性。

简单看一下预编译例子：

```javascript
	<script>

        test();
        function test(){
            console.log('a');
        }
        
    </script>
```
正常来讲，代码执行从上到下，先执行test()，再执行后面的函数声明，所以预期结果应该是不输出a的，但是结果是输出a的。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512211236943.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)

再看一个例子：

```javascript
    <script>
        console.log(a);
        var a = 123;
    </script>
```
a的声明在后，按道理应该报错，因为还没有到a的声明赋值，并不存在a变量，但是运行结果为：undefined
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512211426264.png)
这就是因为JS在执行前，先进行了预编译。
#### AO对象
AO对象全称为：activation object （活跃对象/执行期上下文），在函数执行前执行函数预编译，此时会产生一个AO对象，AO对象保存该函数的参数变量。

##### 函数预编译步骤

>  1. 产生AO对象
> 
>  2. 将函数的参数以及函数里面声明的变量当做AO对象的属性名，值全部为undefined。
>  3. 将实参的值赋值给形参。
>  4. 在函数里面声明的函数，函数名作为AO对象的属性名，值赋值给函数体。（若参数名和函数名重叠，则函数体值会覆盖参数值）

##### 实战理解

```javascript
    <script>
        function test(a) {
            console.log(a);
            var a = 2;
            console.log(a);
            function a () {}
            console.log(a);
            var b = function () {};
            console.log(b);
            function d(){}
        }
        test(1);
    </script>
```

 1. 创建AO对象
AO{
	//此时AO对象为空
	}

2. 确定AO对象的属性名
AO{
	a：undefined;			**//函数参数**
	b：undefined;		 	**//函数里面声明的变量**
	}

3. 将实参值赋值给形参
AO{
a：1; //函数参数
b：undefined; //函数里面声明的变量
}
4. 处理函数里面的声明函数
AO{
a：~~1;~~  function a () {} //变量名一样，值覆盖
b：undefined; //函数里面声明的变量
d：function d () {};
}

此时函数预编译已经完成的，预编译后执行代码：
第一条执行的是控制台打印出a的值，所以输出function a () {}； 
第二条语句赋值给a，则AO对象中a的值被覆盖为2；
第三条语句控制台打印a的值为2；
第四条为声明，预编译处理过所以直接跳过；
第五条打印出a的值，一样为2；
第六条为赋值，赋值b的值为function () {}；
第七条打印出b的值function () {}；
第八条声明，预编译处理过所以直接跳过；

所以输出结果应该是
**function a () {}；
2；
2；
function () {}；**
执行效果如图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512214510729.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)

#### GO对象
GO对象全称为 global object（全局对象，等同于window），在开始预编译时产生的对象，比AO对象先产生，用于存放全局变量，也称为全局作用域。

##### 预编译三步骤

>  1. 生成GO对象
> 2. 将变量声明的变量名当做GO对象的属性名，值为undefinded
> 3. 将声明函数的函数名当做GO对象的属性名，值为函数体

##### 实战理解

```javascript
    <script>
		console.log(a);
        var a = 123;
        function a () {
        }
        console.log(a);     
    </script>
```

 1. 生成GO对象
GO{

	}
 2. 将声明变量添加进GO对象
 GO{
 a：undefined；
 }
3. 将声明函数添加进GO对象
GO{
a：~~undefined~~ ；function a () {}；//覆盖a的值
}

按顺序执行代码
第一次输出结果为：function a () {}
第二次输出结果为：123

执行结果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512222713240.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)
#### 实战深入理解AO、GO
求输出结果

```javascript
        console.log(a);
        a = 100;
        function test() {
            console.log(a);
            a = 200;
            console.log(a);
            var a = b = 300;
        }   
        test();
        console.log(b);
        var a;
        console.log(a);
```

 1. 生成GO对象
  GO{
  }
  2. 将声明变量添加进GO对象内，值为undefined
GO{
a：undefined；
       }
   
   3. 将声明函数添加进GO对象呢，值为函数体
   GO{
   a：undefined；
   function test() { ...... }；
   }
4. 预编译完成，执行代码：输出a，此时a的值为：**undefined**
5. a赋值，此时GO对象内的a值变为100
GO{
a：100；
function test() { … }；
}
6. 执行函数test（），生成AO对象
AO{

	}
7. 将函数声明的变量添加进AO对象，值为undefined
AO{
a：undefined；
	}
8. 函数没有传递参数，跳过函数预编译的第三步
9. 函数里面没有声明函数，跳过函数预编译的第四步
10. 执行函数，打印a，此时AO里面有属性a，则输出AO里面a的值，即输出： **undefined** 
11. AO的a赋值200，此时AO的a的值为200
AO{
a：200；
}
12. 输出a的值：**200**
13. 将300的值赋值给b再赋值给a，此时b未声明，所以b为全局变量，将b添加进GO对象内，将a的值改为300
GO{
a：100；
function test() { … }；
b：300；
}
AO{
a：300；
}
14. 输出a的值：**300**，函数执行完成
15. 输出b的值：**300**
16. 输出a的值，此时a的值为GO里面的值：**100**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512224857183.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)

再举个例子

```javascript
		//GO{
		//生成的GO对象
		//a：undefined；
		//test：function test(){ ... }；
		//}
        function test() {
            console.log(b);//undefined
            if (a) {//AO里面没有a的属性，自动寻找GO里面a的属性，此时a的值为undefined，语句不执行
                var b = 50;
            }
            console.log(b);//undefined
            c = 100;//未声明则为全局变量，添加在GO对象内
            console.log(c); //100
        }
        var a;
        test();//执行函数预编译
        //AO{
        //生成的AO对象
		//b：undefined;
		//}
        a = 10;//GO里面的a赋值为10
        console.log(c);//100
```
输出结果为：
undefined
undefined
100
100

执行结果为：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512230041294.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDkwOTY4Mw==,size_16,color_FFFFFF,t_70)