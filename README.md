# Javascript 笔记

## 变量

- 命名必须是字母或者“_”或“$”开头
- 长度不超过255字符
- 不允许使用空格
- 不能要使用脚本语言中的保留字和关键字以及保留符号命名
- 区分大小写

**javascript 常用关键字**
|           |          |            |        |
| --------- | -------- | ---------- | ------ |
| break     | do       | instanceof | typeof |
| case      | else     | new        | var    |
| catch     | finally  | return     | void   |
| continue  | for      | switch     | while  |
| debugger* | function | this       | with   |
| default   | if       | throw      | delete |
| in        | try      |            |        |

**声明多个变量**

```javascript
var one=10, two = 20, three = 30;// 相当于下面 都有var
var one = 10;
var two = 20;
var three = 30;

var one = two = three = 10;  // 相当于下面 two three 没有var
var one = 10;
    two = 10;
    three = 10;
```

经典面试题(变量作用域)
``` javascript
fn1();
console.log(c);
console.log(b);
console.log(a);
function fn1(){
    var a = b = c = 9;
    console.log(a);
    console.log(b);
    console.log(c);
}
// => 9 9 9 9 9 err:a is not defined
/* ----- 上边等价于 ----- */
fn1();
console.log(c); // => 9 第四个 
console.log(b); // => 9 第五个
console.log(a); // => a is a not defined
function fn1(){
    var a = 9; //（局部a）
        b = 9; //（全局b）
        c = 9; //（全局c）
    console.log(a); // => 9 第一个
    console.log(b); // => 9 第二个
    console.log(c); // => 9 第三个
}
```
> 在函数内部，没有var声明的变量当做全局变量看

**变量提升**

1.function 函数作用域里的变量会遮盖了上层作用域变量。
2.在function作用域内，变量的声明被提升了(只提升声明)。

``` javascript

var num = 10;
fun();
function fun(){
    console.log(num);
    var num = 20;
}
//相当于转为为下面代码
var num = 10;
fun();
function fun() {
    var num;   // 带有var 的变量 提升到 function 作用域的最顶层
    // 只提升变量  ，不给值
    console.log(num);
    num = 20;
}

```



## 数据类型

``` javascript
nsole.log(typeof 10);  // => number
console.log(typeof "abc");  // => string
console.log(typeof true);  // => boolean
console.log(typeof null);  // 空类型 => object
var test;
console.log(typeof test);  // => undefined

```

**null详解**

``` javascript
null == "" // => false
null == undefined // => true
null === undefined // => false

null + 10 // => 10
undefined + 10 // => NaN(not a number)
```

**取整函数**
parseInt(字符，解析数字的基数)

``` javascript
console.log(parseInt(11,8));  //  把8进制的11 转换为10进制
console.log(parseInt("11",2)); //  把2进制的11 转换为10进制
console.log(parseInt("11ab")); //  => 11
console.log(parseInt("11ab11")); //  => 11
console.log(parseInt("ab11")); //  => NaN
```


## 运算符

**++a 和 a++**
++a 先加一再运算
a++ 先运算再加一(下次运算的时候才是加一的值)

``` javascript

var a=10, b=20 , c=30;
    ++a; // => a=11
    a++; // => a=12
    e= ++a + (++b) + (c++) + a++;
    // a=13   b=21    c=30   a=13
    // 在运算中因为(++a)所以a的值已经变为13,最后的（a++）是13参与了运算
alert(e) // => 77
alert(a) // => 14

```

## 数组

### 数组方法

#### 添加方法

**push()** 往数组最后添加一个或多个元素，原数组改变`arr.push(a，b)`返回新的数组长度
**unshift()** 往数组最前面添加一个或多个元素，原数组改变`arr.unshift(a)`返回新的数组长度

#### 删除方法

**pop()**  删除数组最后一个元素(一次只能删除一个)，原数组改变`arr.pop()`返回删除的元素
**shift()**  删除数组第一个元素(一次只能删除一个)，原数组改变`arr.shift()`返回删除的元素

#### 连接数组

**concat()** 用于连接两个或多个数组，原数组不变`arr1.concat(arr2)`返回新数组

#### 数组转换

**join()**将数组用指定的分割符号连接成为一个字符串`arrayObject.join([separator])`,separator可选

