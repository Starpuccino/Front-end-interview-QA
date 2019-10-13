# Javascript

[TOC]

## **JS基础**

### js有哪些数据类型

**基本数据类型：**
Number、String、Boolean、Undefined、Null、Symbol(ES6)

**引用数据类型：**
Array、Object、Function

**区别：**
基本数据类型在内存（内存栈）中保存的是实际值，是按值访问的。而引用数据类型在内存中保存的是指针所指向的地址。

### typeof 与 instanceof的区别

- **typeof**  返回值有 `boolean`  `number`  `string`  `undefined`  `object`  ` function`。
- **instanceof** 用于判断一个变量是否某个对象的实例，⚠️必须要new，不然不行。

### == 与 === 的区别

- **==** 用于比较两者的值相等，在比较的时候会自动转换数据类型。缺点：自动转换类型。
- **===** 判断两者完全相等，比较的时候不会自动转换数据类型。
  ⚠️NaN不等于自身。

### null与undefined的区别

- **null** 是js中的关键字，表示空值，null可以看作是object的一个特殊的值，如果一个object值为空，表示这个对象不是有效对象。
- **undefined** 不是js中的关键字，其是一个全局变量，是Global的一个属性，以下情况会返回undefined:

  1. 使用了一个未定义的变量
  2. 使用了已定义但未声明的变量
  3. 使用了一个对象属性，但该属性不存在或者未赋值
  4. 调用函数时，该提供的参数没有提供
  5. 函数没有返回值时，默认返回undefined

- 输出比较

  ```javascript
  typeOf undefined;     //undefined
  typeOf null;          //object

  Number(undefined);    //NaN
  Number(10+undefined); //NaN
  Number(null);         //0
  Number(10+null);      //10

  undefined===null;     //false
  undefined==null;      //true

  var arr=["aa","bb","cc"];
  arr=null; 						//null当用完一个比较大的对象，进行释放内存时，设置为null
  ```

### new在javascript中的意义

