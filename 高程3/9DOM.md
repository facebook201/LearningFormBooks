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

*  ​

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

  * hasChildNodes() 也是一个非常有用的方法。这个方法在节点包含一个或者多个子节点的情况下 返回true

    ​

* ​























