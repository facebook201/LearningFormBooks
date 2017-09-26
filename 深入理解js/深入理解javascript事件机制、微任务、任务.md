事件循环具有多个任务源，他们保证该源中的执行顺序，但是浏览器可以从循环的每个回合中选择哪个来源执行任务。浏览器会优先考虑性能敏感的任务。

* javascript 代码的执行过程中。除了一些函数调用栈来处理函数的执行顺序。还依靠任务队列（task queue）来处理另一些代码的执行。

  ![border](http://upload-images.jianshu.io/upload_images/599584-15f617d44cdb990d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 一个线程中，事件循环是唯一的 但是任务队列可以是多个。

* 任务队列有分为 macro-task(宏任务) 与 micro-task (微任务) 分别被称为 task 和 job。

* 宏任务指的是 javascript整体代码 （setTimeout、IO、UI rendering）微任务指的是 process.nextTick、promise、Object.observe  **setTimeout作为一个任务分发器，这个函数会立即执行，而它所要分发的任务，也就是它的第一个参数，才是延迟执行**

  ​

* 不同任务源的任务会进入到不同的任务队列 

* 事件循环的顺序，决定了JavaScript代码的执行顺序。它从script(整体代码)开始第一次循环。之后全局上下文进入函数调用栈。直到调用栈清空(只剩全局)，然后执行所有的micro-task。当所有可执行的micro-task执行完毕之后。循环再次从macro-task开始，找到其中一个任务队列执行完毕，然后再执行所有的micro-task，这样一直循环下去。

```javascript
// 为了方便理解，以打印出来的字符作为当前的任务名称
setTimeout(function() {
    console.log('timeout1');
})

new Promise(function(resolve) {
    console.log('promise1');
    for(var i = 0; i < 1000; i++) {
        i == 99 && resolve();
    }
    console.log('promise2');
}).then(function() {
    console.log('then1');
})
console.log('global1');
```

首先，事件循环从宏任务队列开始，这个时候，宏任务队列中，只有一个script(整体代码)任务。每一个任务的执行顺序，都依靠函数调用栈来搞定，而当遇到任务源时，则会先分发任务到对应的队列中去























