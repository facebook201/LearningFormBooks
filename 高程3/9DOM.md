## DOM 节点



#### 10.1 节点层次

每个节点都有自己的数据、特点和方法。**节点分为几种不同的类型、每种类型表示不同的信息及标记。** 节点另外与其他的节点也存在某种关系 构成了层次关系。

**文档节点是每个文档的根节点。** 即document。这里的文档节点只有一个子节点 即html元素。 称为**文档元素**

docuemnt // document nodeType是9

​	html // element nodeType 是 1

```html
<html> // Element
  <head> // Element
	<title>Sample Page // Text </title>
  </head>
  
  <body>
  	     
  </body>
</html>
```



**每一段标记可以通过树中的一个节点表示、** 一共有12个节点类型 

**someNode.nodeType**  就可表示一个节点类型。 返回的阿拉伯数字对应下面的节点类型

* Node.**ELEMENT_NODE**; // 1 元素节点 例如 <p> <div>

  document.querySelector('html').nodeType === 1; // html 文档元素 节点类型是元素节点 

* Node.ATTRIBUTE_NODE(2); // 2 属性节点

* Node.**TEXT_NODE**; // 3 ELement 或者Attr 中的文字

* Node.COMMENT_NODE; // 8 comment节点

* DOCUMENT_NODE; // 9 Document 节点

* ​

### Node类型

所有的节点类型都继承自Node。所有的节点类型都共享着基本的属性和方法。每个节点都有一个nodeType属性。表示节点的类型。为了确保浏览器兼容，最好还是讲nodeTpye数学的数字值进行比较。

```javascript
if (someNode.nodeType === 1) // 兼容所有的浏览器

document.nodeType; // 1 文档节点
document.querySelector('html').nodeType; // 9 元素节点
```

* 1 **nodeName** 和 **nodeValue** 属性

  这两个值完全取决于节点类型。 使用之前 最好先检测一下节点类型。

  if (someNode.nodeType === 1) {

  ​	value = someNode.nodeName; 

  }

  **对于元素节点。nodeName中保存的始终都是元素的标签名.而nodeValue的值始终为null**

* **节点关系**

  每一个节点都有childNodes属性。保存一个NodeList对象。它是一种类数组对象，用于保存一组有序的节点。可以通过位置来访问这些节点。他不是一个数组，类似数组。它实际上是基于COM结构动态执行查询的结果，因此DOM结构的变化能够自动反映在NodeList对象中。

  ```javascript
  // 如何访问保存在NodeList中的节点
  var firstChild = someNode.childNodes[0];
  someNode.childNode[0] === someNode.firstChild;
  var secondChild = someNode.childNodes.item(1);
  var count = someNode.childNodes.length; // nodelist的长度
  someNode.parentNode; // 当前节点的父节点

  someNode.hasChildNodes(); // 判断这个节点是否有子节点 返回布尔值

  // 将NodeList 转为 数组
  Array.prototype.slice.call(someNode.childNodes);
  ```

  每一个节点都有一个parentNode属性。 包含在childNodes列表中的每个节点相互之间都是同胞节点。使用列表中每个节点的previousSibling和nextSibling属性。 列表中第一个节点的previousSibling属性为nul，而列表中最后一个节点的nextSibling属性的值同样为null。

  * hasChildNodes() 也是一个非常有用的方法。这个方法在节点包含一个或者多个子节点的情况下 返回true。这个比查询childNodes列表的length属性更简单的方法

    **虽然所有节点类型都继承自Node，但并不是每种节点都有子节点。**





### 3 操作节点

* 插入节点

  * appendChild() ：向childNodes列表的末尾添加一个节点。appendChild(添加的新节点)。向节点的子节点**列表的末尾添加新的子节点**。

    ```javascript
    var node = document.querySelector('#app');
    var childNode = document.createElement('p');
    childNode.className = 'child-node';
    childNode.innerHTML = 'appendChild向childNodes列表的末尾添加一个子节点';
    node.appendChild(childNode);
    ```

  * insertBefore()：把节点插入到指定的位置 如果你不想放在末尾。接受两个参数。parentNode.insertBefore(新节点, 已知节点); 在已知节点的前面插入一个新的节点。如果参照的节点数null 就跟appendChild() 是一样的。

    ```javascript
          var parentNode = document.getElementById('app'); // 父节点
          var node = document.querySelector('.node'); // 兄弟节点一
          var newNode = document.createElement('span'); // 兄弟节点二
          node2.className = 'node2'; 
          parentNode.insertBefore(newNode, node); 
    ```

    ​

