# JavaScript

---

***后端打工人必须要精通JavaScript***

ECMAScript可理解为JS的一个标准

## 2 快速入门

### 2.1 引入

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <!-- 标签必须成对出现 -->
    <!-- 外部引入 -->
    <script src="js/qj.js"></script>
    
    <!-- 内联合 -->
    <script>
        alert('hello');
    </script>


</head>
<body>

<!-- 或者脚本放在这里也行 -->
</body>
</html>
```

### 2.2 基本语法

```html
<script>
        // 定义变量： 变量类型（var） 名 = val;
        var num = 1;
        var name = "asdasd";

        // condition
        if (num > 1) {
            alert('>1 !');
        } else {
            alert('<=1!');
        }
        
    </script>
```

### 2.3 严格检查模式

```html
<script>
    'use strict'
    let i = 1;
</script>
```

## 3 数据类型

```javascript
// 变量全部用var开头
// 变量名开头不能用数字

// JS不区分小数整数，都是number类型
123
123.1
1.23e3
NaN // 不是一个数
Infinity // 为无穷大

// 字符串
'abc'
"abc"

// Boolean
true;
false;

// Logic arithmetic
和java差不多

// equals
== 等于（少用，类型不一样，值一样，也会判断为true）
=== 绝对等于（常用，类型和值全都一样才会true）

// null & undefined
// Array: 可以类型不一样
var arr = [1,2,3,4,'hello',null,true];

// Object(对象大括号，数组fun括号)
var person = {
  	name: "ma yun",
  	age: 3,
  	tags: ['js','java','web']
};

person.name="ma yun";
```

*浮点数问题*

```javascript
console.log((1/3) === (1 - 2/3)); // 结果为false
// 避免浮点数运算,如果必须要比较
(a - b) < 0.00001;
```

*严格检查模式*

防止javascript语法随意性导致的问题，建议启用。必须写在第一行。

```javascript
'use strict'
let i = 1;
```

### 3.1 字符串

1. 正常字符串用单引号或者双引号包裹

2. 转义字符 \
3. 多行字符串编写：`长字符串`

```javascript
// 反引号
var msg = `acdc
hello
my
friend`;
```

4. 模板字符串

```javascript
let name = "root";
let age = 3;
// 反引号
let msg = `Hello, ${name}`;
```

5. 字符串操作

```javascript
str.length;
str[0];
str.toUpperCase();
str.indexOf('c');
str.substring(0,1);
```

---

### 3.2 数组

数组元素可为任意数据类型

1. 操作

```javascript
arr,length
arr.indexof(element) // 获得元素下标索引
arr.slice(0,1) // 截取数组，类似于substring
arr.push(element, ...) // 加尾
arr.pop() // 去尾
arr.unshift(element, ...) // 加头
arr.shift() // 去头
arr,sort()
arr.reverse()
arr.concat([1,2,3]) // 尾加，返回新数组，原数组不动
arr.join('-') // 数组拼接

```

---

### 3.3 对象

```javascript
var person = {
  	name: "acdc",
  	age: 3,
  	score: 0
}
```

*删除/增加属性*

```javascript
delete person.name
person.newAttr
```

*判断属性值是否在对象中*

```javascript
xxx in xxx
```

---

### 3.4 流程控制

很像Java，除了foreach

```javascript
var age = [12,3,1,32,24];
age.forEach(function(value) {
  console.log(value);
});
```

```javascript
// 遍历下标
for(var index in age) {
      console.log(age[index]);
}
```

### 3.5 Map 和 Set

```javascript
var map = new Map([['tom', 100], ['wbd', 233]]);
console.log(map.get('tom'));
map.set('sb', 666);
map.delete('sb', 666);
```

Set: 无序不重复的集合

```javascript
var set = new Set([3,1,1,1]);
// 输出后结果是 3 1
```

###  3.6 Iterator

```javascript
var map = [['tom', 233], ['dick', 332]];
for (var x of map) {
  	console.log(x);
}

```

---

## 4 函数

### 4.1 函数声明

```javascript
function abs(x) {
            if (typeof x !== 'number') {
                throw 'Not a Number';
            }
            if(x>=0) {
                return x;
            } else {
                return -x;
            }
        }

        let reverseNum = function (x) {
            return -x;
        };


        function absMulti(x) {
            for (let i = 0; i < arguments.length; i++) {
                if (typeof arguments[i] !== 'number') {
                    console.log('Not a Number');
                    continue;
                }

                if(arguments[i]>=0) {
                    console.log(arguments[i]);
                } else {
                    console.log(-arguments[i]);
                }
            }
        }

        // ES6 feature
        function mutiParam(a,b, ...rest) {
            console.log('a: ' + a);
            console.log('b: ' + b);
            console.log(rest);
        }