``` javascript
var arr = [1,2,3,4];
arr.join(':') // => 1:2:3:4
```

**split()** 方法用于把一个字符串分割成字符串数组`stringObject.split(separator,howmany)`

+ 参数 separator 可选。指定要使用的分隔符。如果省略该参数，则使用逗号作为分隔符。
+ howmany 可选。该参数可指定返回的数组的最大长度

``` javascript

var txt = "2015-12-2";
var text = "中国 山东 威海 小渔村";
console.log(txt.split("-"));  // => ["2015","12",2"]
console.log(text.split(" ")); // => ["中国", "山东", "威海", "小渔村"]
```


## DOM

### 访问节点
**parentNode** 父级，当前元素的上一级

**nextSibling** 下一个兄弟节点( ie678写法)
**nextElementSibling**

**previousSibling** 上一个兄弟节点( ie678写法)
**previousElementSibling**

> nextSibling 下一个兄弟的意思， 再ie678里面是正常的，但是在谷歌，火狐浏览器里面，默认的下一个兄弟， 是空格或者是换行。

``` javascript
// 兼容写法
var two = document.getElementById("two");
var next = two.nextElementSibling || two.nextSibling;
```

**firstChild** 第一个子节点( ie678写法)
**firstElementChild**

**lastChild** 最后一个子节点
**lastElementChild**

``` javascript
// 兼容写法
var father = document.getElementById("father");
var first = father.firstElementChild || father.firstChild;
var last = father.lastElementChild || father.lastChild;
```

**childNodes** 得到所有的子节点

> 谷歌等浏览器里面， 会把 折行 也看做是一个孩子。

- nodeType  => 1  元素节点
- nodeType  => 2  属性节点
- nodeType  => 3  文本节点

**children** 获得某个节点下边所有的子孙*元素节点*只获得标签

> 在ie678中包含注释节点，没有注释可以避免


### 操作节点

**createElement()** 创建一个新元素节点 `document.createElement(“标签名”)`

**appendChild()** 追加一个节点 `a.createElement(b)`

**insertBefore()** 在特定位置(参照点的前面)添加一个节点 `a.createElement(b, c)`返回要添加的元素节点
- b参数 要插入的节点
- c参数 参照节点

``` javascript
demo.appendChild(newDiv);
var newSpan = document.createElement("span");
demo.insertBefore(newSpan,newDiv);  // 1 参数  插入的子节点   2 参数 参照节点
```

**removeChild()** 删除子节点`a.removeChild(b)`

**cloneNode** 克隆复制节点 `a.cloneNode(boolean)`参数默认为false
- 参数为true 表示深复制（复制节点及其所有子节点）
- 参数为false 表示浅复制（复制节点本身，不复制子节点）



### 属性

**getAttribute()** 获得元素的属性`a.getAttribute(“属性”)`

**setAttribute()** 设置元素的属性`a.setAttribute(“属性”, "值")`

**removeAttribute()** 删除元素的属性`a.setAttribute(“属性”)`

> 以上写法ie67不支持,一般使用a.className = "className"

**cssText** 改变多个属性设置`a.style.cssText`

``` javascript
div.style.cssText = "width:100px; height:100px;"
```

## 内置对象

|   对象名称   |  对象说明   |
| :------: | :-----: |
| Argument | 函数参数集合  |
|  Array   |   数组    |
| Boolean  |  布尔对象   |
|   Date   |  日期时间   |
|  Error   |  异常对象   |
| Function |  函数构造器  |
|   Math   |  数学对象   |
|  Number  |  数值对象   |
|  Object  |  基础对象   |
|  RegExp  | 正则表达式对象 |
|  String  |  字符串对象  |

### date日期对象

`var a = new Date()` 变量aa中包含所有的日期和时间

**常用方法**

getDate()   获取日 1-31
getDay ()   获取星期 0-6
getMonth ()  获取月 0-11 
getFullYear ()  获取完整年份（浏览器都支持）
getHours ()  获取小时 0-23
getMinutes ()  获取分钟 0-59
getSeconds ()  获取秒  0-59
getMilliseconds ()  获取毫秒         1s  =  1000ms
getTime ()  返回累计毫秒数(从1970/1/1午夜)    时间戳

