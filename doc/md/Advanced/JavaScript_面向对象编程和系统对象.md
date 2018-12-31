---
title:  JavaScript 面向对象编程和系统对象
date: 2018-12-19 16:21:11
updated: 2018-12-19 16:21:11 
mathjax: false
categories: 
tags:
typora-root-url: JavaScript_面向对象编程和系统对象
typora-copy-images-to: JavaScript_面向对象编程和系统对象
top: 1
---


# 六、==JavaScript面向对象（重要）==

## 6.1、什么是对象

我喜欢大眼睛、长头发、大长腿、白皮肤、会洗衣服、会做饭、会生孩子的女孩，比如有孙俪，范冰冰。

这句话中描述的人的特点就是对象的属性，后面的两个人就是符合这个类的实例，也就是对象。

## 6.2、面向对象编程

​	面向对象编程简称OOP（Object-Oritened Programming）为软件开发人员敞开了一扇大门，它使得代码的编写更加简洁、高效、可读性和维护性增强。它实现了软件工程的三大目标：（代码）重用性、（功能）扩展性和（操作）灵活性，它的实现是依赖于面向对象的三大特性：封装、继承、多态。在实际开发中使用面向对象编程可以实现系统化、模块化和结构化的设计。它是每位软件开发员不可或缺的一项技能。

## 6.3、JavaScript自定义对象

​	回顾PHP，要得到一个对象，必须先定义一个类，然后通过 `new` 关键字实例化类，才能得到对象。另外，在实例化对象的时候，构造函数会自动执行。

```php

class Person {
    public $eyes = '眼睛大';
    public $legs = '腿长';
    //
    public function __construct(){
        echo $this->eyes;
    }
    //
    public function cook(){
        echo '会做饭';
    }
}
//实例化对象
$sunli = new Person();
$bingbing = new Person();
```

​	在JavaScript中，准确的说是在==E==CMA==S==cript5中，没有明确类的概念，只有函数，所以要想得到一个自定义的对象，只能使用关键字 `new` 实例化一个函数。

> 在ES6中，才有类的概念。

==如果一个函数被实例化了，那么这个函数就叫做构造函数==，在学习的时候，==我们可以把构造函数当做类==。

10自定义对象.html  代码：

```javascript
//定义一个函数,下面实例化了这个函数，所以这个函数就叫做构造函数，也可以认为是类
function Person(){

}

//实例化这个函数，得到对象
var sunli = new Person();
var bingbing = new Person();
console.log(typeof sunli, typeof bingbing);
```

在PHP中，构造函数，在实例化对象之后，会自动执行，JavaScript中的构造函数也有相同的特点：

```javascript
	//定义一个函数,下面实例化了这个函数，所以这个函数就叫做构造函数，也可以认为是类
    function Person(){
        console.log('123');
    }

    //实例化这个函数，得到对象
    var sunli = new Person();  // 123
    var bingbing = new Person();  // 123
```



## 6.4、this关键字和对象成员

在JavaScript面向对象中，this也是一个伪对象，只能出现在构造函数内部。表示该构造函数的任意对象。

> this很好理解，它和PHP中的 $this一个意思。

定义一个构造函数，并添加一些成员属性和成员方法：

```javascript

    //定义构造函数
    function Person(){
        //public $eyes = 'asdf';
        //定义成员属性
        this.eyes = '大';
        this.legs = '短';
        this.hair;

        //定义成员方法
        this.cook = function(){
            console.log(this.eyes);
        };
        this.wash = function(){
            this.cook();//调用当前对象的成员方法
        };
    }
    var sunli = new Person();
    sunli.wash(); //调用成员方法
	//在实例化得到对象之后，也可以为对象添加成员
    sunli.hair = '短发';
    console.log(sunli.hair);
	//为sunli 添加成员方法
    sunli.sing = function(){
        console.log('sing a song');
    };
    sunli.sing();

```



## 6.5、delete关键字删除对象成员

前面学习过，在JavaScript中，delete可以删除没有var声明的变量。

delete关键字还可以删除对象中的成员，既可以删除成员属性，也可以删除成员方法

12delete删除对象成员.html  

