
### Date 实例是用来处理日期和时间。Date对象基于1970年1月1日起的毫秒数

```javascrit

var today = new Date(); // 当前时间 Wed Aug 16 2017 10:30:01 GMT+0800 (中国标准时间)


```





### API 

```javascript

Date.prototype.toLocaleTimeString(); 
// 返回改日期对象时间部分的字符串 新增参数(locales, options) 指定语言和语言格式化规则

new Date().tolocaleTimeString(); // 上午 10:10:10 
new Date().tolocaleTimeString('en-US'); // 10:10:10 AM


```