### 7.2 闭包

有权访问另一个函数作用域中的变量的函数。常见方式就是在一个函数的内部创建另一个函数。

```javascript
function createFunction(propertyName) {
  return function(obj1, obj2) {
    var value1 = obj1[propertyName];
    var value2 = obj2[propertyName];
    return value1 > value2 ? 1 : 0;
  }
}
```



#### 7.2.1 闭包与变量

作用域链的这种配置机制引出了一个副作用。即闭包只能取得包含函数中任何变量的最后一个值。

```javascript
function createFunction() {
  var result = new Array();
  for (var i = 0; i < 10; i++) {
    return [i] = function() {
      return i;
    };
  }
  return result;
}
```

这里for循环里面的每个函数的作用域链都保存着createFunction函数的活动对象 所有他们引用的都同一变量i。当createFunction 函数返回后。变量i的值是10，此时每个函数都引用着保存变量i的同一个变量对象，所以在每个函数内部i的值都是10。但是我们可以创建另一个匿名函数来强制让闭包的行为符合预期

```javascript
function createFunction() {
  var result = new Array();
  for (var i = 0; i < 10; i++) {
    return[i] = function(num) {
      return function() {
        return num;
      };
    }(i);
  }
  return result;
}
```





 















