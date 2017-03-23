# How-JavaScript-Timers-Work

国外的一篇关于定时器工作机制的好的总结

链接地址：[http://ejohn.org/blog/how-javascript-timers-work/](http://ejohn.org/blog/how-javascript-timers-work/)

这张图片能更好的说明：

![](http://om4hi8hop.bkt.clouddn.com/17-3-23/30588489-file_1490233257711_10f5c.png)


简单解释来说：
   就是一段代码中有一个10ms之后要执行的setTimeOut函数，有一个鼠标点击执行事件，一个每隔10ms执行的setInterval函数，由于javascript是单线程机制的，一个时间只能执行一段代码，所以像setTimeOut和setInterVal函数这种异步的操作，会先放在队列里，等到前面操作执行结束后，来继续相应执行队列里的操作。

看了文章后，自己对这张图片的理解操作为：

1. 0-10ms内 有个10ms的setTimeOut函数要发生，一个鼠标点击事件，一个每隔10ms执行的setInterval函数

2. 10ms -20ms之间 js选择响应mouse Click事件，并迅速执行，timer函数存放在队列里等待下一个可能的时间被执行，前一个Interval执行完毕，下一个Interval也放在队列里等待下一个可能的时间执行

3. 20ms 要注意：当鼠标单击处理程序正在执行第一个间隔回调时。与定时器一样，它的处理程序被排队以便以后执行。**但是，请注意，当interval再次被触发（当timer处理程序正在执行）此处理程序执行的时间被放弃**。如果在排队，所有的区间回调的一大段代码执行时，结果会是一堆间隙的执行没有延迟，在完成。相反，浏览器往往只是等待，直到没有更多的间隔处理程序排队（在有问题的时间间隔），然后再排队。


4. 30ms时，click回调完成，timer可以响应执行，开始执行，interval此时一直排在队列里等待。

5. 30ms-40ms之间，timer执行中，进程空闲下来将interval代码插入，这并不意味着它会马上执行，只能表示它尽快执行。


6. timer执行完毕，之后一直每隔10ms执行interval。。。

大概就是这样理解吧，更多的可能看原版英文理解的更好...
