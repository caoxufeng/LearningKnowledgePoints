```JavaScript
 setTimeout(function(){
     console.log('定时器开始啦')
 });
 
 new Promise(function(resolve){
     console.log('马上执行for循环啦');
     for(var i = 0; i < 10000; i++){
         i == 99 && resolve();
     }
 }).then(function(){
     console.log('执行then函数啦')
 });
 
 console.log('代码执行结束');
```



事实上,按照异步和同步的划分方式,并不准确。

而准确的划分方式是:

* macro-task(宏任务)：包括整体代码script，setTimeout，setInterval
* micro-task(微任务)：Promise，process.nextTick



![avatar](https://image-static.segmentfault.com/386/112/386112937-5a5763d9ef823_articlex)


正确的执行顺序:
> 首先执行script下的宏任务,遇到setTimeout,将其放到宏任 务的【队列】里


>遇到 new Promise直接执行,打印 "马上执行for循环啦"


>遇到then方法,是微任务,将其放到微任务的【队列里打印 "代码执行结束"


>本轮宏任务执行完毕,查看本轮的微任务,发现有一个then方法里的函数, 打印"执行then函数啦"


>到此,本轮的event loop 全部完成


>下一轮的循环里,先执行一个宏任务,发现宏任务的【队列】里有一个 setTimeout里的函数,执行打印"定时器开始啦"
