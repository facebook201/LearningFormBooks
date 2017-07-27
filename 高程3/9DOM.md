## DOM 节点



#### 10.1 节点层次

每个节点都有自己的数据、特点和方法。**节点分为几种不同的类型、每种类型表示不同的信息及标记。** 节点另外与其他的节点也存在某种关系 构成了层次关系。

**文档节点是每个文档的根节点。** 即document。这里的文档节点只有一个子节点 即html元素。 称为**文档元素**



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

*  

### Node类型

所有的节点类型都继承自Node。所有的节点类型都共享着基本的属性和方法。每个节点都有一个nodeType属性。表示节点的类型。