### Math数学对象

**常用方法**

Math.abs()  绝对值函数 `Math.abs(-5) // => 5 `
Math.ceil()  天花板函数，向上取整 `Math.ceil(1.2) // => 2 `
Math.floor() 地板函数，向下取整 `Math.floor(1.2) // => 1 `
Math.round()  四舍五入函数 `Math.abs(1.5) // => 2 `取离他最近的整数，对于 0.5，该方法将进行上舍入

> Math.floor()  -1.2  向下取整为-2
> Math.round()  3.5 将舍入为 4，而 -3.5 将舍入为 -3。




## 定时器

**定时器 setInterval**

window.setInterval(“执行的代码串”,间隔时间);每隔设定的时间执行一次 。一般情况下省略window

> 定时器的一个重要用途就是它可以不断刷新某个区域！ 不在初始化中执行； 而且是有时间可控的。
> setInterval 不考虑函数内部执行多需要的时间，到点了就执行。可能会出现函数还没有执行完，就又执行下一次的情况

``` javascript
setInterval(function(){
  var date = new Date();
  var ms = date.getMilliseconds();
  var s = date.getSeconds()+ ms/1000;
  var m = data.getMinutes()+ s/60;
  var h = date.getHours()%12 + m/60;
  
  ss.style.webkitTransform = "rotate("+s*6+"deg)" // => 秒针在表盘上的指针度数
  
},1000)
```

**定时器 setTimeout**

setTimeout(“执行的代码串”,间隔时间); 只执行一次就结束了 

``` javascript
var num = 5;
go();
function go(){
  num--;
  if(num>0){
    setTimeout(go,1000) //函数名可以换成arguments.callee
  }else{
    window.location.href = "http://bluel.cc"
  }
}
```

> 递归调用setTimeout则会在语句执行完之后才会算时间，然后调用下一次 
> 推荐使用arguments.callee代替函数名，他表示返回正在执行的Function对象

**clearInterval()**  停止setInterval, `clearInterval(定时器的名字);` 

**clearTimeout()** 停止setTimeout, `clearTimeout(定时器的名字);`

``` javascript
clearInterval(timer);  // 先清除以前的定时器
timer = setInterval(function() {},1000)
```



## 运算符优先级

|  级别  |          运算符          |    备注     |
| :--: | :-------------------: | :-------: |
|  1   |          ()           |           |
|  2   |     !, -, ++, --      |  一元（非，负）  |
|  3   |        *, /, %        |           |
|  4   |         +, -          |           |
|  5   |     <, <=, >, >=      |           |
|  6   | =\=, != ,=\=\=, !=\=  |           |
|  7   |          &&           | “与”高于“或”  |
|  8   |         \|\|          |           |
|  9   |          ?:           |    三元     |
|  10  | =, +=, -=, *=, /=, %= | 赋值，计算完毕给值 |

**与 && 使用规则 **

`a&&b`
- 如果a为假，返回a的值(不去看b了)
- 如果a为真，返回b的值

**或 || 使用规则 **

`a||b`
- 如果a为假，返回b的值
- 如果a为真，返回a的值(不去看b了)

``` javascript
1+4 && 3 // => 3
0 && 3+1 // => 0
1 || 2 && 5-1 // => 1
```

## 字符串方法（常用）

**charAt** 获取相应位置的字符`string.charAt(index)`

**charCodeAt** 获取相应位置字符的Unicode编码值`string.charCodeAt(index)`

**indexOf** 方法可返回一个指定的字符串值第一次出现的位置（参数： 索引字符串）`"string".indexOf("s")`从前面寻找第一个符合元素的位置，找不到返回-1

**lastIndexOf** 方法可返回一个指定的字符串值最后出现的位置（参数： 索引字符串）`"string".lastIndexOf("s")`从后面寻找第一个符合元素的位置，找不到返回-1

> lastIndexOf从后往前找但是数的时候还是从前往后数

**encodeURIComponent()** 函数可把字符串作为 URI 组件进行编码

**decodeURIComponent()** 函数可把字符串作为 URI 组件进行解码

**concat 连接字符** 连接两个字符串，返回新的字符串`"txt".concat("abc")`