通过 new 创建的对象 和 构造函数之间建立了一条[原型链](#原型和原型链)，原型链的建立，让原本孤立的对象有了依赖关系和继承能力，让JavaScript 对象能以更合适的方式来映射真实世界里的对象，这是面向对象的本质。

### call,apply,bind的作用

`call(A, args1,args2);`
`apply(A, arguments);`

- 改变this指向。
- 借用别的对象的方法（继承） // Person1.call(this)。
- 调用函数。

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

### 作用域与作用域链

作用域也就是变量的执行环境，即上下文。
作用域链是变量的传递的方向，作用域链的最前端是活动对象，最末端是全局变量window。

### 改变作用域的方法

- new
- call、apply、bind
- 直接调用构造函数

bind改变了以后，返回值是函数。

### 闭包

[详解 https://www.jianshu.com/p/26c81fde22fb](https://www.jianshu.com/p/26c81fde22fb)

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

详解 [https://github.com/mqyqingfeng/Blog/issues/2](https://github.com/mqyqingfeng/Blog/issues/2)

超详解 [https://www.jianshu.com/p/dee9f8b14771](https://www.jianshu.com/p/dee9f8b14771)

![整体的联系](./img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NjMTg4Njg4NzY4Mzc=,size_16,color_FFFFFF,t_70.png)

原型是一个对象，即prototype。Function才有prototype，而所有object都有** proto **。

原型链是原型对象创建过程的历史记录。

- 原型链的形成真正是靠** proto ** 而非prototype，当JS引擎执行对象的方法时，先查找对象本身是否存在该方法，如果不存在，会在原型链上查找，但不会查找自身的prototype。
- 一个对象的 ** proto ** 记录着自己的原型链，决定了自身的数据类型，改变 ** proto ** 就等于改变对象的数据类型。
- 函数的 prototype 不属于自身的原型链，它是创建子类的核心，决定了子类的数据类型，是连接子类原型链的桥梁。
- 在原型对象上定义方法和属性，是为了被子类继承和使用。

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

## **浏览器 BOM DOM storage**

### 事件机制

- 事件捕获： window -> targetDOM
- 事件冒泡： targetDOM -> window
- 事件触发机制： 先捕获，再冒泡

**target和currentTarget的区别：** target是指事件绑定的元素，currentTarget是指事件当前正到的元素。只有当target的元素和currentTarget的元素相同时，才刚好是事件执行到目标节点的位置。

`element.addEventListener(event, function, useCapture) || IE =>  attachEvent`
`useCapture` boolean 指定事件是否在捕获或冒泡阶段执行 || false:冒泡（默认） | true: 捕获
`element.removeEventListener(event,funciton,useCapture)`  解除事件绑定 || IE => detachEvent

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

### 事件循环机制 event-loop

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

- 非立即执行版本：触发事件后不会立即执行，而在n秒后执行，如果n秒内又触发，重新计算函数执行事件
- 立即执行版本：触发事件后函数会立即执行，然后n秒内不触发事件才能继续执行函数的效果。

**节流**： 节流，就是指连续触发事件但是在n秒中只执行一次函数。节流会稀释函数的执行频率。

- 时间戳版本：到达相应的事件后，才会触发函数的执行事件。
- 定时器版本。

### 几个很实用的BOM属性对象方法?

什么是Bom? Bom是浏览器对象。有哪些常用的Bom属性呢？

- **location对象**

  - location.href-- 返回或设置当前文档的URL
  - location.search -- 返回URL中的查询字符串部分。例如 <http://www.dreamdu.com/dreamdu.php?id=5&name=dreamdu> 返回包括(?)后面的内容?id=5&name=dreamdu
  - location.hash -- 返回URL#后面的内容，如果没有#，返回空
  - location.host -- 返回URL中的域名部分，例如 www.dreamdu.com
  - location.hostname -- 返回URL中的主域名部分，例如 dreamdu.com
  - location.pathname -- 返回URL的域名后的部分。例如 <http://www.dreamdu.com/xhtml/> 返回/xhtml/
  - location.port -- 返回URL中的端口部分。例如 <http://www.dreamdu.com:8080/xhtml/> 返回8080
  - location.protocol -- 返回URL中的协议部分。例如 <http://www.dreamdu.com:8080/xhtml/> 返回(//)前面的内容http\:
  - location.assign -- 设置当前文档的URL
  - location.replace() -- 设置当前文档的URL，并且在history对象的地址列表中移除这个URL
  - location.replace(url);
  - location.reload() -- 重载当前页面

- **history对象**

  - history.go() -- 前进或后退指定的页面数 history.go(num);
  - history.back() -- 后退一页
  - history.forward() -- 前进一页

- **Navigator对象**
  - navigator.userAgent -- 返回用户代理头的字符串表示(就是包括浏览器版本信息等的字符串)
  - navigator.cookieEnabled -- 返回浏览器是否支持(启用)cookie

### cookie sessionStorage localStorage区别

- cookie数据始终在同源的http请求中携带
- cookie数据还有路径（path）的概念，可以限制。cookie只属于某个路径下
- cookie数据不能超过4K，长度太大就会被截掉，同域名一般不超过20个,同时因为每次http请求都会携带cookie，所以cookie只适合保存很小的数据，如回话标识。
- localStorage生命周期是永久，除非用户显示在浏览器提供的UI上清除localStorage信息，否则这些信息将永远存在。存放数据大小为一般为5MB,而且它仅在客户端（即浏览器）中保存，不参与和服务器的通信。
- sessionStorage仅在当前会话下有效，关闭页面或浏览器后被清除。存放数据大小为一般为5MB,而且它仅在客户端（即浏览器）中保存，不参与和服务器的通信。源生接口可以接受，亦可再次封装来对Object和Array有更好的支持。
- 作用域不同：不在不同的浏览器窗口中共享，即使是同一个页面；localStorage：在所有同源窗口都是共享的；cookie：也是在所有同源窗口中共享的。

### clientHeight,scrollHeight,offsetHeight ,以及scrollTop, offsetTop,clientTop的区别

- clientHeight：表示的是可视区域的高度，不包含border和滚动条。
- offsetHeight：表示可视区域的高度，包含了border和滚动条。
- scrollHeight：表示了所有区域的高度，包含了因为滚动被隐藏的部分。 
- clientTop：表示边框border的厚度，在未指定的情况下一般为0 。
- scrollTop：滚动后被隐藏的高度，获取对象相对于由offsetParent属性指定的父坐标(css定位的元素或body元素)距离顶端的高度。

## **同源和跨域**

### 浏览器的同源策略

所谓同源是指：协议，域名，端口号相同。

**同源策略又可分为两类：**

1. DOM同源策略：禁止对不同源的DOM进行操作，（iframe）
2. XMLHttpRequest同源策略：禁止使用XHR对象向不同源的服务器地址发起HTTP请求。

**如果没有同源策略会怎么样？**

如果没有XHR同源，黑客可以通过CSRF(跨站请求伪造)攻击获取用户信息。获取页面中的cookie并直接跨域请求。

### XHR请求跨域

#### JSONP

由于`script`标签不受浏览器的同源策略影响，允许跨域引用资源。因此可以动态创建script标签，然后利用src进行跨域。

```javascript
// 1. 定义一个 回调函数 handleResponse 用来接收返回的数据
function handleResponse(data) {
    console.log(data);
};

// 2. 动态创建一个 script 标签，并且告诉后端回调函数名叫 handleResponse
var body = document.getElementsByTagName('body')[0];
var script = document.getElement('script');
script.src = 'http://www.laixiangran.cn/json?callback=handleResponse';
body.appendChild(script);

// 3. 通过 script.src 请求 `http://www.laixiangran.cn/json?callback=handleResponse`，
// 4. 后端能够识别这样的 URL 格式并处理该请求，然后返回 handleResponse({"name": "laixiangran"}) 给浏览器
// 5. 浏览器在接收到 handleResponse({"name": "laixiangran"}) 之后立即执行 ，也就是执行 handleResponse 方法，获得后端返回的数据，这样就完成一次跨域请求了。
```

**优点**

- 使用简便，没有兼容性问题，目前最流行的一种跨域方法。

**缺点**

- 只支持GET请求
- 安全性问题，看其他域是否安全
- 要确定JSONP请求是否失败很难

#### CORS跨域资源共享（Cross-origin resource sharing）

详解 [http://www.ruanyifeng.com/blog/2016/04/cors.html](http://www.ruanyifeng.com/blog/2016/04/cors.html)

**优点**

- CORS是一个W3C标准，CORS支持所有类型的HTTP请求。
- 它允许浏览器向跨源服务器，发出XMLHttpRequest请求，从而克服了AJAX只能同源使用的限制。
- 整个CORS通信过程，都是浏览器自动完成，不需要用户参与。对于开发者来说，CORS通信与同源的AJAX通信没有差别，代码完全一样。
- 浏览器一旦发现AJAX请求跨源，就会自动添加一些附加的头信息，有时还会多出一次附加的请求，但用户不会有感觉。
- 因此，实现CORS通信的关键是服务器。只要服务器实现了CORS接口，就可以跨源通信。

**缺点**

- CORS需要浏览器和服务器同时支持。目前，所有浏览器都支持该功能，IE浏览器不能低于IE10。
- 第一次发送非简单请求时会多一次请求。

**分类**

- **简单请求（simple request）**

  1. 请求方法是`HEAD` `GET` `POST`三者之一
  2. HTTP的头信息不超出以下几种字段：`Accept` `Accept-Language` `Content-Language` `Last-Event-ID` 
  3. Content-Type 仅限于`application/x-www-form-urlencoded`  `multipart/form-data` `text/plain`

- **非简单请求（not-so-simple request）**

  不满足简单请求的就是非简单请求。比如请求方法是`PUT`或`DELETE`，或者`Content-Type`字段的类型是`application/json`。

**过程**

**简单请求（simple request）**

- 浏览器发现这次跨源AJAX请求是简单请求，就自动在头信息之中，添加一个`Origin`字段，`Origin`字段用来说明，本次请求来自哪个源（协议 + 域名 + 端口）。

- 服务器根据这个值，决定是否同意这次请求，如果`Origin`指定的源，不在许可范围内，服务器会返回一个正常的HTTP回应。浏览器发现，这个回应的头信息没有包含`Access-Control-Allow-Origin`字段（详见下文），就知道出错了，从而抛出一个错误，被`XMLHttpRequest`的`onerror`回调函数捕获。

  ⚠️这种错误无法通过状态码识别，因为HTTP回应的状态码有可能是200。

- 如果`Origin`指定的域名在许可范围内，服务器返回的响应，会多出几个头信息字段。

- ```http
Access-Control-Allow-Origin: http://api.bob.com
   Access-Control-Allow-Credentials: true
   Access-Control-Expose-Headers: FooBar
   Content-Type: text/html; charset=utf-8
  ```
  
   1. `Access-Control-Allow-Origin` 字段必须。它的值要么是请求时`Origin`字段的值，要么是`*`，表示接受任意域名的请求。
   2. `Access-Control-Allow-Credentials` 字段可选，是一个布尔值，表示是否允许发送Cookie。默认情况下，Cookie不包括在CORS请求之中。设为true，即表示服务器许可，Cookie可以包含在请求中。这个值也只能设为true，如果服务器不要浏览器发送Cookie，删除该字段即可。
   3. `Access-Control-Expose-Headers` 字段可选。CORS请求时，XMLHttpRequest对象的getResponseHeader()方法只能拿到6个基本字段：`Cache-Control`、`Content-Language`、`Content-Type`、`Expires`、`Last-Modified`、`Pragma`。如果想拿到其他字段，就必须在`Access-Control-Expose-Headers`里面指定。上面的例子指定，`getResponseHeader('FooBar')`可以返回`FooBar`字段的值。

- 如果要把Cookie发到服务器，不仅要服务器同意，开发者必须在AJAX请求中打开`withCredentials`属性

  ```javascript
  var xhr = new XMLHttpRequest();
  xhr.withCredentials = true;
  //如果省略withCredentials，有的浏览器还是会一起发送Cookie。可以显式设置withCredentials = false
  ```

  ⚠️如果要发送Cookie，`Access-Control-Allow-Origin`就不能设为`*`，必须指定明确的、与请求网页一致的域名。

**非简单请求（not-so-simple request）**

- 非简单请求的CORS请求，会在正式通信之前，增加一次HTTP查询请求，称为"预检"请求（preflight）。

- 浏览器先询问服务器，当前网页所在的域名是否在服务器的许可名单之中，以及可以使用哪些HTTP动词和头信息字段。只有得到肯定答复，浏览器才会发出正式的`XMLHttpRequest`请求，否则就报错。

- "预检"请求用的请求方法是`OPTIONS`，表示这个请求是用来询问的。

  1. `Origin`，表示请求来自哪个源。
  2. `Access-Control-Request-Method` 是必须的，用来列出浏览器的CORS请求会用到哪些HTTP方法。
  3. `Access-Control-Request-Headers` 是一个逗号分隔的字符串，指定浏览器CORS请求会额外发送的头信息字段。

- 预检请求的回应

- ```http
  HTTP/1.1 200 OK
  Date: Mon, 01 Dec 2008 01:15:39 GMT
  Server: Apache/2.0.61 (Unix)
  Access-Control-Allow-Origin: http://api.bob.com
  Access-Control-Allow-Methods: GET, POST, PUT
  Access-Control-Allow-Headers: X-Custom-Header
  Content-Type: text/html; charset=utf-8
  Content-Encoding: gzip
  Content-Length: 0
  Content-Type: text/plain
  ```

  1. `Access-Control-Allow-Origin` 字段必须，表示 `http://api.bob.com` 可以请求数据。该字段也可以设为`*`，表示同意任意跨源请求。

  2. `Access-Control-Allow-Methods` 字段必需，表明服务器支持的**所有跨域请求的方法**。

     ⚠️返回的是**所有支持的方法**，而不单是浏览器请求的那个方法。这是为了避免多次"预检"请求。

  3. `Access-Control-Allow-Headers` 如果浏览器请求包括`Access-Control-Request-Headers`字段，则`Access-Control-Allow-Headers`字段是必需的。表明服务器支持的**所有头信息字段**，不限于浏览器在"预检"中请求的字段。

  4. `Access-Control-Allow-Credentials` 字段与简单请求时的含义相同。

  5. `Access-Control-Max-Age` 可选，指定本次预检请求的有效期，单位为"秒"。上面结果中，有效期是20天（1728000秒），即允许缓存该条回应1728000秒（即20天），在此期间，不用发出另一条预检请求。

- 如果浏览器否定了"预检"请求，会返回一个正常的HTTP回应，但是没有任何CORS相关的头信息字段。浏览器就会认定，服务器不同意预检请求，因此触发一个错误，被`XMLHttpRequest`对象的`onerror`回调函数捕获。

#### iframe + form实现post跨域

```javascript
const requestPost = ({url, data}) => {
  // 首先创建一个用来发送数据的iframe.
  const iframe = document.createElement('iframe')
  iframe.name = 'iframePost'
  iframe.style.display = 'none'
  document.body.appendChild(iframe)
  const form = document.createElement('form')
  const node = document.createElement('input')
  // 注册iframe的load事件处理程序,如果你需要在响应返回时执行一些操作的话.
  iframe.addEventListener('load', function () {
    console.log('post success')
  })

  form.action = url
  // 在指定的iframe中执行form
  form.target = iframe.name
  form.method = 'post'
  for (let name in data) {
    node.name = name
    node.value = data[name].toString()
    form.appendChild(node.cloneNode())
  }
  // 表单元素需要添加到主文档中.
  form.style.display = 'none'
  document.body.appendChild(form)
  form.submit()

  // 表单提交后,就可以删除这个表单,不影响下次的数据发送.
  document.body.removeChild(form)
}
// 使用方式
requestPost({
  url: 'http://localhost:9871/api/iframePost',
  data: {
    msg: 'helloIframePost'
  }
})
```

#### Nginx代理

```
server{
    # 监听9099端口
    listen 9099;
    # 域名是localhost
    server_name localhost;
    #凡是localhost:9099/api这个样子的，都转发到真正的服务端地址http://localhost:9871 
    location ^~ /api {
        proxy_pass http://localhost:9871;
    }    
}
```

#### Websocket

#### Nodejs中间件代理

### 窗口间跨域

#### postMessage跨域

postMessage是HTML5 XMLHttpRequest Level 2中的API，且是为数不多可以跨域操作的window属性之一，它可用于解决以下方面的问题：

- 页面和其打开的新窗口的数据传递
- 多窗口之间消息传递
- 页面与嵌套的iframe消息传递

```javascript
postMessage(data,origin);
// data: html5规范支持任意基本类型或可复制的对象，但部分浏览器只支持字符串，所以传参时最好用JSON.stringify()序列化。
// origin: 协议+主机+端口号，也可以设置为"*"，表示可以传递给任意窗口，如果要指定和当前窗口同源的话设置为"/"。
```

#### window.name

window 对象有个 name 属性，该属性有个特征：即在一个窗口（window）的生命周期内，窗口载入的所有的页面（不管是相同域的页面还是不同域的页面）都是共享一个 window.name 的，每个页面对 window.name 都有读写的权限，window.name是持久存在一个窗口载入过的所有页面中的，并不会因新页面的载入而进行重置。

#### location.hash + iframe（同主域）

子框架具有修改父框架 src 的 hash 值，通过这个属性进行传递数据，且更改 hash 值，页面不会刷新。但是传递的数据的字节数是有限的。

#### document.domain（同主域）

对于主域名相同，而子域名不同的情况，可以使用 document.domain 来跨域。这种方式非常适用于 iframe 跨域的情况。

比如主域名是[http://crossdomain.com](http://crossdomain.com/):9099，子域名是[http://child.crossdomain.com](http://child.crossdomain.com/):9099，这种情况下给两个页面指定一下document.domain即document.domain = crossdomain.com就可以访问各自的window对象了。

## **异步加载**

### JS异步加载的三种方式

#### HTML5新属性：async和defer

**defer**

- IE4.0就出现。defer属声明脚本中将不会有document.write和dom修改。浏览器会并行下载其他有defer属性的script。而不会阻塞页面后续处理。
- 注：所有的defer脚本必须保证**按顺序执行**的。

> <script type="text/javascript" defer></script>

**async**

- Html5新属性。脚本将在下载后尽快执行，作用同defer，但是**不能保证脚本按顺序执行**。
- 他们将在onload事件之前完成。

> <script type="text/javascript" defer></script>

#### 方法一：Script DOM Element

这种加载方式执行完之前会阻止onload事件的触发。

```javascript
// 动态插入<script>标签
(function(){
  var scriptEle = document.createElement("script");
  scriptEle.type = "text/javasctipt";
  scriptEle.async = true;	// async属性是HTML5中新增的异步支持
  scriptEle.src = "http://cdn.bootcss.com/jquery/3.0.0-beta1/jquery.min.js";
  var x = document.getElementsByTagName("head")[0];
  x.insertBefore(scriptEle, x.firstChild);
 })();
```

#### 方法二：onload时的异步加载

把插入script的方法放在一个函数里面，然后放在window的onload方法里面执行，这样就解决了阻塞onload事件触发的问题。

```javascript
(function(){
 if(window.attachEvent){
   window.attachEvent("load", asyncLoad);
  }else{
   window.addEventListener("load", asyncLoad);
  }
  var asyncLoad = function(){
   var ga = document.createElement('script');
    ga.type = 'text/javascript';
    ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(ga, s);
  }
)();
```

#### 方法三：其他方法

由于JavaScript的动态性，还有很多异步加载方法： XHR Injection、 XHR Eval、 Script In Iframe、 Script defer属性、 document.write(script tag)。

**XHR Injection(XHR 注入)：**通过XMLHttpRequest来获取JavaScript，然后创建一个script元素插入到DOM结构中。ajax请求成功后设置script.text为请求成功后返回的responseText。

```javascript
//获取XMLHttpRequest对象，考虑兼容性。
  var getXmlHttp = function(){
    var obj;
    if (window.XMLHttpRequest)
      obj = new XMLHttpRequest();
    else
      obj = new ActiveXObject("Microsoft.XMLHTTP");
    return obj;
  };
  //采用Http请求get方式;open()方法的第三个参数表示采用异步(true)还是同步(false)处理
  var xmlHttp = getXmlHttp();
  xmlHttp.open("GET", "http://cdn.bootcss.com/jquery/3.0.0-beta1/jquery.min.js", true);
  xmlHttp.send();
  xmlHttp.onreadystatechange = function(){
    if (xmlHttp.readyState == 4 && xmlHttp.status == 200){
      var script = document.createElement("script");
      script.text = xmlHttp.responseText;
      document.getElementsByTagName("head")[0].appendChild(script);
    }
  }
```

**XHR Eval：**与XHR Injection对responseText的执行方式不同，直接把responseText放在eval()函数里面执行。

```javascript
 //获取XMLHttpRequest对象，考虑兼容性。
  var getXmlHttp = function(){
    var obj;
    if (window.XMLHttpRequest)
      obj = new XMLHttpRequest();
    else
      obj = new ActiveXObject("Microsoft.XMLHTTP");
    return obj;
  };
  //采用Http请求get方式;open()方法的第三个参数表示采用异步(true)还是同步(false)处理
  var xmlHttp = getXmlHttp();
  xmlHttp.open("GET", "http://cdn.bootcss.com/jquery/3.0.0-beta1/jquery.min.js", true);
  xmlHttp.send();
  xmlHttp.onreadystatechange = function(){
    if (xmlHttp.readyState == 4 && xmlHttp.status == 200){
      eval(xmlHttp.responseText);
      //alert($);//可以弹出$,表明JS已经加载进来。click事件放在其它出会出问题，应该是还没加载进来
      $("#btn1").click(function(){
        alert($(this).text());
      });
    }
  }
```

**Script In Irame：**在父窗口插入一个iframe元素，然后再iframe中执行加载JS的操作。

```javascript
 var insertJS = function(){alert(2)};
 var iframe = document.createElement("iframe");
 document.body.appendChild(iframe);
 var doc = iframe.contentWindow.document;//获取iframe中的window要用contentWindow属性。
 doc.open();
 doc.write("<script>var insertJS = function(){};<\/script><body οnlοad='insertJS()'></body>");
 doc.close();
```

**GMail Mobile：**业内JS内容被注释，所以不会执行，在需要的时候，获取script中的text内容去掉注释，调用eval()执行。

```javascript
<script type="text/javascript">
/*
var ...
*/
</script>
```

## **JS源码**

### Ajax

**Ajax的实现步骤:**

1. 创建XMLHttpRequest对象(IE的话为ActiveXObject)
2. 创建一个新的HTTP请求，并指定该请求的方法、URL及验证信息
3. 设置相应HTTP请求状态变化的函数
4. 发送HTTP请求
5. 获取异步调用返回的数据
6. 使用JavaScript 和 DOM实现局部刷新

**readyState:** 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
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

### Arguments

`arguments`对象是所有（非箭头）函数中都可用的**局部变量**。你可以使用`arguments`对象在函数中引用函数的参数。此对象包含传递给函数的每个参数，第一个参数在索引0处。例如，如果一个函数传递了三个参数，你可以以如下方式引用他们：

```js
arguments[0]
arguments[1]
arguments[2]
```

参数也可以被设置：

```js
arguments[1] = 'new value';
```

`arguments`对象不是一个 [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array) 。它类似于`Array`，但除了length属性和索引元素之外没有任何`Array`属性。例如，它没有 [pop](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop) 方法。但是它可以被转换为一个真正的`Array`：

```js
var args = Array.prototype.slice.call(arguments);
var args = [].slice.call(arguments);

// ES2015
const args = Array.from(arguments);
const args = [...arguments];
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

### 实现深拷贝

```javascript
// 方法一：使用JSON对象的parse和stringify，当值为undefined、function、symbol会在转换过程中被忽略
function deepClone(obj){
    let _obj = JSON.stringify(obj),
        objClone = JSON.parse(_obj);
    return objClone
}

// 方法二： 通过递归方法，遍历每个元素的子节点，直到没有子节点为止，复制出一个相同的对象。
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
```

### Promise实现

[Promise的实现 - 简书](https://www.jianshu.com/p/327e38aec874)

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

### Promise实现循环

```javascript
let delayPrint = (i) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log(i);
            resolve('ok:'+i)
        }, 1000)
    })
}