```

### 4.2 变量作用域

两个函数，只要在内部，相同的变量名不会冲突.

嵌套，由内向外查找变量，如内部变量和外部重名，内部覆盖外部的。

js引擎能够自动提升变量声明，但是不能提升赋值操作。

ES6 新增了`let`命令，用来声明局部变量。它的用法类似于`var`，但是所声明的变量，只在`let`命令所在的代码块内有效，而且有暂时性死区的约束。

先看个`var`的常见变量提升的面试题目：

```javascript
var a = 99;            // 全局变量a
f();                   // f是函数，虽然定义在调用的后面，但是函数声明会提升到作用域的顶部。 
console.log(a);        // a=>99,  此时是全局变量的a
function f() {
  console.log(a);      // 当前的a变量是下面变量a声明提升后，默认值undefined
  var a = 10;
  console.log(a);      // a => 10
}

// 输出结果：
undefined
10
99
```

ES6新增的`let`，可以声明块级作用域的变量。

```javascript
{ 
  var i = 9;
} 
console.log(i);  // 9
{ 
  let j = 9;     // i变量只在 花括号内有效！！！
} 
console.log(j);  // Uncaught ReferenceError: j is not defined
```

用`let`声明的变量，不存在变量提升。而且要求必须 等`let`声明语句执行完之后，变量才能使用，不然会报`Uncaught ReferenceError`错误。
例如：

```javascript
console.log(aicoder);    // 错误：Uncaught ReferenceError ...
let aicoder = 'aicoder.com';
// log方法这里就才可以安全使用aicoder
```

let变量不能重复声明

```javascript
let a = 0;
let a = 'sss';
// Uncaught SyntaxError: Identifier 'a' has already been declared
```

### 4.3 方法

```javascript
var person = {
  name: 'Gordon Freeman',
  birth: 1984,
  age: function () {
    let now = new Date().getFullYear();
    return now - this.birth;
  }
};

// 获得方法
person.age();
```

如果方法和对象拆开写，使用 *apply*关键字重定向

```javascript
function getAge() {
  var now = new Date().getFullYear();
  return. now - this.birth;
}

var person = {
  name: 'Gordon Freeman',
  birth: 1984,
  age: getAge
};

getAge.apply(person, []) // this指向person，无参数
```

## 5 内部对象

### 5.1 Date

```javascript
var now = new Date();
now.getFullYear(); //年
now.getMonth(); // 月
now.getDate(); // 日
now.getDay(); // 星期几
now.getHours();
now.getMinutes();
now.getSecounds();
now.getTime(); // 时间戳，全世界统一，从1970.1.1 0:00:00开始的毫秒数。
now.toLocaleString();
now.toGMTString();
```

### 5.2 JSON

```javascript
var user = {
   name: 'qinjiang',
   age: 3,
   sex: 'male'
}

var jsonUser = JSON.stringify(user);
var obj = JSON.parse('{"name":"qinjiang", "age":3,"sex":"male"}');