* 移除节点  **removeChild** 接受一个参数 即要移除的节点。被移除的节点成为方法的返回值

  ```javascript
        var parentNode = document.getElementById('app'); // 父节点
        var node = document.querySelector('.node');
        var result = parentNode.removeChild(node);
        console.log(result); // <p class="node2"></p>
  ```

  ​

* 替换节点

  **replaceChild()方法接受两个参数是：要插入的节点和要替换的节点。** 要替换的节点将由这个方法返回并从文档树种删除。同时由要插入的节点占据其位置。

  parentNode.replaceChild(newNode, node);

  ```javascript
  var parentNode = document.getElementById('app'); // 父节点
        var node = document.querySelector('.node');
        var newNode = document.createElement('span');
        newNode.innerHTML = 'new Node';
        parentNode.replaceChild(newNode, node);
  ```

  ​

* 复制节点 **cloneNode**

  用于创建调用这个方法的节点的一个完全相同的副本。cloneNode()方法接受一个布尔值参数，表示是否执行深复制。在参数为true的情况下  复制整个**子节点树** 






### 10.2 Document 类型

JavaScript通过Document类型表示文档。在浏览器中 document 对象是HTMLDocument（继承自Document类型）的一个实例。document对象是window对象的一个属性，因此可以将其作为全局对象来访问。

* nodeType是9;   document.nodeType === Node.DOCUMENT_NODE === 9;
* nodeName的值 ‘#document’ 返回当前节点的节点名称
* nodeValue parentNode的值都是null。





### 10.2.1 文档的子节点

* Document 节点的子节点可以是**DocumentType、Element** 还有两个内置的访问子节点的快捷方式。第一个就是documentElement属性，它是一个会返回文档对象的根元素的**只读属性** (html元素) 

  document.documentElement === document.childNodes[0] === document.firstChild

* document.body 属性。指向body元素。

  var body = document.body; 

  ​

* 文档信息。 

  其中第一个属性就是 title，包含着 title元素中的文本，显示在浏览器窗口的标题栏。 

  document.title; // 取得文档标题

  document.URL; // 地址栏中显示的URL

  document.domain; // 取得域名

  ​

#### 查找元素

* document.getElementById(); 接受一个参数 取得元素的ID；找到返回该元素 否则返回null; 
* document.getElementsByName();  通过元素的name属性来获取节点
* document.getElementsByTagName(); 通过元素标签获取节点



#### Element类型

ELement类型就要算用的最多的类型。具有以下特征

* nodeType值为 1
* nodeName值为元素的标签名
* nodeValue 值为null
* parentNode可能是Document 或Element





#### 属性操作

* 获取属性 getAttribute （元素节点.getAttribute(元素属性名)）获取元素节点中指定属性的属性值
* 设置属性 setAttribute   (属性名, 属性值) 创建或改变元素节点的属性
* 删除属性 removeAttribute  元素节点.removeAttribute(属性名) 删除指定的属性



**attributes属性**

Element类型是使用attributes属性的唯一一个DOM节点类型。包含一个NamedNodeMap，是一个集合。类似于NodeList。也是一个"动态"集合。元素的每一共特性都有一个attr节点表示。



#### 创建节点

* createElement 

  document.createElement(元素标签); 创建元素节点

* createAttribute 

  document.createAttribute(元素属性) 创建属性节点

* createTextNode 

  document.createTextNode(文本内容) 创建文本节点

  ​

#### 文档片段 DocumentFragment类型

在所有类型中，只有DocumentFragement在文档中没有对应的标记。DOM规定文档片段是一种轻量级的文档。

* nodeType 为11
* nodeName 值是 '#document-fragment'
* nodeValue 是 null
* parentNode值是null



假设我们为ul元素添加三个列表项。如果逐个添加列表项。将会导致浏览器反复渲染 

```javascript
var fragment = document.createDocumentFragment();
var ul = document.getElementById('ul');
var li = null;

for (var i = 0; i < 3; i++) {
  li = document.createElement('li');
  li.appendChild(document.createTextNode('item ' + (i + 1)));
  fragment.appendChild(li);
}
ul.appendChild(fragment);
```





##### 插入标记 1. innerHTML 属性

