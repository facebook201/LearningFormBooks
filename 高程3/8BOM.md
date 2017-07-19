### BOM (浏览器对象模型)

BOM的核心对象是window，它表示浏览器一个实例。ECMAScript表示规定的Global对象。意味着在网页中定义的任何一个对象、变量和函数。都以window作为其Global对象。



#### 8.2 location对象

location 是一个很特别的对象。既是window对象的属性。也是document对象的属性。



### 8.2.1  查询字符串参数

解析查询字符串，然后返回包含所有参数的一个对象

```javascript
function getQueryStringArgs() {
  // 取得查询字符串去掉开头的问号
  var qs = (location.search.length > 0) ? location.search.substring(1) : '',
  // 保存数据对象
  args = {},
  
  // 取得每一项
  items = qs.length ? qs.split('&') : [],
  item = null,
  name = null;
  // 在循环中使用
  i = 0, len = items.length;
  // 逐个将每一项添加到args对象中
  for (i = 0; i < len; i++) {
   item = items[i].split('=');
   name = decodeURIComponent(item[0]);
    if (name.length) {
      args[name] = decodeURIComponent(item[1]);
    }
  }
  return args;
}
```



### 8.2.2 位置操作

location对象通过很多方式来改变浏览器的位置。使用assign() 方法为其传递一个URL。

location.assign('http://www.baidu.com');

window.location = 'http://www.baidu.com';

location.href="http://www.baidu.com";



#### 9.1 能力检测 又称特性检测

能力检测相当于想知道某个特性是否会按照适当方式来进行。 举个例子

```javascript
// 这种方式其实是没有用的 只是检测了是否存在相应的方法
function isSortable(object) {
  return !!object.sort;
}
// 但是任何包含sort属性的对象也会返回true。
var result = isSortable({ sort: true });

// 更好的方式是判断它是不是一个函数
function isSortable(object) {
  return typeof object.sort === 'function';
}
```



DOM对象是宿主对象，IE以及更早的版本中宿主对象是通过COM而非JS实现的。

* 内置对象：在引擎初始化阶段就创建好的对象。是原生对象的一个子集。原生对象包括了一些运行过程中动态创建的对象

  ​

* 原生对象 独立于宿主环境的ECMAScript实现

  ​

* 宿主对象不是引擎的原生对象。而是由宿主框架通过某种机制注册到js引擎中的对象。

  ![border](http://liuwanlin.info/content/images/2015/Mar/1212164ejwgmjheh1m7hhm-1.png?_=4990917)

* ​
