var obj = {a:'hello', b:'hellob'}; // JS object
var json = '{"a":"hello","b":"hellob"}'; // JSON
```



### 5.3 Ajax

- 原生js写法，xhr同步请求
- jQuery封装好的方法

---

## 6 面向对象编程

原型对象。

### 6.1 面向对象

- 原型:

  ```apl
  var Student = {
    name: 'qinjiang',
    age: 3,
    run: function() {
      	console.log(this.name + " run...");
    }
  };
  
  var xiaoming = {
    	name: 'xiaoming'
  };
  
  // 小明的原型是student
  xiaoming.__proto__ = Student;
  
  var Bird = {
    fly: function() {
      	console.log(this.name + "fly。。。")；
    }
  }
  
  // 把小明变成鸟
  xiaoming.__proto__ = Bird;
  ```

- Class关键字定义类， 继承

  ```javascript
  function Student(name) {
    	this.name = name;
  }
  
  // 给原型新增方法
  Student.prototype.hello = function () {
    	alert('hello');
  }
  
  // ES6 之后
  // 直接使用class关键词定义学生类
  class Student {
  		constructor(name) {
        	this.name = name;
      }
    
    	hello() {
        	alert('hello');
      }
  }
  
  var xiaoming = new Student('xiaoming');
  
  // 继承
  
  class XiaoStudent extends Student{
    	constructor(name. grade) {
        	super(name)
        	this.grade = grade;
      }
    
    	myGrade() {
        	alert('我是一个小学生');
      }
  }
  var xiaohong = new XiaoStudent('xiaohong');
  ```

- 原型链

  ![image-20210301220546378](/Users/shaotienlee/Desktop/Study/Notes/JavaScript.assets/image-20210301220546378.png)

## 7 BOM对象

BOM: 浏览器对象模型。

> window(重要，浏览器窗口)

```javascript
window.alert(1);
window.innerweight; // 显示高度
window.innerwidth;
```

> Navigator

```javascript
window.outerHeight;
1097
navigator.appVersion;
"5.0 (Macintosh)"
navigator.userAgent;
"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:86.0) Gecko/20100101 Firefox/86.0"
navigator.platform;
"MacIntel"
```

> Screen（屏幕尺寸）

```javascript
screen.width
1792 // px
screen.height
1120
```

> Location(重要，当前页面URL信息)

```javascript
location.
host: "www.baidu.com"
hostname: "www.baidu.com"
href: "https://www.baidu.com/"
protocol: "https:"
reload() // refresh the page
assign('https://cn.bin.com/') // redirect

```

> document(重要,当前页面HTML DOM文档树)

```javascript
document.
title;
getElementByID('id');
cookie
// 服务器端可以设置cookie: httpOnly加强cookie安全
```

> history

```javascript
history.back()
history.forward()
```

---

## 8 DOM 对象及其操作

文档对象模型。浏览器网页就是一个DOM树结构

- 更新DOM节点
- 遍历DOM节点
- 删除节点
- 添加节点

操作前先要获得节点

```javascript
var h1 = document.getElementsByTagName('h1');
document.getElementById('');
document.getElementsByClassName('');

var father = document.getElementById('father');
var children = father.children // 获取某个父节点的所有子节点
father.firstChild
father.lastChild

```

*这是原生代码，以后一般都用JQuery*

### 8.1 更新DOM节点

```javascript
var p = document.getElementById('id1');

p.innerText = '123'; // 修改文本的值

p.innerHTML = '<strong>123</strong>'; // 可以解析文本的HTML标签

// 设置样式
p.innerText = 'abc';
p.style.color = 'red';
p.style.fontSize = '20px';
p.style.padding = '2em';
```

### 8.2 删除DOM节点

```javascript
// 先获取目标父节点，再通过父节点删除目标
// 借刀杀人
eg: <div id="father">
  			<h1>title1</h1>
  			<p id="p1">p1</p>
		</div>
 
var father = document.getElementId('father');
// var father = p1.parentElement;
father.removeChild(p1)
// father.removeChild(father.children[0])
```

### 8.3 创建和插入节点

先获得某个DOM节点，假设该DOM节点是空的，可以通过innerText添加一个元素；但是如果这个DOM节点已经有元素了，就是追加。

```html
<body>
<div id="father">
    <h1>title1</h1>
    <p id="p1">p1</p>
</div>

<hr>

<p id="js">JavaScript</p>
<div id="list">
    <p id="se">JavaSE</p>
    <p id="ee">JavaEE</p>
    <p id="me">JavaME</p>
</div>

<script>
    let father = document.getElementById('father');
    father.removeChild(p1) // 删除东西

    let js = document.getElementById('js');
    let list = document.getElementById('list');

    list.appendChild(js); // 把那个js东西移过来追加到后面

    // 通过JS创建新节点 p标签
    var newNode = document.createElement('p');

    // 也可以写 newNode.setAttribute('id', 'newNode');
    newNode.id = 'newNode';
    newNode.innerText = 'Hello, KuGou';
    // 把这个新节点追加在list后面
    list.append(newNode);

    // Advanced
  	// 创建Script节点并保存在头里
    let myScript = document.createElement('script');
    myScript.setAttribute('type', 'text/javascript');
    myScript.innerText = "alert('233');"

    // 找头也可以用document.getElementByTagName('head')[0]
    // byTagName返回的是数组，你就用浏览器打印下返回的都是啥就知道了
    document.head.appendChild(myScript);

    // 创建css，并且插入HTML
    let myStyle = document.createElement('style');
    myStyle.setAttribute('type', 'text/css');
    myStyle.innerHTML = 'body {' +
        'background-color: chartreuse' +
        '}';
    document.getElementsByTagName('head')[0].appendChild(myStyle);


