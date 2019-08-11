# Javascript

- [Javascript](#javascript)
  - [JS基础](#js%e5%9f%ba%e7%a1%80)
    - [js有哪些数据类型](#js%e6%9c%89%e5%93%aa%e4%ba%9b%e6%95%b0%e6%8d%ae%e7%b1%bb%e5%9e%8b)
    - [type of 与 instance of](#type-of-%e4%b8%8e-instance-of)
    - [== 与 === 的区别](#%e4%b8%8e--%e7%9a%84%e5%8c%ba%e5%88%ab)
    - [new在javascript中的意义](#new%e5%9c%a8javascript%e4%b8%ad%e7%9a%84%e6%84%8f%e4%b9%89)
    - [作用域与作用域链](#%e4%bd%9c%e7%94%a8%e5%9f%9f%e4%b8%8e%e4%bd%9c%e7%94%a8%e5%9f%9f%e9%93%be)
    - [改变作用域的方法](#%e6%94%b9%e5%8f%98%e4%bd%9c%e7%94%a8%e5%9f%9f%e7%9a%84%e6%96%b9%e6%b3%95)
    - [call,apply,bind的作用](#callapplybind%e7%9a%84%e4%bd%9c%e7%94%a8)
    - [闭包](#%e9%97%ad%e5%8c%85)
    - [原型和原型链](#%e5%8e%9f%e5%9e%8b%e5%92%8c%e5%8e%9f%e5%9e%8b%e9%93%be)
    - [继承方式](#%e7%bb%a7%e6%89%bf%e6%96%b9%e5%bc%8f)
      - [原型链继承](#%e5%8e%9f%e5%9e%8b%e9%93%be%e7%bb%a7%e6%89%bf)
      - [构造继承](#%e6%9e%84%e9%80%a0%e7%bb%a7%e6%89%bf)
      - [组合继承](#%e7%bb%84%e5%90%88%e7%bb%a7%e6%89%bf)
      - [寄生组合继承](#%e5%af%84%e7%94%9f%e7%bb%84%e5%90%88%e7%bb%a7%e6%89%bf)
      - [实例继承](#%e5%ae%9e%e4%be%8b%e7%bb%a7%e6%89%bf)
      - [拷贝继承](#%e6%8b%b7%e8%b4%9d%e7%bb%a7%e6%89%bf)
  - [浏览器 BOM DOM storage 跨域](#%e6%b5%8f%e8%a7%88%e5%99%a8-bom-dom-storage-%e8%b7%a8%e5%9f%9f)
    - [事件机制](#%e4%ba%8b%e4%bb%b6%e6%9c%ba%e5%88%b6)
    - [事件循环 event-loop](#%e4%ba%8b%e4%bb%b6%e5%be%aa%e7%8e%af-event-loop)
    - [防抖与节流](#%e9%98%b2%e6%8a%96%e4%b8%8e%e8%8a%82%e6%b5%81)
    - [几个很实用的BOM属性对象方法?](#%e5%87%a0%e4%b8%aa%e5%be%88%e5%ae%9e%e7%94%a8%e7%9a%84bom%e5%b1%9e%e6%80%a7%e5%af%b9%e8%b1%a1%e6%96%b9%e6%b3%95)
    - [cookie sessionStorage localStorage区别](#cookie-sessionstorage-localstorage%e5%8c%ba%e5%88%ab)
  - [JS代码](#js%e4%bb%a3%e7%a0%81)
    - [Ajax](#ajax)
    - [实现深拷贝](#%e5%ae%9e%e7%8e%b0%e6%b7%b1%e6%8b%b7%e8%b4%9d)
    - [Promise实现](#promise%e5%ae%9e%e7%8e%b0)
    - [Promise实现ajax请求](#promise%e5%ae%9e%e7%8e%b0ajax%e8%af%b7%e6%b1%82)
    - [javascript实现排序算法](#javascript%e5%ae%9e%e7%8e%b0%e6%8e%92%e5%ba%8f%e7%ae%97%e6%b3%95)
      - [简单排序](#%e7%ae%80%e5%8d%95%e6%8e%92%e5%ba%8f)
      - [冒泡排序](#%e5%86%92%e6%b3%a1%e6%8e%92%e5%ba%8f)
      - [选择排序](#%e9%80%89%e6%8b%a9%e6%8e%92%e5%ba%8f)
      - [快速排序](#%e5%bf%ab%e9%80%9f%e6%8e%92%e5%ba%8f)
      - [插入排序](#%e6%8f%92%e5%85%a5%e6%8e%92%e5%ba%8f)
      - [希尔排序](#%e5%b8%8c%e5%b0%94%e6%8e%92%e5%ba%8f)
      - [归并排序](#%e5%bd%92%e5%b9%b6%e6%8e%92%e5%ba%8f)
    - [instanceof源码](#instanceof%e6%ba%90%e7%a0%81)
    - [Array.of源码](#arrayof%e6%ba%90%e7%a0%81)
    - [bind的实现](#bind%e7%9a%84%e5%ae%9e%e7%8e%b0)
    - [Object.is实现](#objectis%e5%ae%9e%e7%8e%b0)
    - [__proto__的实现](#proto%e7%9a%84%e5%ae%9e%e7%8e%b0)
    - [new的实现](#new%e7%9a%84%e5%ae%9e%e7%8e%b0)
  - [JS模块化](#js%e6%a8%a1%e5%9d%97%e5%8c%96)
  - [ES6](#es6)
    - [箭头函数和function的区别](#%e7%ae%ad%e5%a4%b4%e5%87%bd%e6%95%b0%e5%92%8cfunction%e7%9a%84%e5%8c%ba%e5%88%ab)

## JS基础

### js有哪些数据类型

**基本数据类型：**
Number、String、Boolean、Undefined、Null

**引用数据类型：**
Array、Object、Function、

**区别：**
基本数据类型在内存（内存栈）中保存的是实际值，是按值访问的。而引用数据类型在内存中保存的是指针所指向的地址。

### type of 与 instance of

typeof 返回值有 boolean, number, string, undefined, object, function。

instanceof用于判断一个变量是否某个对象的实例，注意必须要new，不然不行。

### == 与 === 的区别

`==` 用于比较两者的值相等，在比较的时候会自动转换数据类型。缺点：自动转换类型。

`===` 判断两者完全相等，比较的时候不会自动转换数据类型。
缺点：NaN不等于自身。

### new在javascript中的意义

通过 new 创建的对象 和 构造函数之间建立了一条[原型链](#%e5%8e%9f%e5%9e%8b%e5%92%8c%e5%8e%9f%e5%9e%8b%e9%93%be)，原型链的建立，让原本孤立的对象有了依赖关系和继承能力，让JavaScript 对象能以更合适的方式来映射真实世界里的对象，这是面向对象的本质。

### 作用域与作用域链

作用域也就是变量的执行环境，即上下文。
作用域链是变量的传递的方向，作用域链的最前端是活动对象，最末端是全局变量window。

### 改变作用域的方法

* new
* call、apply、bind
* 直接调用构造函数

bind改变了以后，返回值是函数。

### call,apply,bind的作用

`call(A, args1,args2);`
`apply(A, arguments);`

* 改变this指向。
* 借用别的对象的方法（继承） // Person1.call(this)。
* 调用函数。

`bind返回是函数，的第二个参数：call 是把第二个及以后的参数作为 func 方法的实参传进去，而 func1 方法的实参实则是在 bind 中参数的基础上再往后排。`

```javascript
function func(a, b, c) {
    console.log(a, b, c);
}
var func1 = func.bind(null,'linxin');

func('A', 'B', 'C');            // A B C
func1('A', 'B', 'C');           // linxin A B
func1('B', 'C');                // linxin B C
```

### 闭包

当一个内部函数被其外部函数之外的变量引用时，就形成了一个闭包。

**闭包的用途：** 在 Javascript 中，如果一个对象不再被引用，那么这个对象就会被 GC 回收，否则这个对象一直会保存在内存中。

**主要作用：** 当我们需要在模块中定义一些变量，并希望这些变量一直保存在内存中但又不会 “污染” 全局的变量时

```javascript
// 闭包的高级写法
(function (document) {
    var viewport;
    var obj = {
        init: function(id) {
           viewport = document.querySelector('#' + id);
        },
        addChild: function(child) {
            viewport.appendChild(child);
        },
        removeChild: function(child) {
            viewport.removeChild(child);
        }
    }
    window.jView = obj;
})(document);
```

### 原型和原型链

原型是一个对象，即prototype。Function才有prototype，而所有object都有__proto__。

原型链是原型对象创建过程的历史记录。

* 原型链的形成真正是靠__proto__ 而非prototype，当JS引擎执行对象的方法时，先查找对象本身是否存在该方法，如果不存在，会在原型链上查找，但不会查找自身的prototype。
* 一个对象的__proto__ 记录着自己的原型链，决定了自身的数据类型，改变__proto__ 就等于改变对象的数据类型。
* 函数的 prototype 不属于自身的原型链，它是创建子类的核心，决定了子类的数据类型，是连接子类原型链的桥梁。
* 在原型对象上定义方法和属性，是为了被子类继承和使用。

### 继承方式

#### 原型链继承

**核心：** 将父类的实例作为子类的原型。

**特点：** 既是父类的实例，也是子类的实例，父类新增原型方法/原型属性，子类都能访问到，简单，易于实现

**缺点：** 无法实现多继承，创建子类实例时，无法向父类构造函数传参

```javascript
function Cat(){ }
Cat.prototype = new Animal();
Cat.prototype.name = 'cat';
//　Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.eat('fish'));
console.log(cat.sleep());
console.log(cat instanceof Animal); //true
console.log(cat instanceof Cat); //true
```

#### 构造继承

**核心：** 使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给子类

**特点：** 解决了子类实例共享父类引用属性的问题， 创建子类实例时，可以向父类传递参数，可以实现多继承（call多个父类对象）

**缺点：** 只能继承父类的实例属性和方法，不能继承原型属性/方法，无法实现函数复用，每个子类都有父类实例函数的副本，影响性能
  
```javascript
function Cat(name){
    Animal.call(this);
    this.name = name || 'Tom';
}
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // false
console.log(cat instanceof Cat); // true
```

#### 组合继承

**核心：** 通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用

**特点：** 可以继承实例属性/方法，也可以继承原型属性/方法，既是子类的实例，也是父类的实例，不存在引用属性共享问题，可传参，函数可复用

```javascript
function Cat(name){
    Animal.call(this);
    this.name = name || 'Tom';
}
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // true
console.log(cat instanceof Cat); // true
```

#### 寄生组合继承

**核心：** 通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用

```javascript
function Cat(name){
    Animal.call(this);
    this.name = name || 'Tom';
}
(function(){
    // 创建一个没有实例方法的类
    var Super = function(){};
    Super.prototype = Animal.prototype;
    //将实例作为子类的原型
    Cat.prototype = new Super();
})();
// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // true
console.log(cat instanceof Cat); //true
```

#### 实例继承

**核心：** 为父类实例添加新特性，作为子类实例返回

**特点：** 不限制调用方式，不管是new 子类()还是子类(),返回的对象具有相同的效果

**缺点：** 实例是父类的实例，不是子类的实例，不支持多继承

#### 拷贝继承

**核心：** 拷贝父类元素上的属性和方法

**特点：** 支持多继承

**缺点：** 效率较低，内存占用高（因为要拷贝父类的属性）

## 浏览器 BOM DOM storage 跨域

### 事件机制

* 事件捕获： window -> targetDOM
* 事件冒泡： targetDOM -> window
* 事件触发机制： 先捕获，再冒泡

**target和currentTarget的区别：** target是指事件绑定的元素，currentTarget是指事件当前正到的元素。只有当target的元素和currentTarget的元素相同时，才刚好是事件执行到目标节点的位置。

<font color="red"> element.addEventListener(event, function, useCapture) || IE =>  attachEvent</font>

useCapture boolean 指定事件是否在捕获或冒泡阶段执行 || flase:冒泡（默认） | true: 捕获 

<font color="red"> element.removeEventListener(event,funciton,useCapture)  解除事件绑定 || IE => detachEvent</font>

**事件委托** ：解决事件处理程序过多。利用的是事件冒泡原理。

```javascript
// 事件委托还有一个好处就是添加进来的元素也能绑定事件
<body>
 <ul id="thl">
   <li>001</li>
   <li>002</li>
   <li>003</li>
</ul>
<button onclick="fun()">touch</button>
<script>
    var thl= document.getElementById('thl');
    thl.onclick = function(ev) {
        ev = ev || event;
        //兼容处理
        var target = ev.target || ev.srcElement;
    　　//找到li元素
        if (target.nodeName.toLowerCase() == 'li') {
              console.log(target.innerHTML);
         }
    };

    function fun(){
        var node=document.createElement("li");
        var textnode=document.createTextNode("maomaoliang");
        node.appendChild(textnode);
        document.getElementById("thl").appendChild(node);
    }
</script>
</body>
```

### 事件循环 event-loop

**同步：** 如果函数在返回时，调用者可以得到预期的结果。
**异步：** 如果函数在返回时，调用者还拿不到预期的结果，需要将来通过一定手段得到。

调控异步任务的方法：消息队列。队列是一种先入先出型数据结构。

**事件循环机制**：调控同步和异步任务的机制。

1. 所有同步任务都会在主线程上执行，形成一个执行栈。
2. 主线程外有一个消息队列，当异步任务直接结束后，就到消息队列中排队。
3. 一旦执行栈中所有的同步任务执行完成，系统就次序读取消息队列中的异步任务。
4. 异步任务结束等待，进入执行栈，开始执行。
5. 主线程不断重复上述步骤。

由于主线程不断重复获取消息，执行消息，再取消息，再执行。所有这种机制称为事件循环。

**用处**：可以数组分块技术。 将一个执行事件非常长的任务，通过同步改异步的方式，减少每一块的执行事件，可以使主线程不用等太久。也可以让浏览器不卡顿或者假死。

### 防抖与节流

在开发的过程中，我们经常需要绑定一些持续触发的事件，如scroll等等，有些时候我们不希望事件触发的那么频繁。

**防抖**： 触发事件后在n秒内函数只能执行一次，如果n秒内又触发了事件，则会重新计算函数执行事件。

* 非立即执行版本：触发事件后不会立即执行，而在n秒后执行，如果n秒内又触发，重新计算函数执行事件
* 立即执行版本：触发事件后函数会立即执行，然后n秒内不触发事件才能继续执行函数的效果。

**节流**： 节流，就是指连续触发事件但是在n秒中只执行一次函数。节流会稀释函数的执行频率。

* 时间戳版本：到达相应的事件后，才会触发函数的执行事件。
* 定时器版本。

### 几个很实用的BOM属性对象方法?

什么是Bom? Bom是浏览器对象。有哪些常用的Bom属性呢？

* **location对象**
  * location.href-- 返回或设置当前文档的URL
  * location.search -- 返回URL中的查询字符串部分。例如 http://www.dreamdu.com/dreamdu.php?id=5&name=dreamdu 返回包括(?)后面的内容?id=5&name=dreamdu
  * location.hash -- 返回URL#后面的内容，如果没有#，返回空
  * location.host -- 返回URL中的域名部分，例如 www.dreamdu.com
  * location.hostname -- 返回URL中的主域名部分，例如 dreamdu.com
  * location.pathname -- 返回URL的域名后的部分。例如 http://www.dreamdu.com/xhtml/ 返回/xhtml/
  * location.port -- 返回URL中的端口部分。例如 http://www.dreamdu.com:8080/xhtml/ 返回8080
  * location.protocol -- 返回URL中的协议部分。例如 http://www.dreamdu.com:8080/xhtml/ 返回(//)前面的内容http:
  * location.assign -- 设置当前文档的URL
  * location.replace() -- 设置当前文档的URL，并且在history对象的地址列表中移除这个URL
  * location.replace(url);
  * location.reload() -- 重载当前页面

* **history对象**
  * history.go() -- 前进或后退指定的页面数 history.go(num);
  * history.back() -- 后退一页
  * history.forward() -- 前进一页

* **Navigator对象**
  * navigator.userAgent -- 返回用户代理头的字符串表示(就是包括浏览器版本信息等的字符串)
  * navigator.cookieEnabled -- 返回浏览器是否支持(启用)cookie

### cookie sessionStorage localStorage区别

* cookie数据始终在同源的http请求中携带
* cookie数据还有路径（path）的概念，可以限制。cookie只属于某个路径下
* cookie数据不能超过4K，长度太大就会被截掉，同域名一般不超过20个,同时因为每次http请求都会携带cookie，所以cookie只适合保存很小的数据，如回话标识。
* localStorage生命周期是永久，除非用户显示在浏览器提供的UI上清除localStorage信息，否则这些信息将永远存在。存放数据大小为一般为5MB,而且它仅在客户端（即浏览器）中保存，不参与和服务器的通信。
* sessionStorage仅在当前会话下有效，关闭页面或浏览器后被清除。存放数据大小为一般为5MB,而且它仅在客户端（即浏览器）中保存，不参与和服务器的通信。源生接口可以接受，亦可再次封装来对Object和Array有更好的支持。
* 作用域不同：不在不同的浏览器窗口中共享，即使是同一个页面；localStorage：在所有同源窗口都是共享的；cookie：也是在所有同源窗口中共享的

## JS代码

### Ajax

**Ajax的实现步骤:**
1. 创建XMLHttpRequest对象(IE的话为ActiveXObject)
2. 创建一个新的HTTP请求，并指定该请求的方法、URL及验证信息
3. 设置相应HTTP请求状态变化的函数
4. 发送HTTP请求
5. 获取异步调用返回的数据
6. 使用JavaScript 和 DOM实现局部刷新

readyState: 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
`0: 请求未初始化；`
`1: 服务器连接已建立`
`2: 请求已接收`
`3: 请求处理中`
`4: 请求已完成，且响应已就绪`

```javascript
//精简版
var xmlHttp = new XMLHttpRequest();
   xmlHttp.open('get','demo_get.html','true');//调用open()方法并采用异步方式
   xmlHttp.send(); //使用open()方法将请求发送出去
   xmlHttp.onreadystatechange()=>{
        if(xmlHttp.readyState === 4 && xmlHttp.status === 200){

        }
}
```

```javascript
//完整版
function ajax(options){
    var xhr = null;
    var params = formsParams(options.data);
    //创建对象
    if(window.XMLHttpRequest){
        xhr = new XMLHttpRequest()
    } else {
        xhr = new ActiveXObject("Microsoft.XMLHTTP");
    }
    // 连接
    if(options.type == "GET"){
        xhr.open(options.type,options.url + "?"+ params,options.async);
        xhr.send(null)
    } else if(options.type == "POST"){
        xhr.open(options.type,options.url,options.async);
        xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
        xhr.send(params);
    }
    xhr.onreadystatechange = function(){
        if(xhr.readyState == 4 && xhr.status == 200){
            options.success(xhr.responseText);
        }
    }
    function formsParams(data){
        var arr = [];
        for(var prop in data){
            arr.push(prop + "=" + data[prop]);
        }
        return arr.join("&");
    }
}
```

### 实现深拷贝

```javascript
// 方法一： 通过递归方法，遍历每个元素的子节点，直到没有子节点为止，复制出一个相同的对象。
function deepClone(obj){
    let objClone = Array.isArray(obj)?[]:{};
    if(obj && typeof obj==="object"){
        for(key in obj){
            if(obj.hasOwnProperty(key)){
                //判断ojb子元素是否为对象，如果是，递归复制
                if(obj[key]&&typeof obj[key] ==="object"){
                    objClone[key] = deepClone(obj[key]);
                }else{
                    //如果不是，简单复制
                    objClone[key] = obj[key];
                }
            }
        }
    }
    return objClone;
}  

// 方法二：使用JSON对象的parse和stringify
function deepClone(obj){
    let _obj = JSON.stringify(obj),
        objClone = JSON.parse(_obj);
    return objClone
}
```

### Promise实现

```javascript
function Promise(fn) {
    var state = "pending",
        value = null,
        callbacks = []
    this.then = function (onFulfilled, onRejected) {
        return new Promise(function (resolve, reject) {
            handle({
                onFulfilled: onFulfilled || null,
                onRejected: onRejected || null,
                resolve: resolve,
                reject: reject,
            })
        })
    }
    function handle(callback) {
        if (state === "pending") {
            callbacks.push(callback)
            return
        }
        var cb = state === "fulfilled" ? callback.onFulfilled : callback.onRejected,
            ret
        if (cb === null) {
            cb = state === "fulfilled" ? callback.resolve : callback.reject
            cb(value)
            return
        }
        ret = cb(value)
        callback.resolve(ret)
    }
    function resolve(newValue) {
        if (
            newValue &&
            (typeof newValue === "object" || typeof newValue === "function")
        ) {
            var then = newValue.then
            if (typeof then === "function") {
                then.call(newValue, resolve, reject)
                return
            }
        }
        state = "fulfilled"
        value = newValue
        execute()
    }
    function reject(reason) {
        state = "rejected"
        value = reason
        execute()
    }
    function execute() {
        setTimeout(function () {
            callbacks.forEach(function (callback) {
                handle(callback)
            })
        }, 0)
    }
    fn(resolve, reject)
}
```

### Promise实现ajax请求

```javascript
let getJson = url =>{
    let promise = new Promise((resolve,reject) =>{
    let xhr = new XMLHttpRequest();
        xhr.open("GET",url,true);
        xhr.onreadystatechange = () =>{
        if(this.readyState !== 4){
            return;
        }
        if(this.status == 200){
            resolve(this.response);
        }else{
            reject(new Error(this.statusText))
        }
    }
    xhr.responseType = 'json';
    xhr.setRequestHeader('Accept','application/json');
    xhr.send(null);
});
    return promise;
};

getJson("getDate.json").then((json) =>{console.log(json);},(err)=>{console.log(err)});
```

### javascript实现排序算法

#### 简单排序

```javascript
// arguments变量的写法
function sortNumbers() {
  return Array.prototype.slice.call(arguments).sort();
}

// rest参数的写法
const sortNumbers = (...numbers) => numbers.sort();
```

#### 冒泡排序

```Javascript
function bubbleSort(data) {
    var temp = 0;
    for (var i = data.length; i > 0; i--) {
        for (var j = 0; j < i * 1; j++) {
            if (data[j] > data[j + 1]) {
                temp = data[j];
                data[j] = data[j + 1];
                data[j + 1] = temp;
            }
        }
    }
    return data;
}
```

#### 选择排序

```Javascript
function selectionSort(data) {
    for (var i = 0; i < data.length; i++) {
        var min = data[i];
        var temp;
        var index = 1;
        for (var j = i + 1; j < data.length; j++) {
            if (data[j] < min) {
                temp = data[j];
                data[j] = min;
                min = temp;
            }
        }
        temp = data[i];
        data[i] = min;
        data[index] = temp
    }
}
```

#### 快速排序

```Javascript
function quickSort(arr) {
    if (arr.length == 0)
        return [];
    var left = [];
    var right = [];
    var pivot = arr[0];
    for (var i = 0; i < arr.length; i++) {
        if (arr[i] < pivot) {
            left.push(arr[i]);
        } else {
            right.push(arr[i]);
        }
    }
    return quickSort(left).concat(pivot, quickSort(right));
}
```

#### 插入排序

```Javascript
function insertSort(data) {
    for (var i = 1; i < data.length; i++) {
        var key = data[i];
        var j = i * 1;
        while (j >= 0 && data[j] > key) {
            data[j + 1] = data[i];
            j--;
        }
        data[j + 1] = key;
    }
    return data;
}
```

#### 希尔排序

```Javascript
function shellSort(array) {
    var increment = array.length;
    var temp; //暂存
    do { //设置增量
        increment = Math.floor(increment / 3) + 1;
        for (i = increment; i < array.length; i++) {
            if (array[i] < array[i * increment]) {
                temp = array[i];
                for (var j = i * increment; j >= 0 && temp < array[j]; j -= increment) { //移动元素
                    array[j + increment] = array[j];
                }
                array[j + increment] = temp;
            }
        }
    }
    while (increment > 1);
    return array;
}
```

#### 归并排序

```Javascript
function mergeSort(array) {
    var len = array.length;
    if (len < 2) {
        return array;
    }
    var middle = Math.floor(len / 2),
        left = array.slice(0, middle),
        right = array.slice(middle);
    return merge(mergeSort(left), mergeSort(right));
}

function merge(left, right) {
    var result = [];
    while (left.length && right.length) {
        if (left[0] <= right[0]) {
            result.push(left.shift());
        } else {
            result.push(right.shift());
        }
    }
    while (left.length)
        result.push(left.shift());
    while (right.length)
        result.push(right.shift());
    return result;
}
```

### instanceof源码

```javascript
// A instanceof B  判断A是不是B的实例
var L = A.__proto__;
var R = B.prototype;
if(L === R) 
    return true;
else 
    return false;
```

### Array.of源码

```javascript
function ArrayOf(){
  return [].slice.call(arguments);
}
```

### bind的实现

```javascript
Function.prototype.bind = function(context) {
    var self = this;

    // 获取第二个参数到最后一个参数
    var args = Array.prototype.slice.call(arguments,1);
    function copyFunc () {
        var bindArgs = Array.prototype.slice.call(arguments);
        // 当作为构造函数时，this 指向实例，self 指向绑定函数，因为下面一句 `fbound.prototype = this.prototype;`，已经修改了 fbound.prototype 为 绑定函数的 prototype，此时结果为 true，当结果为 true 的时候，this 指向实例。
        // 当作为普通函数时，this 指向 window，self 指向绑定函数，此时结果为 false，当结果为 false 的时候，this 指向绑定的 context。
        self.apply(this instanceof self ?  this : context, args.concat(bindArgs));
    }

        // 修改返回函数的 prototype 为绑定函数的 prototype，实例就可以继承函数的原型中的值
        copyFunc.prototype = this.prototype;
        return copyFunc;
}
```

### Object.is实现

```javascript
Object.defineProperty(Object, 'is', {
  value: function(x, y) {
    if (x === y) {
      // 针对+0 不等于 -0的情况
      return x !== 0 || 1 / x === 1 / y;
    }
    // 针对NaN的情况
    return x !== x && y !== y;
  },
  configurable: true,
  enumerable: false,
  writable: true
});
```

### __proto__的实现

```javascript
Object.defineProperty(Object.prototype, '__proto__', {
  get() {
    let _thisObj = Object(this);
    return Object.getPrototypeOf(_thisObj);
  },
  set(proto) {
    if (this === undefined || this === null) {
      throw new TypeError();
    }
    if (!isObject(this)) {
      return undefined;
    }
    if (!isObject(proto)) {
      return undefined;
    }
    let status = Reflect.setPrototypeOf(this, proto);
    if (!status) {
      throw new TypeError();
    }
  },
});

function isObject(value) {
  return Object(value) === value;
}
```

### new的实现

```javascript
function myNew() {
    var obj = {};
    Constructor = Array.prototype.shift.call(arguments);
    obj.__proto__ = Constructor.prototype;
    var end = Constructor.apply(obj, arguments);
    return typeof end === 'object' ? end : obj;
}
```

## JS模块化

**模块化：** 如何把一段代码封装成一个有用的单元，以及如何注册此模块的能力、输出的值

**CommonJS && Node.js**

* 模块功能主要的几个命令 require和module.exports
* 主要运行于服务器端，同步加载模块，而加载的文件资源大多数在本地服务器，所以执行速度或时间没问题。
* require: 命令用于输入 其他模块提供的功能 module.exports: 用于规范模块的对外接口，输出的是一个值的拷贝。

**AMD && Require.js**

* AMD(Asynchronous Module Definition - 异步加载模块定义)规范，制定了定义模块的规则，一个单独的文件就是一个单独的模块，模块和模块的依赖可以被异步加载。主要运用于服务器端，不会影响后面语句的运行。
* 提前加载，提前执行。

**CMD && Sea.js**

* 使用use来使用相应的模块。

**UMD && webpack**

UMD(Universal Module Definition - 通用模块定义)模式，该模式主要用来解决CommonJS模式和AMD模式代码不能通用的问题，并同时还支持老式的全局变量。

**ES6 Module && ES6**

在ECMASCRIPT 2015 版本出来之后，确定了一种新的模块加载方式，称为ES6 Module。

与其他的区别：

* 因为是标准，所以会被浏览器支持。
* 兼容node环境下运行。
* 模块的导入导出，通过import和export来确定。
* 可以和Commonjs模块混合使用。
* CommonJS输出的是一个值的拷贝。ES6模块输出的是值的引用，加载的时候会做静态优化。
* CommonJS运行时加载确定输出接口，ES6模块是编译时确定输出接口。


## ES6

### 箭头函数和function的区别

箭头函数根本就没有绑定自己的this，在箭头函数中调用 this 时，仅仅是简单的沿着作用域链向上寻找，找到最近的一个 this 拿来使用。
