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
- css3有哪些新特性
- 垂直居中的几种实现方式
- transition 动画 animation 的参数和区别
- flex是否支持IE9,有哪些属性值

## js篇

- 什么是闭包，闭包的使用场景
- JavaScript原型，原型链 ? 有什么特点
- 什么是事件代理
- Javascript如何实现继承
- 谈谈this的理解
- Ajax原理
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

## 笔试篇

- 数组去重降序排序
- 判断一个对象是否为数组
- 冒泡排序、快速排序
- 写一个正则表达式，长度6-8位，必须数字字母混合并且首字母大写
- 写一个通用的事件侦听器函数

## 开放篇

- 对前端工程师这个职位是怎么样理解的？它的前景会怎么样
- 什么是前端工程化
- 未来三到五年的规划是怎样的
- 平时是如何学习前端的
- 项目中遇到的问题并怎么解决的