**slice** 指定区域截取字符串 `"asdf".slice(2,3)`=>d
- 截取位置，从 索引号2 的位置 开始截取，如果没有结束位置，则会一直截取到最后。
- 结束位置，从最左边数的个数    这里从a开始数3个 
- 截取位置如果为负数则表示，从右边开始往左边取 -1 就是取最后一个-2 就是取最后两个的意思。

**substr**  指定长度截取字符串 `"abcde".substr(2,2)`=>cd
- 截取位置，从 索引号2 的位置 开始截取，如果没有结束位置，则会一直截取到最后。
- 截取的长度，从当前位置开始数   截取几个字符
- 负值有兼容性问题

**substring** 指定区域截取字符串（同slice，只会从小往大截取）``

**toFixed** 保留设定小数位，后面小数会四舍五入`1.3548219.toFixed(2)`

**toUpperCase**  转换为大写

**toLowerCase**  转换为小写


## offset

**offsetWidth**  盒子的 (宽度 + 内边距 + 边框) 之和（不包括margin）

**offsetHeight**  盒子的 (高度 + 内边距 + 边框) 之和（不包括margin）

**offsetLeft** 返回距离上级盒子（带有定位）左边的位置

**offsetTop** 返回距离上级盒子（带有定位）顶部的位置

> 以上四个返回的都是数值不带px

**offsetParent** 返回该对象的父级 （带有定位）元素本身
 	1.如果当前元素的父级元素没有进行CSS定位（position为absolute或relative），offsetParent为body。
 	2.如果当前元素的父级元素中有CSS定位（position为absolute或relative），offsetParent取**最近的那个父级元素**。

## 动画原理

运动动画原理：  盒子本身的位置 +  步长 (步长不变为匀速运动)

``` javascript
timer = setInterval(function() {
box.style.left = box.offsetLeft + 5 + "px";
// 到了某个地方就应该停止定时器
  if(box.offsetLeft >=400) {
    clearInterval(timer);
  }
},30)
```

**缓动动画**

leader = leader  +  ( target - leader )  / 10  步长的绝对值会依次变小
- leader : 盒子本身的位置
- target : 盒子的目标位置
- ( target - leader )  / 10 : 步长


``` javascript
// 缓动动画封装(物体横向移动)
function animate (obj,target) {
  clearInterval(obj.timer)
  obj.timer =  setInterval(function(){
    var step = (target - obj.offsetLeft) / 10;
    step = step>0 ? Math.ceil(step) : Math.floor(step)
    obj.style.left = obj.offsetLeft + step +"px"
    if(target == obj.offsetLeft){
      clearInterval(obj.timer)
    }
  },30)
}
```


## 滚动scroll

`window.onscroll = function(){事件}` 

**scrollTop, scrollLeft** 被卷去的头部部分
1.怪异模式的浏览器 （未声明DTD ）    
	我们应该使用  document.body.scrollTop          scrollLeft
2.标准模式的浏览器
    我们应该使用的是  document.documentElement.scrollTop;  
3.ie9+ 以上的版本 以及正常浏览器  （除了ie678等）
	我们跟提倡 使用  window.pageYOffset;         pageXOffset  
三种方法 都是 被卷去的头部写法。

兼容写法：`var scrolltop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0;`

``` javascript
function scroll() {  // 开始封装自己的scrollTop
  if(window.pageYOffset != null) {  // ie9+ 高版本浏览器
    // 因为 window.pageYOffset 默认的是  0  所以这里需要判断
    return {
      left: window.pageXOffset,
      top: window.pageYOffset
    }
  } else if(document.compatMode === "CSS1Compat") 
  {  // 标准浏览器   来判断有没有声明DTD
    return {
      left: document.documentElement.scrollLeft,
      top: document.documentElement.scrollTop
    }
  }
  return {   // 未声明 DTD
    left: document.body.scrollLeft,
    top: document.body.scrollTop
  }
}

```


**scrollTo**  页面滚动到指定坐标

`window.scrollTo(xpos,ypos)`
- xpos	必需。要在窗口文档显示区左上角显示的文档的 x 坐标。
- ypos必需。要在窗口文档显示区左上角显示的文档的 y 坐标

window.scrollTo(0,0); 返回顶部