```javascript
/*var a = 1;
b = 2;
delete a;
delete b;
console.log(a, b);*/

function Dog(){
    this.eyes = '大';
    this.name = '大黄';
    this.jiao = function(){
        console.log('汪汪汪');
    }
}

//实例化一个小狗
var dog1 = new Dog();
//delete dog1.eyes;  //删除对象的成员属性
console.log(dog1.eyes);
//delete dog1.jiao;  //删除对象的成员方法，方法不能带小括号。
dog1.jiao();
```



## 6.6、对象在内存中的存在形式

```javascript
	function Person(){
        this.eyes = '长';
        this.cook = function () {
            console.log('做得一手好饭');
        }
    }

    var sunli = new Person();

    var bingbing = sunli; //将sunli赋值给bingbing，赋的是对象sunli指向堆区的地址
    bingbing.eyes = '大'; //修改bingbing的eyes属性
    console.log(sunli.eyes); //大
```

对应的内存图：

![1532766667149](1532766667149.png)

```javascript
function Person(){
    this.eyes = '长';
    this.cook = function () {
        console.log('做得一手好饭');
    }
}

var sunli = new Person();

var bingbing = sunli; //将sunli赋值给bingbing，赋的是对象sunli指向堆区的地址
/*bingbing.eyes = '大'; //修改bingbing的eyes属性
console.log(sunli.eyes); //大*/
//bingbing = null;
//console.log(sunli);

function change(o){
    o.eyes = '大又圆';
}

change(bingbing);

console.log(bingbing.eyes, sunli.eyes); //大又圆 大又圆
```



## 6.7、直接量语法定义对象

直接量语法定义对象，也就是不用定义构造函数，而是直接定义一个变量，然后用一对大括号 `{}` 表示对象，这种形式的对象，里面也可以有成员属性和成员方法。

这部分知识前面已经学习过了。下面试着定义几个对象：

```javascript
var a = {}; //空对象
var b = {name:'赵伟', age:21}; //对象中可以有成员属性
var c = {
    name:'宋江',
    age:35,
    nickname:'及时雨',
    chaodai:'宋'
};
var d = {
    name:'宋江',
    age:35,
    nickname:'及时雨',
    chaodai:'宋',
    fn1:function () {
        console.log(this.name);
    },
    fn2:function () {

    }
};

//d.成员;
d.fn1(); //宋江
```



# 七、==系统对象==（会查手册）

内置对象，即JavaScript预定义的一些对象，这些对象中定义好了一些常用的方法。我们直接实例化（有些不需要实例化）这些对象，然后就可以使用这些方法了。

这部分涉及到的方法非常多，要求会查手册。手册位置：w3c手册---点导航的JavaScript—点左侧的JavaScript—点右侧的参考书。 

## 7.1、Object对象

​	目前，可以认为Object是一个空对象。

​	Object对象也是一个构造器（构造函数），这个对象是其他所有对象的父对象，也就是说其他所有的对象都继承Object对象。==其他所有对象，包括DOM对象==。

## 7.2、String对象

字符串对象，对象内置了很多实用的属性和方法。

使用方法：

1. 实例化String，并将要操作的字符串传递进去，然后通过对象调用成员。
2. 把字符串当做对象，直接使用字符串调用成员。

```javascript
/****************** 下面演示使用String对象的两种方式 *******************/

//方式一：实例化String、传入要操作的字符串。然后使用对象去调用String对象的成员
var s = new String('hello');
console.log(s.length); // 5

//方式二：直接把字符串当做对象，然后调用String对象中的属性或方法
console.log('hello'.length); // 5
```

下面演示一些常用的字符串方法：

