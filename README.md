
<h1 align="center">《JavaScript踩坑指南》JavaScrip-StepPitGuide📖</h1>
<p align="center"><img src="http://www.kejiganhuo.tech/wp-content/uploads/2017/03/cropped-319907-106.jpg" /></p>

---

* 三句箴言

1. **一入前端深似海，任何前端小白也可成为大牛，要用心体会前端知识，说前端简单的什么的最变态了！**

2. **永远都不要以为自己会了，细心体会基础多去扩展知识永远都需要学习，因为你不知道面试的时候面试官是个什么样的大牛！**

3. **你努力，不一定能成功，你不努力，连机会都会没有。**

* 注 ：面试为`校招面试`
---

<h1 align="center">序</h1>

---

# 目录

## 第一章 面试经历

[01-01](https://github.com/TYRMars/JavaScrip-StepPitGuide)`2018校招阿里面试提前批-前端开发工程师-8.7`

[01-02](https://github.com/TYRMars/JavaScrip-StepPitGuide)`2018校招腾讯面试提前批-前端开发工程师-8.14`

## 第二章 问题总结

[02-01](https://github.com/TYRMars/JavaScrip-StepPitGuide)`阿里面试问题总结`

[02-02](https://github.com/TYRMars/JavaScrip-StepPitGuide)`腾讯面试问题总结`


## 附录：知识点

### 自己总结的知识

* [TYRMars/JSLearn](https://github.com/TYRMars/JSLearn) `JavaScript基础知识学习总结`

* [TYRMars/JSLearn-ES6](https://github.com/TYRMars/JSLearn-ES6) `ES6知识学习总结`

* [TYRMars/ReactLearn](https://github.com/TYRMars/ReactLearn) `React基础知识学习总结`

* [TYRMars/WebsafeLearn](https://github.com/TYRMars/WebsafeLearn) `Web安全知识学习总结`

### JavaScript基础知识点

* [MDN - 最标准的Web前端文档](https://developer.mozilla.org/zh-CN/)
* [script标签要放到哪里](http://blog.csdn.net/ybdesire/article/details/49284699)
* [深入理解javascript原型和闭包 - 王福朋](http://www.cnblogs.com/wangfupeng1988/p/4001284.html)

### JavaScript事件问题

* [深入浅出JS事件](http://www.cnblogs.com/jingwhale/p/4656869.html)
* [JQuery ready和load的 区别](http://blog.csdn.net/u010555110/article/details/51861054)
* [JQuery ready和load的 区别 - 慕课网](http://www.imooc.com/code/3253)
* [zepto的tap事件点透分析](http://smile-leaf-language.github.io/2016/02/02/zepto-tap/)

### JavaScript通信问题📞

* [跨域问题](http://blog.csdn.net/joyhen/article/details/21631833)
* [webpack跨域 http-proxy-middleware](http://www.jb51.net/article/120259.htm) / [npm模块之http-proxy-middleware使用教程（译）](http://blog.csdn.net/xmloveth/article/details/56847456)
* [IE8和IE9上的HTTP access control (CORS) 的实现 --- XDomainRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XDomainRequest)

### CSS

* [CSS知多少](http://www.cnblogs.com/wangfupeng1988/p/4325007.html)
* [利用HTML和CSS实现常见的布局](https://segmentfault.com/a/1190000003931851)
* [前端移动端页面开发（布局篇）](http://www.xiaoxiangzi.com/Programme/CSS/4298.html)
* [手机网站📱常见六种布局](http://www.qdfuns.com/notes/17640/934ef9a496386a5243b449cdf3faceea:storey-3.html)
* [Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
* [Flex 布局教程：实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

---

# 第一章

## 01-01
### 阿里面试

* 此次面试，面试的是阿里巴巴国际UED的前端团队

* 面试的主要问题：
    * DOM事件
    * 实习项目中常用的API
    * Web安全
    * 前端性能优化
    * 跨域问题

## 01-02
### 腾讯面试

* 此次面试，面试的是腾讯QQ音乐前端开发

* 面试主要问题：
    * DOM事件
    * 页面加载<script>标签放到哪里
    * 对比load和ready (考察点在与页面加载DOMContentLoaded)与script标签问题同在一个知识链条上
    * 跨域问题
    * 页面性能优化

# 第二章

## 02-01
### 阿里面试总结

## 02-02
### 腾讯面试总结

```JavaScript
function ajax(url,fnSucc,fnFaild) {
    //1.创建ajax对象
    if(window.XMLHttpRequest){
        var iAjax = new XMLHttpRequest();
    }else{
        var iAjax = new ActiveXObject("Microsoft.XMLHTTP");
    }
    //2.连接服务器
    //open(方法、文件名、异步传输)
    iAjax.open('GET',url,true);
    //3.发送请求
    iAjax.send();
    //4.接受返回
    iAjax.onreadystatechange = function () {
        //iAjax.readyState 浏览器和服务器进行到哪一步了
        if(iAjax.readyState == 4){
            if(iAjax.status == 200){
                fnSucc(iAjax.responseText);
            }
            else{
                if(fnFaild){
                    fnFaild(iAjax.status);
                }
                alert('失败'+iAjax.status);
            }
        }
    }
}

(function() {
    var TOUCHSTART, TOUCHEND;
    if (typeof(window.ontouchstart) != 'undefined') {
        TOUCHSTART = 'touchstart';
        TOUCHEND = 'touchend';
        TOUCHMOVE ='touchmove';

    } else if (typeof(window.onmspointerdown) != 'undefined') {
        TOUCHSTART = 'MSPointerDown';
        TOUCHEND = 'MSPointerUp';
        TOUCHMOVE = 'MSPointerMove';
    } else {
        TOUCHSTART = 'mousedown';
        TOUCHEND = 'mouseup';
        TOUCHMOVE = 'mousemove';
    }
    function NodeTouch(node) {
        this._node = node;
    }
    function tap(node,callback,scope) {
        node.addEventListener(TOUCHSTART, function(e) {
            x = e.touches[0].pageX;
            y = e.touches[0].pageY;
        });
        node.addEventListener(TOUCHEND, function(e) {
            e.stopPropagation();
            e.preventDefault();
            var curx = e.changedTouches[0].pageX;
            var cury = e.changedTouches[0].pageY;
            if (Math.abs(curx - x) < 6 && Math.abs(cury - y) < 6) {
                callback.apply(scope, arguments);
            }
        });
    }
    function longTap(node,callback,scope) {
        var x,y,startTime=0,endTime=0,in_dis=false;
        node.addEventListener(TOUCHSTART, function(e) {
            x = e.touches[0].pageX;
            y = e.touches[0].pageY;
            startTime=(new Date()).getTime();
        });
        node.addEventListener(TOUCHEND, function(e) {
            e.stopPropagation();
            e.preventDefault();
            var curx = e.changedTouches[0].pageX;
            var cury = e.changedTouches[0].pageY;
            if (Math.abs(curx - x) < 6 && Math.abs(cury - y) < 6) {
                in_dis=true;
            }else{
                in_dis=false;
            }
            endTime=(new Date()).getTime();
            if (endTime - startTime > 300 && in_dis) {
                callback.apply(scope, arguments);
            }
        });
    }
    NodeTouch.prototype.on = function(evt, callback, scope) {
        var scopeObj;
        var x,y;
        if (!scope) {
            scopeObj = this._node;
        } else {
            scopeObj = scope;
        }
        if (evt === 'tap') {
            tap(this._node,callback,scope);
        } else if(evt === 'longtap'){
            longTap(this._node,callback,scope);
        } else {
            this._node.addEventListener(evt, function() {
                callback.apply(scope, arguments);
            });
        }
        return this;
    };
    window.$ = function(selector) {
        var node = document.querySelector(selector);
        if (node) {
            return new NodeTouch(node);
        } else {
            return null;
        }
    }
})();

var box=$("#box");
box.on("longtap",function(){
    console.log("你已经长按了");
},box);
```