</script>
</body>
```



*向前插入*

```html
<p id="js">JavaScript</p>
<div id="list">
    <p id="se">JavaSE</p>
    <p id="ee">JavaEE</p>
    <p id="me">JavaME</p>
</div>

<script>
   let ee = document.getElementById('ee');
   let ks = document.getElementById('js');
   let list = document.getElementById('list');
   list.insertBefore(js, ee); // js查到ee前一格
</script>
```

---

## 9 操作表单

### 9.1 表单操作

**可以用来做前端验证**

> form

- text文本
- 下拉select
- 单选radio
- 多选checkbox
-  密码password
- 隐藏域hidden

```html
<form action="post" >
    <p>
        <span>用户名</span> <input type="text" id="username">
    </p>
    <p>
        <span>性别</span>
        <input type="radio" name="gender" value="male"> male
        <input type="radio" name="gender" value="female"> female
    </p>

</form>


<script>
    // 得到输入框的值
    var username = document.getElementById('username');
    console.log(username.value);

    // 修改输入框的值
    username.value = 'bbbbb';
    console.log(username.value);

    // 重要：对于单选/多选等等固定值的获取
    let man_radio = document.getElementsByName('gender')[0];
    let woman_radio = document.getElementsByName('gender')[1];

    // 检验是否被选
    man_radio.checked;
    // 也可以给别人赋值
    man_radio.checked = true;
</script>

```

### 9.2 表单提交及其验证

```html
<!-- form可以绑定事件onsubmit(),如果函数返回值为假，会阻止提交操作 -->
<form action="#" method="post" onsubmit="return checkpassword()">
    <p>
        <span>用户名</span> <input type="text" id="username" name="username">
    </p>
    <p>
        <span>密码</span> <input type="password" id="password" name="password">
    </p>

    <!-- button可以绑定事件onclick() -->
    <button type="submit">交</button>

</form>

<script>
    function checkpassword() {
        let username = document.getElementById('username');
        let password = document.getElementById('password');

        console.log(username.value);
        console.log(password.value);

        // 需要引入MD5工具类对password进行加密
        password.value = md5(password.value);
        console.log(password.value);

        // 在这里可以放检验表单的东西。true就能正常提交。
        return true;
    }

</script>
```

---

## 10 jQuery

### 10.1 jQuery与JavaScript的关系

jQuery是个库，存在大量的JavaScript函数.[封装]

### 10.2 获取jQuery

算了，还是用cdn吧

国内

```html
<script src="http://apps.bdimg.com/libs/jquery/1.9.1/jquery.min.js"></script>
```

### 10.3 jQuery选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="http://apps.bdimg.com/libs/jquery/1.9.1/jquery.min.js"></script>
</head>
<body>

<!-- 记住一个公式

    $('selector').action()

 -->
<a href="#" id="test-jquery">Hit me</a>

<script>
    document.getElementById('test-jquery');
    // 等价于
    $('#test-jquery').click(function () {
        alert('hello, world!');
    });
</script>
</body>
</html>
```

### 10.4 jQuery 事件

```html
<body>

mouse：<span id="mouseMove"></span>
<div id="divMove">
    在这里移动鼠标
</div>


<script>
    // 当网页加载完后，响应事件
    $(document).ready(function () {
        $('#divMove').mousemove(function (e) {
            $('#mouseMove').text('x: ' + e.pageX + ' y: ' + e.pageY);
        });
    });
</script>

</body>
```

### 10.5 jQuery DOM操作

```html
<body>
<ul id="test-ul">
    <li class="js">javaScript</li>
    <li name="python">python</li>
</ul>

<script>
    // 获得值
    console.log($('#test-ul li[name=python]').text());

    // 设置值
    $('#test-ul li[name=python]').text('I love it');

    console.log($('#test-ul').html());
    $('#test-ul').html('<h1>okkk</h1>' +
        '<h2>noooo</h2>');

    // css操作
    $('#test-ul').css('color', 'green');

    // 隐藏: display: none
    $('h2').css('display', 'none');
    // 等价于 $('h2').hide();
    $('h2').show();
    // 隐藏用的开关
    $('h2').toggle();
    $('h2').toggle();
  
   // ajax

</script>
</body>
```

