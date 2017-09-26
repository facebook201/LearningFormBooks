#### 对象使用和属性

javascript中所有变量都是对象。除了null 和 undefined。

常见的错误数字的字面量不是对象。它试图将点操作符解析为浮点数字面值得一部分。

```javascript
2.toString(); // SyntaxError
2..toString(); // 第二个点可以正常解析
2 .toString(); // .前面的空格
(2).toString(); // 优先计算2
```



#### 删除属性

删除属性的唯一方法使用 delete操作符；设置属性为 undefined 或 null 无法真正的删除属性。而仅仅是移除了属性和值的关联。



#### hasOwnProperty 函数

判断一个对象是否包含自定义属性而不是原型链上的属性。注意一点 javascript不会保护hasOwnProperty。因此如果一个对象碰巧存在这个属性。就需要使用外部的hasOwnProperty函数来获取正确的结果。

```javascript
var foo = {
    hasOwnProperty: function() {
        return false;
    },
    bar: 'Here be dragons'
};
foo.hasOwnProperty('bar'); // 总是返回 false
// 使用其它对象的 hasOwnProperty，并将其上下为设置为foo
{}.hasOwnProperty.call(foo, 'bar'); // true
```

一般来说 没有人这样做。



#### instanceof 运算符

它返回一个布尔值。表示指定对象是否为某个构造函数的实例。

```javascript
var v = new V();
v instanceof V; // true

// 对整个原型链上的对象都有效
var d = new Date();
d instanceof Date // true
d instanceof Object // true

// instanceof的原理是检查原型链，对于那些不存在原型链的对象，就无法判断。
Obejct.create(null) instanceof Object;
```

左边是实例对象。右边是构造函数。

由于`instanceof`对整个原型链上的对象都有效，因此同一个实例对象，可能会对多个构造函数都返回`true`。

`instanceof`运算符只能用于对象，不适用原始类型的值。









