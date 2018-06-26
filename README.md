# 前端面试题整理
前端常见面试题，定期维护更新

## http、网络部分及html综合题

- http有几种请求方式？
> OPTIONS：返回服务器针对特定资源所支持的HTTP请求方法。也可以利用向Web服务器发送'*'的请求来测试服务器的功能性。
>
> HEAD：向服务器索要与GET请求相一致的响应，只不过响应体将不会被返回。这一方法可以在不必传输整个响应内容的情况下，就可以获取包含在响应消息头中的元信息。
>
> GET：向特定的资源发出请求。
>
> POST：向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。
>
> PUT：向指定资源位置上传其最新内容。
>
> DELETE：请求服务器删除Request-URI所标识的资源。
>
> TRACE：回显服务器收到的请求，主要用于测试或诊断。 
>
> CONNECT：HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。
- 从浏览器地址栏输入url到显示页面的步骤
> 1、应用层DNS解析域名
>
> 2、应用层客户端发送HTTP请求
>
> 3、传输层TCP传输报文
>
> 4、网络层IP协议查询MAC地址
>
> 5、数据到达数据链路层
>
> 6、服务器接收数据
>
> 7、服务器响应请求
>
> 8、服务器返回相应文件
>
> 9、客户端进行渲染
- 如何进行网站优化
> 缓存、图片、样式、脚本、请求数
>
- HTTP状态码
> 20X;30X;40X;50X
>
- html5有哪些新特性
> 新增标签、新增哪些标签的属性
>
- cookies，sessionStorage 和 localStorage 的区别
>


## css篇

- 解释下盒模型
- 怎么理解BFC
- 清除浮动的方式(overflow:hidden的原理)
> 在父元素里设置某个子元素浮动。浮动后，子元素脱离了文档流，使得父元素无法包住这个浮动的子元素
> <span color='red'>BFC可以包含浮动</span>这一特性来清除浮动,而overflow:hidden可以触发一个BFC
- css3有哪些新特性
- 垂直居中的几种实现方式
- transition 动画 animation 的参数和区别
- flex是否支持IE9,有哪些属性值

## js篇

- 什么是闭包，闭包的使用场景
> 有权访问另一个函数作用域内变量的函数都是闭包

> 闭包就是一个函数引用另外一个函数的变量，因为变量被引用着所以不会被回收，因此可以用来封装一个私有变量。这是优点也是缺点，不必要的闭包只会徒增内存消耗
- JavaScript原型，原型链 ? 有什么特点
> 每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时
如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时所说的原型链的概念
关系：instance.constructor.prototype = instance.__proto__

> JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变当我们需要一个属性的时，Javascript引擎会先看当前对象中是否有这个属性， 如果没有的就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象
- 什么是事件代理
> 事件代理（Event Delegation），又称之为事件委托。是 JavaScript 中常用绑定事件的常用技巧。顾名思义，“事件代理”即是把原本需要绑定的事件委托给父元素，让父元素担当事件监听的职务。事件代理的原理是DOM元素的事件冒泡。使用事件代理的好处是可以提高性能
可以大量节省内存占用，减少事件注册，比如在table上代理所有td的click事件就非常棒
可以实现当新增子对象时无需再次对其绑定
- Javascript如何实现继承
> 原型链继承(将父类的实例作为子类的原型)
```
function Cat(){ 
}
Cat.prototype = new Animal();
Cat.prototype.name = 'cat';
//　Test Code
var cat = new Cat();
```
> 构造继承(使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给子类（没用到原型）)
```
function Cat(name){
  Animal.call(this);
  this.name = name || 'Tom';
}
// Test Code
var cat = new Cat();
```
> 组合继承(通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用)
```
function Cat(name){
  Animal.call(this);
  this.name = name || 'Tom';
}
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;
// Test Code
var cat = new Cat();
```
> 寄生组合继承(通过寄生方式，砍掉父类的实例属性，这样，在调用两次父类的构造的时候，就不会初始化两次实例方法/属性，避免的组合继承的缺点)
```
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
```
- 谈谈this的理解
> this是在运行时绑定，而不是在编写时绑定，this实际值取决于函数调用时的上下文。this的绑定和函数声明的位置没有关系，只取决于函数的调用方式。在JavaScript中，当函数被调用时，会创建一个活动记录（执行时上下文），这个记录包含函数在何处调用、函数的调用方法和传入参数等信息，this会记录其中一个属性。判断this实际绑定值，关键在于分析函数实际调用的位置
> new绑定