let forbody = Promise.resolve('begin');
for (let i = 1; i <= 5; i++) {
    forbody = forbody.then(res=>{
        return delayPrint(i);
    })
}
```

### Promise.all实现

- 接收一个 Promise 数组，返回一个 Promise,用p缓存

在传给 Promise.all 的所有 Promise 都兑现后,p也会随之兑现并按照传入顺序返回各 Promise 兑现的结果数组，但只要有一个 Promise 被拒绝,那么 p 就会立即以该 Promise 的拒绝理由确定为被拒绝。

同时异步请求多个数据的时候，即并行，就会使用用all

```javascript
static all(proArr) {
  return new Promise((resolve, reject) => {
    let ret = []
    let count = 0
    let done = (i, data) => {
      ret[i] = data
      if(++count === proArr.length) resolve(ret)
    }
    for (let i = 0; i < proArr.length; i++) {
      proArr[i].then(data => done(i,data) , reject)
    }
  })
}
```

### Promise.race实现

得益于promise的状态只能改变一次，即resolve和reject都只被能执行一次，我们把返回的promie里的resolve和reject方法放在了promiseAry每一个promise的成功或者失败回调里面，当其中任意一个成功或失败后就会调用我们传进去的resolve和reject，一旦调用了，就不会再次调用。


```javascript
static race(promiseAry) {
  return new Promise((resolve, reject) => {
    for (let i = 0; i < promiseAry.length; i++) {
      promiseAry[i].then(resolve, reject)
    }
  })
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

### Javascript实现数组排序算法

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

### 判断是否为Array

```javascript
var arr = [1,2,3,1];
arr instanceof Array;  			// true 多个frame凉凉
arr.constructor === Array;  // true 多个frame凉凉

function isArrayFn (obj) {
	return Object.prototype.toString.call(obj) === '[object Array]';
}

Array.isArray();						// ECMAScript5
```

### 实现一个add方法，使计算结果能够满足如下预期：

函数柯里化(Currying)

> add(1)(2)(3) = 6;
> add(1, 2, 3)(4) = 10;
> add(1)(2)(3)(4)(5) = 15;

```javascript
function add() {
    // 第一次执行时，定义一个数组专门用来存储所有的参数
    var _args = Array.prototype.slice.call(arguments);

    // 在内部声明一个函数，利用闭包的特性保存_args并收集所有的参数值
    var _adder = function() {
        _args.push(...arguments);
        return _adder;
    };

    // 利用toString隐式转换的特性，当最后执行时隐式转换，并计算最终的值返回
    _adder.toString = function () {
        return _args.reduce(function (a, b) {
            return a + b;
        });
    }
    return _adder;
}

add(1)(2)(3)                // 6
add(1, 2, 3)(4)             // 10
add(1)(2)(3)(4)(5)          // 15
add(2, 6)(1)                // 9
```

### Array.of源码

```javascript
Array.of = function() {
    return Array.prototype.slice.call(arguments);
};
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

### __ proto __ 的实现

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

## **JS模块化**

**模块化：** 如何把一段代码封装成一个有用的单元，以及如何注册此模块的能力、输出的值

**CommonJS && Node.js**

- 模块功能主要的几个命令 require和module.exports
- 主要运行于服务器端，同步加载模块，而加载的文件资源大多数在本地服务器，所以执行速度或时间没问题。
- require: 命令用于输入 其他模块提供的功能 module.exports: 用于规范模块的对外接口，输出的是一个值的拷贝。

**AMD && Require.js**

- AMD(Asynchronous Module Definition - 异步加载模块定义)规范，制定了定义模块的规则，一个单独的文件就是一个单独的模块，模块和模块的依赖可以被异步加载。主要运用于服务器端，不会影响后面语句的运行。
- 提前加载，提前执行。

**CMD && Sea.js**

- 使用use来使用相应的模块。

**UMD && webpack**

UMD(Universal Module Definition - 通用模块定义)模式，该模式主要用来解决CommonJS模式和AMD模式代码不能通用的问题，并同时还支持老式的全局变量。

**ES6 Module && ES6**

在ECMASCRIPT 2015 版本出来之后，确定了一种新的模块加载方式，称为ES6 Module。

与其他的区别：

- 因为是标准，所以会被浏览器支持。
- 兼容node环境下运行。
- 模块的导入导出，通过import和export来确定。
- 可以和Commonjs模块混合使用。
- CommonJS输出的是一个值的拷贝。ES6模块输出的是值的引用，加载的时候会做静态优化。
- CommonJS运行时加载确定输出接口，ES6模块是编译时确定输出接口。

## **ES6**

> 详细文档见 [http://es6.ruanyifeng.com](http://es6.ruanyifeng.com)

### 箭头函数和function的区别

箭头函数根本就没有绑定自己的this，在箭头函数中调用 this 时，仅仅是简单的沿着作用域链向上寻找，找到最近的一个 this 拿来使用。

### let和var的区别

let所声明的变量，只在`let`命令所在的代码块内有效，而且有暂时性死区的约束。

let不存在变量提升

