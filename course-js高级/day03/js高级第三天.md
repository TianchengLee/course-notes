# js高级学习笔记


# js高级03天

## 1.函数的定义及调用
### 1.1函数的导读
- 复习一下之前的函数
- 学习函数的高级用法
- 能够说出函数的多种定义和调用
- 能够说出和改变函数内部的this指向
- 能够说出严格模式的特点
- 能够把函数作为参数和返回值传递
- 能够说出闭包的作用
- 能够说出递归的两个条件
- 能够输出浅拷贝和深拷贝的区别

### 1.2 函数的定义用
- 能够说出常用的函数定义的方式有哪几种？
```js
    function fn(){}
    var fn = function(){}
    var f = new Function(){}
```
- new Function()需要注意那几点
```js
    Function里面的参数必须是字符串格式
    使用较少，执行效率低，书写也不方便
    函数也是一个对象
    var fn = new Function()
    console.log(fn instanceof Object)//true
```

### 1.3 函数的调用
- 能够说出普通函数怎么调用？
- 能够说出对象的方法怎么调用？
- 构造函数的调用方式
- 事件绑定的函数的调用的方式
- 定时器函数的调用方式
- 立即执行函数的调用方式

## 2.函数的this指向以及改变this指向

### 2.1 函数内部的this指向
- 普通函数的this指向？
- 构造函数的this指向？
- 对象方法调用的this指向?
- 事件绑定的this指向?
- 定时器的this指向?
- 立即执行函数的this指向?

### 2.2 call方法的使用
- call方法是否会调用函数？
- call方法的作用是什么？
- call方法的应用场景？      
```js
        //父构造函数
        function Father(uname, age){
            this.uname = uname
            this.age = age
        }
        //子构造函数
        function Son(uname, age, score){
            //使用call改变this指向，这里的this是指向实例对象
            Father.call(this, uname, age)
            this.score = score
        }
        var son = new Son('刘德华',18,100)
        console.log(son)    
```

### 2.3 apply方法的使用
- apply方法能否直接调用函数
- apply方法的参数与call有什么区别
- apply方法一般的应用场景
```js

```
### 2.4 bind方法的使用
- bind方法能直接调用函数
- bind方法能否改变this指向
- bind方法的返回值是什么？
- bind方法的应用场景

### 2.5 call、apply、bind的区别
```
共同点: 都可以改变this指向
不同点:
call 和 apply 会调用函数, 并且改变函数内部this指向.
call 和 apply传递的参数不一样,call传递参数使用逗号隔开,apply使用数组传递 bind 不会调用函数, 可以改变函数内部this指向.
应用场景
1. call经常做继承.
2. apply经常跟数组有关系. 比如借助于数学对象实现数组最大值最小值
3. bind不调用函数,但是还想改变this指向.比如改变定时器内部的this指向.
```

## 3.js的严格模式

### 3.1 严格模式的定义
- 什么是严格模式？
- 为什么会有严格模式？
- 怎么开启严格模式？
- 怎么在一个函数里面开启严格模式

### 3.2 严格模式下的一些注意事项
- 严格模式下哪些操作是不能去做的
```js
 'use strict'
num = 10
console.log(num)//严格模式后使用未声明的变量 
‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐ ‐‐‐‐‐‐‐
var num2 = 1;
delete num2;//严格模式不允许删除变量 ‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐ ‐‐‐‐‐‐‐
function fn() {
console.log(this); // 严格模式下全局作用域中函数中的 this 是 undefined }
  fn();
  ‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐
  ‐‐‐‐‐‐‐‐
  function Star() {
this.sex = '男'; }
// Star();严格模式下,如果 构造函数不加new调用, this 指向的是undefined 如果给 他赋值则 会报错.
var ldh = new Star();
console.log(ldh.sex); ‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐‐ ‐‐‐‐‐‐‐‐‐
setTimeout(function() {
console.log(this); //严格模式下，定时器 this 还是指向 window
}, 2000);
```

## 4.高阶函数

### 4.1高阶函数的定义
- 什么是高阶函数
- 我们使用过哪些高阶函数

## 5.闭包

### 5.1 闭包的定义
- 复习变量的作用域
- 了解什么是闭包

### 5.2 闭包的作用
- 延伸变量的作用范围

### 5.3 闭包的应用
- 用闭包实现打车计价

### 5.4 闭包的扩展
```js
//思考题1：
        var name = 'The window';
        var object = {
            name: 'My Object',
            getNameFunc:function () {
                return function () {
                    return this.name;
                }
            }
        }
        console.log(object.getNameFunc()())//立即执行函数里面的this指向window
        //拆解1
        // var fn = function () {
        //         return function () {
        //             return this.name;
        //         }
        //     }
        //拆解2
        // fn = function () {
        //             return this.name;
        //         }
        //加上括号就是调用
        // fn()

        // 思考题二
        var name = 'The window';
        var object = {
            name: 'My Object',
            getNameFunc:function () {
                var that = this;
                return function () {
                    return that.name;
                }
            }
        }
        console.log(object.getNameFunc()())    
```

## 6.递归

### 6.1 递归的定义
- 什么是递归
- 递归需要注意哪些点
- 怎么用递归求斐波函数
- 使用递归实现数据的遍历案例

## 7.浅拷贝和浅拷贝
- 浅拷贝的对象级别的拷贝指向的是什么？

```js
        //浅拷贝只是拷贝一层，更深层次对象级别的只拷贝引用
        //深拷贝拷贝多层，每一级别的数据都会去拷贝
        var obj = {
            id: 1,
            name: 'Euni',
            msg:{
                age:18
            }
        };
        var o = {};
        
        // for (var k in obj) {
        //     //k 是属性的名字，obj[o]可以拿到对象的属性值
        //     o[k] = obj[k]
        // }
        // console.log(o)
        // //由于对象级别的拷贝只是拷贝引用的地址，一个改变，另一个跟着改变
        // o.msg.age = 20
        // console.log(obj)
        Object.assign(o, obj)
        o.msg.age = 30
        console.log(o)
        console.log(obj )
```

- 什么是深拷贝？

```js

```
- 使用递归实现深拷贝
- 扩展使用JSON.parse(),JSON.stringify()实现对对象的深拷贝
```js
//JSON.stringify()将 JavaScript json对象转换为JavaScript对象表示法的JSON字符串(对象转为字符串)
//JSON.parse()用于从一个JSON字符串中解析出json对象

var test={
    a:"ss",
    b:"dd",
    c:[
        {dd:"css",ee:"cdd"},
        {mm:"ff",nn:"ee"}
    ]
};

//拷贝一个字符串会新辟一个新的存储地址，这样就切断了引用对象的指针联系。
var test1 = JSON.parse(JSON.stringify(test));//拷贝数组,注意这行的拷贝方法
console.log(test);
console.log(test1);
test1.c[0].dd="change"; //改变test1的c属性对象的d属性
console.log(test);  //不影响test
console.log(test1);
//根据测试结果，我们可以看到，test1已经从test复制一份，并且test1改变其中属性的值时，对原来的对象test没有造成影响。

//注意
//JSON.parse(),JSON.stringify()兼容性问题
//可以通过为IE7以及IE7以下版本的IE浏览器引入json2.js，使用json2.js来解决JSON的兼容性问题
<!--[if lt IE 7]>
<script src="具体放路径/json2.js"></script> 
<![endif]-->
```