```javascript
/********************************* indexOf() ************************/
/*
检测字符串中是否含有指定字符，存在返回首次出现位置，不存在返回-1
*/
console.log('hello'.indexOf('e')); // 1
console.log('hello'.indexOf('h')); // 0
console.log('hello'.indexOf('a')); //-1


/********************************* substr() ************************/
/*
截取字符串。
两个参数，参数1表示起始位置,可以是负数；参数2可选，表示长度，非负，不填表示截取到结尾
*/
console.log('hello'.substr(1));// ello
console.log('hello'.substr(1,2));// el
console.log('hello'.substr(-3,2));// ll

/********************************* substring() ************************/
/*
截取字符串。
两个参数，都是非负数。分别表示起始位置和结束位置，参数2不写表示到结尾
*/
console.log('hello'.substring(1,2));//e

/********************************* slice() ************************/
/*
截取字符串。
两个参数，参数1表示起始位置，可以是负数。参数2表示结尾位置。注意结尾位置不能在起始位置之前。
*/
console.log('hello'.slice(1,2)); //e
console.log('hello'.slice(-3,2)); //ll


/********************************* split() ************************/
/*
将字符串分割成数组。
两个参数，参数1表示分隔符，参数2可选，表示数组的最大长度
*/
console.log('hello'.split('l')); //Array [ "he", "", "o" ]
console.log('hello'.split('l', 2)); //Array [ "he", "" ]

/********************************* replace() ************************/
/*
替换字符串中的值。
两个参数，参数1表示查找的值，参数2表示替换后的值。支持正则
*/
console.log('hello'.replace('l', 'k')); //heklo  只替换一次
console.log('hello'.replace(/l/g, 'k')); //hekko 使用正则全部替换，有关正则，后天学习

/********************************* trim()IE9支持 ************************/
/*
去掉字符串两边的空白。
*/
console.log('  world  '.trim()); //world
```

通过浏览器可以查到系统对象中有哪些成员，方法是在浏览器的console区，输出String.prototype.

![1532769108592](1532769108592.png)

## 7.3、Date对象

使用方法，先new Date()，得到一个对象，然后用这个对象调用它里面的成员方法。 

```javascript
var date = new Date(); //实例化Date对象
console.log(date.getFullYear()); //调用getFullYear()方法，获取"年"
```

下面演示通过Date对象，获取当前的时间，格式为：“年-月-日 时:分:秒”

```javascript
//自定义函数，判断如果数字小于10，则在其前面加0。如把 9 变成 09
function check(x){
	if(x<10){
		return '0'+x;
	}
	return x;
}
//实例化对象
var d = new Date();
//console.log(d); //Date 2018-04-14T07:13:15.554Z
var year = check(d.getFullYear());
var month = check(d.getMonth() + 1);
var day = check(d.getDate());
var hour = check(d.getHours());
var minute = check(d.getMinutes());
var second = check(d.getSeconds());

var t = year+'-'+month+'-'+day+' '+hour+':'+minute+':'+second;
console.log(t);
```

## 7.4、Array对象

数组就是对象，所以可以直接使用数组调用Array对象的成员属性和方法。

下面演示常用的Array对象的成员属性和方法：

```javascript
//定义用于测试的数组
var arr1 = ['a', 'b', 'c', 'd'];

//length属性，表示数组中单元个数，即数组的长度
console.log(arr1.length); // 4

//concat()方法，连接一个或多个数组
console.log(arr1.concat(arr2)); //Array [ "a", "b", "c", "d", "e", "f", "g" ]

//join()方法，将数组单元连接成字符串，默认的分隔符是逗号，也可以自己指定分隔符
console.log(arr1.join()); //a,b,c,d
console.log(arr1.join(''));//abcd

//pop()方法，删除并返回数组的最后一个元素
console.log(arr1.pop()); //d
console.log(arr1);//Array [ "a", "b", "c" ]

//定义用于测试的数组
var arr2 = ['e', 'f', 'g'];

//push()方法，向数组的末尾添加一个或更多元素，并返回新的长度。
console.log(arr2.push('hhh')); // 4
console.log(arr2); //Array [ "e", "f", "g", "hhh" ]

//reverse()方法，颠倒数组中元素的顺序。
console.log(arr2.reverse()); //Array [ "hhh", "g", "f", "e" ]
```

## 7.5、Math对象

用法：无需实例化对象，直接使用“ `Math.成员`”即可，比如 `Math.random();`  

下面列举一些Math对象属性和方法：

```javascript
//属性：
//PI : 表示圆周率，用法Math.PI
console.log(Math.PI); //3.141592653589793

//方法：
//abs(x)   返回数的绝对值。 正数的绝对值是它本身，负数的绝对值是它的相反数。
console.log(Math.abs(-3)); // 3
console.log(Math.abs(3)); // 3

//ceil(x)   对数进行上舍入。
console.log(Math.ceil(3.1)); // 3

//floor(x)  对数进行下舍入。
console.log(Math.floor(3.8)); // 3

//round(x)  把数四舍五入为最接近的整数。
console.log(Math.round(2.5)); // 3

//max(x,y) 返回 x 和 y 中的最高值。
console.log(Math.max(3,1)); // 3

//min(x,y) 返回 x 和 y 中的最低值。 
console.log(Math.min(3,5)); // 3

//random() 返回 0 ~ 1 之间的随机数。包含0，不包含1。[0,1) 
console.log(Math.random());

//随机整数公式：Math.floor(i + Math.random() * (j – i + 1))
//公式中的i表示小的数，j表示大的数
//获取1~10之间的随机数
var suiji = Math.floor(1 + Math.random() * (10-1+1));
console.log(suiji);
```