## 事件对象(event)

兼容性：
- 普通浏览器 event
- ie678 window.event

``` javascript
document.onclick = function(event){}
```

![event属性](https://www.tuchuang001.com/images/2017/01/24/1.png)

**pageX  pageY**

以我们的页面文档左上角  为对齐   检测 距离    它特别像  绝对定位

> ie 678 不支持pageX  pageY 只能 `pageY = clientY + document.documentElement.scrollTop`

**screenX  screenY**

用来检测 我们鼠标 距离我们电脑屏幕的 距离  

**清除选中内容**

兼容方案：`window.getSelection ? window.getSelection().removeAllRanges() : document.selection.empty();`

**client 家族**

- offsetWidth:   width  +  padding  +  border     （披着羊皮的狼）
- clientWidth： width  +  padding      不包含border
- scrollWidth:   width + padding  不包含边框   大小是内容的大小

![height.png](https://www.tuchuang001.com/images/2017/01/24/height.png)

**检测屏幕宽度(可视区域)**

clientWidth   返回的是 可视区 大小    浏览器内部的大小 
window.screen.width   返回的是我们电脑的 分辨率   跟浏览器没有关系

``` javascript
//检测屏幕宽度封装
function client() {
  if(window.innerWidth != null) {  // ie9 +
    return {
      width: window.innerWidth,
      height: window.innerHeight
    }
  }
  else if (document.compatMode === "CSS1Compat") {  // 标准模式
    return {
      width: document.documentElement.clientWidth,
      height: document.documentElement.clientHeight
    }
  }
  return {  // 怪异模式
    width: document.body.clientWidth,
    height: document.body.clientHeight
  }
}
```


**window.onresize**     改变窗口事件

window.onscroll  = function() {}  屏幕滚动事件 
window.onresize = function() {}  窗口改变事件

- 每个页面还是只能有一个这样的写法
- onresize 事件会在窗口或框架被调整大小时发生 


## 事件冒泡

事件冒泡: 当一个元素上的事件被触发的时候，比如说鼠标点击了一个按钮，同样的事件将会在那个元素的所有祖先元素中被触发。这一过程被称为事件冒泡；这个事件从原始元素开始一直冒泡到DOM树的最上层。

冒泡顺序：
- IE6.0：div -> body -> html -> document 
- 其他浏览器：div -> body -> html -> document -> window

> 不是所有的事件都能冒泡。以下事件不冒泡：blur、focus、load、unload

**阻止冒泡**

w3c的方法是event.stopPropagation()
IE则是使用event.cancelBubble = true

兼容写法：

``` javascript
if(event && event.stopPropagation){
  event.stopPropagation();  //  w3c 标准
}else{
  event.cancelBubble = true;  // ie 678  ie浏览器
}
```

**判断当前对象**

返回当前对象的 id 

- 火狐 谷歌 等   event.target.id        
- ie 678          event.srcElement.id    

兼容性写法：
``` javascript
var targetId = event.target ? event.target.id : event.srcElement.id;
```

**获得用户内容**
window.getSelection()     标准浏览器    w3c 
document.selection.createRange().text;    ie  678

**访问样式属性**

div.style[“width”]      引号必须写

**获得css样式属性值**

ie 专属  div.currentStyle.left 
w3c   window.getComputedStyle(元素,伪元素)

兼容性的写法
``` javascript
function getStyle(obj,attr) {
  if(obj.currentStyle) {
 // 如果支持，返回改属性值
 // return  obj.style.left    只能得到行内式的
 // return  obj.currentStyle["left"];   // 正确的写法，但是left 是传进来的
    return  obj.currentStyle[attr];
  } else {
    return window.getComputedStyle(obj,null)[attr];
  }
}
```

**遍历JSON**

`for(var k in json) {   }` 

- 遍历数组时，k代表的是元素的下标
- 遍历json时，k代表的是属性名

``` javascript
var arr = [1,3,5,7,9];
for(var k in arr) {
  console.log(k);    //  再数组里面 k  输出的索引号    0,1,2,3,4
  console.log(arr[k]);  // 输出值  1,3,5,7,9
5      }
6      var json = {width:500,height:500,top:100};
7      // json.width   输出 500
8      //  json 的属性很多 ，我们要一一得到  遍历json    key :value
9      for(var k in json) {
10          console.log(k);   // key      这里的k 输出的是属性
11          console.log(json[k]);  // json[k]    输出的是属性值
12      }
```



## 正则表达式（Regular Expression）

**特点**
- 灵活性、逻辑性和功能性非常的强
- 可以迅速地用极简单的方式达到字符串的复杂控制
- 对于刚接触的人来说，比较晦涩难懂

由一些**普通字符**和**元字符**组成，普通字符就是字母和数字，元字符具有特殊意义的字符

**test()方法**

正则对象方法，检测测试字符串是否符合该规则，返回true和false，参数（测试字符串）。`表达式.test("要验证的内容");`

``` javascript
// 验证  567 符不符合 \d 的规范
console.log(/\d/.test(567));
```

### 预定义类

| 正则   | 匹配              | 描述             |
| ---- | --------------- | -------------- |
| .    | [^\n\r]         | 除了换行和回车之外的任意字符 |
| \d   | [0-9]           | 数字字符           |
| \D   | [^0-9]          | 非数字字符          |
| \s   | [\t\n\x0B\f\r]  | 空白字符           |
| \S   | [^\t\n\x0B\f\r] | 非空白字符          |
| \w   | [a-zA-Z_0-9]    | 单词字符           |
| \W   | [^a-zA-Z_0-9]   | 非单词字符          |



### 简单类

`/string/.test("string")` 必须全部包含，返回ture（能多不能少）

``` javascript
console.log(/liu/.test("liuzb")) // => true
```

`/[string]/.test("string")` 只要包含其中任何字母，返回ture

``` javascript
console.log(/[liu]/.test("luzb")) // => true
```

### 负向类

括号内，前面加个元字符`^`进行**取反**，表示匹配不能为括号里面的字符

``` javascript
console.log(/[^abc]/.test('a')); // => false
console.log(/[^abc]/.test('gg')); // => true
```

**注意:**  这个符号 ^  一定是写到方括号里面


### 范围类

有时匹配的东西过多，而且类型又相同，全部输入太麻烦，我们可以在中间加了个横线

``` javascript
console.log(/[a-z]/.test('1111')); // => false
console.log(/[A-Z]/.test('aa')); // => false
```

### 组合类

用中括号匹配不同类型的单个字符。

``` javascript
console.log(/[a-zA-Z0-9]/.test('aA')); // => true
```

### 正则边界

`^` 会匹配行或者字符串的起始位置

**注：** `^`在`[]`中才表示非！这里表示开始

`$` 会匹配行或字符串的结尾位置

`^$`在一起 表示必须是这个（精确匹配）

``` javascript
// 边界可以精确说明要什么
console.log(/lily/.test("lilyname")); // => true
console.log(/^lily$/.test("lily"));  // => true
console.log(/^lily$/.test("ly"));   // => false
console.log(/^lily$/.test("lilylily"));   // => false
```

### 量词

| 符号    | 类型   | 描述                      |
| ----- | ---- | ----------------------- |
| *     | 贪婪   | 重复零次或更多 (>=0)           |
| +     | 懒惰   | 重复一次或更多次 (>=1)          |
| ?     | 占有   | 重复零次或一次 (0\|\|1)        |
| {}    |      | 重复多少次                   |
| {n}   |      | n次(x=n)                 |
| {n,}  |      | 重复n次或更多                 |
| {n,m} |      | 重复出现的次数比n多但比m少(n<=x<=m) |
| x\|y  | 或    | 匹配x或y其中任意一个             |



``` javascript
// 以ab开头，重复c
console.log(/^abc*$/.test('bc')) // => false 
console.log(/^abc*$/.test('abcccccc')) // => true
console.log(/^abc*$/.test('ab')) // => true (*可以是0重复)

console.log(/^abc+$/.test('ab')) // => false (+至少重复0次)

console.log(/^abc?$/.test('abcc')) // => false (?重复0次或1次)

console.log(/^[0-9]{6}$/.test('123456')) // => true

console.log(/^[0-9]{6,}$/.test('12345678')) // => true

console.log(/^[0-9]{6,8}$/.test('123456')) // => true
console.log(/^[0-9]{6,8}$/.test('1234567')) // => true
console.log(/^[0-9]{6,8}$/.test('1234568')) // => true
console.log(/^[0-9]{6,8}$/.test('123456789')) // => false

// 匹配练习
/^0\d{2}-\d{8}$/ => 010-12345678 
/^0\d{3}-\d{7}$/ => 0351-1234567
/^(0\d{3}-\d{7})|(0\d{2}-\d{8})$/ => 以上两个都匹配

//中文匹配
/^[\u4e00-\u9fa5]{2,4}$/

```

**replace()**

replace() 方法用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。
`需要匹配的对象.replace(正则式/字符串，替换的目标字符)`


``` javascript
var text = "hello world!"
text.replace(/wOrlD/i,"js")

```

**匹配模式**

g：表示全局模式（global），即模式将被应用于所有字符串而非发现一个而停止
i：表示不区分大小写（ease-insensitive）模式，在确定匹配想时忽略模式与字符串的大小写
`/world/g,/wOrLd/i`


## 闭包

我们可以用一个函数 去访问 另外一个函数的内部变量的方式就是闭包

**优点：**不产生全局变量，实现属性私有化。
**缺点：**闭包中的数据会常驻内存，在不用的时候要删掉否则会导致内存溢出。

``` javascript
// 简单示例
function outerFun(){
  var a=0;
  function innerFun(){
    a++;
    alert(a);
  }
  return innerFun;  //注意这里
}
  var obj=outerFun(); // 执行一次外部函数，给a变量赋值并返回内部函数的函数体
  obj();  obj();  // 执行返回的内部函数体 => 1 2
  var obj2=outerFun(); // 重新执行外部函数，给a变量赋值并返回内部函数的函数体
  obj2();  obj2();  // => 1 2
// => 1 2 1 2

// 精简写法
obj = function (a){
  return function(){
    a++;
    alert(a);
  }
}(0);

```

## 对象

对象就是带有**属性和方法**的数据类型 。

基本数据类型： string    number    boolean    null    undefined
复杂数据类型： Array    object    function

### 声明/使用对象

- `var obj = new Object();` 构造函数方式
- `var obj = {};` 字面量方式（推荐）

``` javascript
// 声明对象
var obj = {}; 
obj.name = "andy";  // 属性
obj.age = 25;
obj.showName = function() {   // 声明方法    方法一定带有 ()
    alert("andy");
}
obj.showAge = function() {
    alert("25");
}
// 使用对象
console.log(obj.name);  // 调用属性
console.log(obj.age);
obj.showName();   //  调用方法
obj.showAge();

// 封装写法
function Person(name,age){
  var obj = {}
  obj.name = name;
  obj.age = age;
  obj.showName = function() {
    alert(obj.name);
  }
  obj.showAge = function() {
    alert(obj.age);
  }
  return obj;
}

var ad = Person("andy",18);
ad.showName();
```


## 面向对象

- 功能模块化
- 是对面向过程的封装

**类**（泛指）和**对象**（特指）
类是对象的抽象，而对象是类的具体实例


### new

new运算符的作用是创建一个对象实例。这个对象可以是用户自定义的，也可以是带构造函数的一些系统自带的对象。

**new 关键字可以让 this  指向新的对象** 

> 所谓"构造函数"，其实就是一个普通函数，但是内部使用了this变量。对构造函数使用new运算符，就能生成实例，并且this变量会绑定在实例对象上。

``` javascript
function a(val,index){ // 构造函数
  this.val = val;
  this.index = index; 
  this.set = function(){ // 给每一个实例创建一个单独的方法
    //.....
  }
} // => (泛指-类)
a(); // => this 指向 window
var demo = new a(); // => this 指向 demo （特指-对象）类被实例化成对象
```

### prototype 原型

共同的 相同的 部分
主要解决：函数因为使用非常非常多，重复执行效率太低。

具体格式：`类.prototype.方法  = function() {}`,可以把那些不变的属性和方法，直接定义在prototype对象上

``` javascript
function Person (name,age){
  this.name = name;
  this.age = age;
}
// 原型声明在函数体的外面（避免重复执行，而共用同一个方法）
Person.prototype.showName = function(){
  console.log(this.name)
}
```
