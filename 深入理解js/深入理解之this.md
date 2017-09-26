#### setTimeout 中的this

setTimeout方法是让某个方法延迟执行。 setTimeout 方法是挂在window下的。 **超时调用的代码都是在全局作用域中执行。因此函数中this的值是非严格模式下指向 window对象。严格模式指向undefined**

结论：setTimeout中所执行函数中的this，永远指向window！！注意是要**延迟执行的函数中的this** 

**setTimeout(this.method, time)这种形式中的this，即上文中提到的第一个this，是根据上下文来判断的，默认为全局作用域，但不一定总是处于全局下，具体问题具体分析。**

**setTimeout(匿名函数, time)这种形式下，匿名函数中的变量也需要根据上下文来判断，具体问题具体分析**



### 函数调用一般指向的windows

```javascript
function a(){
    var user = "追梦子";
    console.log(this.user); //undefined
    console.log(this); //Window
}
a();

```



### 方法调用

再次强调一点，this的指向在函数创建的时候是决定不了的，在调用的时候才能决定，谁调用的就指向谁，一定要搞清楚这个。

```javascript
var o = {
    user:"追梦子",
    fn:function(){
        console.log(this.user);  //追梦子
    }
}
o.fn();

var o = {
    user:"追梦子",
    fn:function(){
        console.log(this.user); //追梦子
    }
}
window.o.fn(); // 最终this指向的是调用它的对象
```

如果一个函数中有this，**这个函数中包含多个对象，尽管这个函数是被最外层的对象所调用，this指向的也只是它上一级的对象**



#### 构造函数this

```javascript
function Fn(){
    this.user = "追梦子";
}
var a = new Fn();
console.log(a.user); //追梦子

```



#### 当this碰到return的时候

```javascript
function fn()  
{  
    this.user = '追梦子';  
    return {};  
}
var a = new fn;  
console.log(a.user); //undefined

function fn()  
{  
    this.user = '追梦子';  
    return {
        name: 'shiyao'
    };  
}
var a = new fn;  
console.log(a.user); //shiyao


function fn()  
{  
    this.user = '追梦子';  
    return function(){};
}
var a = new fn;  
console.log(a.user); //undefined

function fn()  
{  
    this.user = '追梦子';  
    return 1;
}
var a = new fn;  
console.log(a.user); //追梦子

function fn()  
{  
    this.user = '追梦子';  
    return undefined;
}
var a = new fn;  
console.log(a); //fn {user: "追梦子"}
```

**如果返回值是一个对象，那么this指向的就是那个返回的对象，如果返回值不是一个对象那么this还是指向函数的实例。**



