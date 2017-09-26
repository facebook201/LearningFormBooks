#### apply、call、bind。都是继承自Function的方法。



apply 调用一个函数，具有一个指定的this值，以及作为一个数组（或类似数组的对象）提供的参数。**call方法跟apply类似，接受若干个参数列表 apply是一个参数的数组**

语法：**fun.apply(thisArg, [argsArray])** 

参数: 

  thisArg: 在fun运行时指定的this值。需要注意的是 指定的this值并不一定是该函数执行时真正的this值。如果在非严格模式下 则指定null 或 undefined 时会自动指向全局对象。原始值得this会指向原始值得自动包装对象。

argsArray: 一个数组或者类数组对象，其中的数组元素将作为单独的参数传给 `fun` 函数。如果该参数的值`为null` 或 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)，则表示不需要传入任何参数。

```javascript
var numbers = [1, 3, 5, 7];
var max = Math.min.apply(null, numbers); // 7
var min = Math.min.apply(null, numbers); // 1
```



* bind 跟 apply 和 call 一样都是用来改变this指向的。 它不同的是会创建一个新的函数。（**它不会立即执行**）当被调用时 将其this 关键值设置为提供的值。在调用新函数时。**返回由指定的this值和初始化参数改造的原函数拷贝**

  ```javascript
  this.x = 9;
  var module = {
    x: 81,
    getX: function(){
      return this.x;    
    }
  };
  module.getX(); // 81
  var retrieveX = module.getX;
  retrieveX(); // 9
  // 创建一个新函数，将"this"绑定到module对象
  // 新手可能会被全局的x变量和module里的属性x所迷惑
  var boundGetX = retrieveX.bind(module);
  boundGetX(); // 返回 81
  ```

* setTimeout

  ```javascript
  const dog = {
    name: '1',
    catch: function(){
      setTimeout(function(){
        console.log(this.name); // undefined
      }, 1000);  
    }
  };
  // 这里setTimeout里面函数是一个匿名函数 因为setTimeout是挂在window下的。 超时代码都是在全局作用域里面执行。因此函数中的this在非严格模式下面指向window 严格模式指向undefined
  ```

  ​



* 偏函数应用 **使一个函数拥有预设的初始参数。这些参数作为bind的第二个参数跟在this(或者其他对象比如 null, undefined)后面.之后它们会被插入到目标函数的参数列表的开始位置，传递给绑定函数的参数会跟在他们后面**

  ```javascript
  function list(){
    return Array.prototype.slice.call(arguments);    
  }

  var bindList = list.bind(undefined, 30);

  bindList(); // [30]
  bindList(1, 2, 3); // [30, 1, 2, 3]
  ```

#### 偏函数 和 柯里化函数

偏函数解决的问题: 如果我们有函数是多个参数的 我们希望能够固定器中某几个参数的值。如果有一个函数要多次调用 这样无需多次传入第一个参数，已经被bind绑定好了。　作为将函数当做返回值输出的典型应用就是偏函数。所谓偏函数是指创建一个调用另外一个部分——参数或变量已经预置的函数——的函数的用法。

指定部分参数来返回一个新的定制函数的形式就是偏函数**

```javascript
// isType 函数就是一个典型的偏函数应用
function isType(type){
  return function(obj){
    return Object.prototype.toString.call(obj) === '[object ' + type + ']'; 
  }    
}
```





**柯里化** : 转换 一个调用函数 f(a, b, c) 为 f(a)(b)(c) 方式调用。用于创建已经设置好了一个或多个参数的函数。使用闭包返回一个函数。 当函数被调用时 返回的函数还需要传一些参数。

**调用另一个函数并为它传入要柯里化的函数和必要参数。** 

```javascript
function curry(fn){
  // 保留参数 除去第一个回调函数
  var args = Array.prototype.slice.call(arguments, 1);    
  return function(){
    var innerArgs = Array.prototype.slice.call(arguments);
    var finalArgs = args.concat(innerArgs); // [args, ...innerArgs]
    return fn.apply(null, finalArgs);
  }
}

function add(num1, num2){
  return num1 + num2;    
}
var curried = curry(add, 5);
console.log(curried(3)); // 8


// 创造出更复杂的bind函数
function bind(fn, context){
	var args = Array.prototype.slice.call(arguments, 2);
	return function(){
		var innerArgs = Array.prototype.slice.call(arguments);
		var finalArgs = args.concat(innerArgs);
		return fn.apply(context, finalArgs);
	};
}
```



总结

- 偏函数应用是找一个函数，固定其中的几个参数值，从而得到一个新的函数。
- 函数加里化是一种使用匿名单参数函数来实现多参数函数的方法。
- 函数加里化能够让你轻松的实现某些偏函数应用。





