在读写模式下。innerHTML属性返回与调用元素的所有子节点对应的HTML标记。



* element的children是一个只读属性，返回一个Node的子elements的 HTMLCollection实例，只包含元素中同样的子节点。除此之外 children 属性与childNodes没有区别。即在元素中只包含元素节点。

  ​

* contains() 方法 返回一个布尔值 来表示传入的节点是否为该节点的后代节点。Node.contains

  实际开发中 经常需要知道某个节点是不是另一个节点的后代。方法接受一个参数 即检测后代节点。如果被检测的节点是后代节点，该方法返回true; 否则false

  ```javascript
  document.documentElement.contains(node);
  ```

* innerText 属性

  innerText属性可以操作元素中包含的所有文本内容。包括子文档树种的文本。在通过innerText读取值时。

  在通过innerText写入值的时候。会删除元素的所有子节点 插入包含相应文本值的文本节点。

  ```html
  <div id="app">
    <p>This is a list</p>
    <ul>
    	<li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </ul>
  </div>
  ```

  ```javascript
  // 这里 我们先来看看 innerHTML 和 innerText的区别
  var parentNode = document.querySelector('#app');
  parentNode.innerHTML; 
  /**
    <p>This is a list</p>
    <ul>
    	<li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </ul>
  */

  /** innerText 
   * This is a list
   * Item 1
   * Item 1
   * Item 1
   */

  parentNode.innerText = 'hello world';
  // 最后就是下面的结构
  <div id="app">Hello world!</div>
  ```

  我们可以看到 两者的区别。innerText返回的值text内容。不会返回dom。 





### DOM2 和 DOM3



* 12.2 样式

  任何支持style特性的html元素在JavaScript中都有一个对应的style属性。 这个对象是一个CSSStyleDeclaration的实例。

  ```javascript
  var node = document.getElementById('app');

  node.style.backgroundColor = '#f00'; // 设置node盒子的背景色是红色
  ```

  其中一个不能直接转换的CSS属性是float。由于它是js的保留字。不能用作属性名。 cssFloat;IE支持styleFloat;



*  计算的样式 

  “DOM2级样式增强了document.defaultView” 提供了getComputedStyle方法、这个方法接受两个参数：要取得计算样式的元素和一个为元素字符串。如果不需要 第二个参数可以为null. 返回CSSStyleDeclaration对象。包含所有当前元素的所有计算样式。

  ```javascript
  var box = document.getElementById('myDiv');
  // 判断是否存在 特性检测
  if (document.defaultView) {
    
  }
  var computedStyle = document.defaultView.getComputedStyle(box, null);
  ```

  ​

* 元素大小

  * 偏移量

    * offsetHeight: 元素在垂直方向上占用的空间大小。像素为单位。

    * offsetWidth: 元素在水平方向上占用大小。 包括边框 clientWidth 不包括边框

      width + padding + margin + border

    * offsetLeft：元素的左外边框至包含元素的左内边框之间的像素距离。

    * offsetTop：元素的上外边框至包含元素的上内边框之间的像素距离。

    所有这些偏移量属性都是只读的，而且每次访问它们都需要重新计算。因此，应
    该尽量避免重复访问这些属性；如果需要重复使用其中某些属性的值，可以将它们保
    存在局部变量中，以提高性能。

    ​

  * 客户区大小 

    * clientWidth : 元素内容区宽度加上左右内边距宽度
    * clientHeight : 是元素内容区高度加上上下内边距高度

    width + padding + margin 

    ​

  * 滚动大小

    * scrollHeight：在没有滚动条的情况下，元素内容的总高度。

    * scrollWidth：在没有滚动条的情况下，元素内容的总宽度。

    * scrollLeft：被隐藏在内容区域左侧的像素数。通过设置这个属性可以改变元素的滚动位置。

    * scrollTop：被隐藏在内容区域上方的像素数。通过设置这个属性可以改变元素的滚动位置。

      ​

  * 确定元素大小 

    * top
    * left
    * right
    * bottom
    * height
    * width

    对于不支持getBoundingClientRect()的浏览器，可以通过其他手段取得相同的信息。一般来
    说，right 和left 的差值与offsetWidth 的值相等，而bottom 和top 的差值与offsetHeight
    相等.

    ```javascript
    var parent = document.getElementById('app');
    var box = parent.getBoundClientRect();

    height = box.bottom - box.top;
    width = box.right - box.left;
    ```





* ​

  ​

