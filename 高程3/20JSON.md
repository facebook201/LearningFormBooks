### JSON

20.1 语法 可以表示下面三种类型的值

* 简单值：使用JavaScript相同的语法。可以在JSON中表示字符串、数值、布尔值、null。 但是JSON不支持undefined
* 对象： 对象作为一种复杂数据类型、表示的是一组无序的键值对。
* 数组： 数组也是一种复杂数据类型。表示一组有序的值的列表。可以通过数值索引来访问其中的值。



#### 对象



```javascript
//  字面量对象 
var person = {
    name: 'Nicholas',
  	age: 29
};

JSON.stringfy(person);
{
    "name": "Nicholas",
    "age": 29
}

// 数组
// JSON 中的第二种复杂数据类型是数组。 JSON数组采用的就是JavaScript中的数组字面量形式。
var values = [24, 'hi', true];

"[24, "hi", true ]"

// JSON数组没有变量和分好 把数组和对象结合起来 可以构成更复杂的数据集合
[
    {
        "title": "Perfessional JavaScript",
      	"authors": [
            "name": "shiyao"
        ],
      	edition: 2
    },
    {
        "title": "Perfessional JavaScript",
      	"authors": [
            "name": "shiyao"
        ],
      	edition: 2
    }
]
```





### JSON 对象 

```javascript
var book = {
  name: 'syo',
  age: 23
};

// stringify() 把JavaScript对象序列化为JSON字符串 
var json = JSON.stringify(book);
{
    "name": "syo",
     "age": 23
}

// parse() 把JSON字符串解析为原生的JavaScript值


```

