## 7.6、window对象

window对象和下面要讲到的 Navigator、Screen 、History 、Location都属于浏览器对象，即BOM对象。

javascript:ECMAScript  DOM  BOM

==window对象的成员在被调用时，可以省略window==。

下面列举window对象中常用方法：

```javascript
alert(); -- 弹出一个警告框
confirm('你确定要删除吗');  点击确定返回true，点击取消返回false
prompt() – 弹出一个可输入的对话框，点击确定返回输入的内容，点击取消返回null
```

 open方法用于打开一个新浏览器窗口，经常用于弹窗。下面演示open方法的使用：

```html
<input type="button" value="手机预览" id="btn" />
<script>
    document.getElementById('btn').onclick = function () {
		//window.open('新窗口url','新窗口名字','新窗口属性');
		window.open('http://www.blog.com', '手机版博客', 'width=600,height=500');
	}
</script>
```

window对象中定时器方法也是非常有用且常见的方法：

基本用法如下：

```javascript
var s =setTimeout("js代码或js函数", 毫秒数) //表示多少毫秒后，执行前面的js代码或函数，只执行一次
var t =setInterval("js代码或js函数", 毫秒数) //表示每隔多少毫秒，执行一次前面的js代码或函数。
clearTimeout(s); //清除由setTimeout产生的定时器
clearInterval(t); //清除由setInterval产生的定时器
```



## 7.7、navigator对象

 navigator对象包含有关浏览器的信息。

没有应用于 navigator 对象的公开标准，不过所有浏览器都支持该对象。

经检测，navigator对象中有用的属性只有一个，它是 `navigator.userAgent`，从这个结果中可以查看到浏览器及浏览器的版本。 

```javascript
console.log(navigator.userAgent); //不同浏览器结果不同
```

## 7.8、screen对象

屏幕对象，通过该对象可以获取到电脑显示器的高度和宽度。

```javascript
document.write(screen.width + "*" + screen.height); //输出分辨率，宽度*高度
document.write(screen.availWidth + "*" + screen.availHeight); //不包含任务栏的高度和宽度
```

## 7.9、history对象

history 对象包含用户（在浏览器窗口中）访问过的 URL。

```javascript
history.back(); //加载 history 列表中的前一个 URL。 相当于后退 
history.forward(); //加载 history 列表中的下一个 URL。 相当于前进
history.go(); //加载 history 列表中的某个具体页面。 通过参数指定跳转到哪个页面
```

## 7.10、location对象

location 对象包含有关当前 URL 的信息。

下面是location对象的一些属性：

```javascript
document.write(location.hash + '<br>'); // 设置或返回从井号 (#) 开始的 URL（锚）。
document.write(location.host + '<br>'); // 设置或返回主机名和当前 URL 的端口号。
document.write(location.hostname + '<br>'); // 设置或返回当前 URL 的主机名。
document.write(location.href + '<br>'); // 设置或返回完整的 URL。
document.write(location.pathname + '<br>'); // 设置或返回当前 URL 的路径部分。
document.write(location.port + '<br>'); // 设置或返回当前 URL 的端口号。
document.write(location.protocol + '<br>'); // 设置或返回当前 URL 的协议。
document.write(location.search + '<br>'); //设置或返回从问号 (?) 开始的 URL（查询部分）。
```

location对象中比较有用的方法是 `reload()`.它可以刷新当前的页面：

```javascript
location.reload(); //刷新页面，和点击刷新按钮一个效果
location.reload(true); //清除缓冲刷新，和按住Ctrl点击刷新按钮一样
```

```html
<input type="button" value="刷新" id="sx">

<script>
    document.getElementById('sx').onclick = function () {
        location.reload(); //和按F5、或点击浏览器的刷新按钮一样
        location.reload(true); //强制刷新。和Ctrl+F5一样。表示清除缓存刷新
    }
</script>
```