> 隐式绑定(当对象内部包含一个指向函数的属性，并且在调用时通过这个属性间接引用函数（obj.prop()的形式），那么函数内的this会隐式指向这个对象，也即隐式绑定)
```
function foo() {
    console.log(this.a);
}

var obj = {
    a: 2,
    foo: foo
};

obj.foo();  //  2
```
> 显示绑定(在某些情况下，我们希望函数内的this绑定在某些指定的对象上，这称为显示绑定。在JavaScript中可以使用call和apply为函数显示指定this绑定。call和apply的第一个参数是一个对象，这个对象会被绑定到this上)
```
function foo() {
    console.log(this.a);
}

var obj = {
　　a:2
};

foo.call(obj);  //  2
```
> 默认绑定(使用默认绑定规则，this被绑定到全局对象上。在strict模式下，this会绑定到undefined)
- Ajax原理
> 简单来说通过XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来操作DOM而更新页面
- 什么是同源策略，如何解决跨域问题
- 谈谈你对webpack的看法
> WebPack 是一个模块打包工具，你可以使用WebPack管理你的模块依赖，并编绎输出模块们所需的静态文件。
> 它能够很好地管理、打包Web开发中所用到的HTML、Javascript、CSS以及各种静态文件（图片、字体等），让开发过程更加高效。
> 对于不同类型的资源，webpack有对应的模块加载器。webpack模块打包器会分析模块间的依赖关系，最后 生成了优化且合并后的静态资源
>
- CMD和AMD的区别
- 前端常用的设计模式
- Promise的原理，怎么简单的实现一个promise
> Promise 概括来说是对异步的执行结果的描述对象,是js异步的解决方案，通常用于ajax请求
> promise 的3种状态pending、fullfilled、rejected
> 1、Promise 构造器中必须传入函数，否则会抛出错误。(没有执行器还怎么做异步操作。。。)
>
> 2、Promise.prototype上的 catch(onrejected) 方法是 then(null,onrejected) 的别名,并且会处理链之前的任何的reject
>
> 3、Promise.prototype 上的 then和 catch 方法总会返回一个全新的 Promise 对象
>
> 4、如果传入构造器的函数中抛出了错误,该 promise 对象的[[PromiseStatus]]会赋值为 rejected，并且[[PromiseValue]]赋值为 Error 对象
>
> 5、then 中的回调如果抛出错误，返回的 promise 对象的[[PromiseStatus]]会赋值为 rejected，并且[[PromiseValue]]赋值为 Error 对象
>
> 6、then 中的回调返回值会影响 then 返回的 promise 对象
>
```
function Promise(executor) {
    // 容器，存放then订阅的东西
    this._deferreds = []
    var _this = this
    // 承诺被执行
    function resolve(stuff) {
        // 取出存的东西
        _this._deferreds.forEach(function (deferred) {
            // 执行
            deferred(stuff)
        })
    }
    // Promise传入的函数，执行时将resolve传进去
    executor(resolve)
}

Promise.prototype.then = function (onFulfilled) {
    // 往里面放东西
    this._deferreds.push(onFulfilled)
}
```

- 同步和异步的区别
- es6的新特效
- var、let、const区别
- 箭头函数和普通函数的区别
- 怎么实现一个深拷贝
- jQuery为什么可以一直.下去
> 因为每次都是返回一个实例
- 数组的常用方法
- 0.1+0.2等于什么，为什么会出现这种现象
- addEventListener有几个参数
- 双精度小数在内存中占多少位
- 求一个节点的索引（react中怎么做）
- 如何合并两个对象
- 是否了解Web注入攻击，说下原理，最常见的两种攻击（XSS 和CSRF）
- promise.all和promise.race的理解
> Promise.all可以将多个Promise实例包装成一个新的Promise实例。同时，成功和失败的返回值是不同的，成功的时候返回的是一个结果数组，而失败的时候则返回最先被reject失败状态的值

> Promse.race就是赛跑的意思，意思就是说，Promise.race([p1, p2, p3])里面哪个结果获得的快，就返回那个结果，不管结果本身是成功状态还是失败状态。

> Promise.race()的作用：
用于和定时器绑定，可以测试一些接口的响应速度，分析用户的网络状况之类的，，比如将一个请求，和三秒后执行定时器 包装成promise 实例，然后加入 promise.race队列中， 当请求三秒还未响应时候，可以给用户一些提示， 或者是一些其他操作。

## 框架篇

- react的生命周期
- react组件之间的传值
- props和state的区别
- redux的原理
- router的原理
- 如何做ssr
- webpack的优化措施
- webpack中loader和plugin的区别
- 如何实现一个观察订阅模式
- react的高阶函数和高阶组件
> 高阶函数的定义：接收函数作为输入，或者输出另一个函数的一类函数，被称作高阶函数。对于高阶组件，它描述的便是接受React组件作为输入，输出一个新的React组件的组件。

> 更通俗地描述为，高阶组件通过包裹（wrapped）被传入的React组件，经过一系列处理，最终返回一个相对增强（enhanced）的React组件，供其他组件调用。

## 笔试篇

- 数组去重降序排序
- 判断一个对象是否为数组
- 冒泡排序、快速排序
- 写一个正则表达式，长度6-8位，必须数字字母混合并且首字母大写
- 写一个通用的事件侦听器函数
- 数组降维
```
function deepFlatten(arr){
    return arr.reduce((r,v) => {
       return r.concat(Array.isArray(v) ? deepFlatten(v) : v)
    },[] )
}
```
- 深拷贝
```
function deepClone(obj){
  let clone = Object.assign({}, obj);
  Object.keys(clone).forEach(
    key => (clone[key] = typeof obj[key] === 'object' ? deepClone(obj[key]) : obj[key])
  );
  return Array.isArray(obj) ? (clone.length = obj.length) && Array.from(clone) : clone;
};
```

## 开放篇

- 对前端工程师这个职位是怎么样理解的？它的前景会怎么样
- 什么是前端工程化
- 未来三到五年的规划是怎样的
- 平时是如何学习前端的
- 项目中遇到的问题并怎么解决的




