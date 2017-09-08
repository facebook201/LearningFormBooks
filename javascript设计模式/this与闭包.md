#### 3.1 变量的作用域

局部变量只有在函数内部访问的到 函数外面是访问不到的。而且变量的搜索是从内到外而非从外到内的。

```javascript
var a = 1;
var fun = function() [
  var b = 2;
  var fun2 = function() {
    var c = 3;
  	console.log(a);
    console.log(b);
  }
  fun2();
  console.log(c)； // ReferenceError:
];
fun(); // 
```



#### 变量的生存周期

全局变量的生命周期是永久的，但是局部变量的生命周期随着函数调用的解暑而销毁。

```javascript
var func = function(){
  var a = 1;
  return function(){
    a++;
    alert ( a );
  }
};
var f = func();

f(); // 输出：2
f(); // 输出：3
f(); // 输出：4
f(); // 输出：5  
```

 当退出函数后，局部变量a  并没有消失，而是似乎一直在某个地方存活着。这是因为当执行var f = func(); 时，f  返回了一个匿名函数的引用，它可以访问到func()被调用时产生的环境，而局部变量a  一直处在这个环境里。既然局部变量所在的环境还能被外界访问，这个局部变量就有了不被销毁的理由。在这里产生了一个闭包结构，局部变量的生命看起来被延续了。



**判断类型**

```javascript
function isType(type) {
  return function(obj) {
    return Object.prototype.call.toSTring.call(obj) === '[object' + type +']';
  }
}
```







#### 高阶函数

* 函数可以作为参数被传递
* 函数可以作为返回值输出



#### 函数作为参数传递

* 回调函数  在ajax  异步请求的应用中，回调函数的使用非常频繁。当我们想在ajax  请求返回之后做一

  些事情，但又并不知道请求返回的确切时间时，最常见的方案就是把callback  函数当作参数传入

  发起ajax  请求的方法中，待请求完成之后执行callback  函数：

  ```javascript
  var getUserInfo = function(userId, callback) {
      $.ajax('http://xx')
  } 
  ```

  ​

* ​































