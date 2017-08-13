### File API

HTML5在DOM中为文件输入元素添加了一个files集合。 在通过文件输入字段选择了一个或多个文件时，files集合中包含一组File对象，每个File对象对应着一个文件。每个File对象都有下列只读属性。

* name 本地文件系统中的文件名
* size 文件的字节大小
* type 字符串 文件MIME类型
* lastModifiedDate 上一次文件被修改的时间



### FileReader类型

它是一种异步文件读取机制。可以把FileReader想象成XMLHttpRequest，区别只是它读取的是文件系统。而不是远程服务器。为了读取文件中的数据 FileReader提供了几个方法。

* readAsText(file, encoding): 以纯文本形式读取文件，将读取到的文本保存在result属性中。第二个参数用于指定编码类型。可选

* readAsDataURL(file)：读取文件并将文件以数据URI 的形式保存在result 属性中。

* readAsBinaryString(file)：读取文件并将一个字符串保存在result 属性中，字符串中的

  每个字符表示一字节。

* readAsArrayBuffer(file)：读取文件并将一个包含文件内容的ArrayBuffer 保存在

  result 属性中。

  ​

  ​

  ​

  ### 图片上传 

















