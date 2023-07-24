## 第十一章：Promise与异步编程
Promise的声生命周期<br>
Promise的内部属性[[PromiseState]]被用来表示三种状态：pending、fulfilled、rejected。但是这个属性不会暴露出来，无法检测Promise的状态。<br>
Promise的then方法，接受一个函数作为参数，该函数接受两个参数resolve方法和reject方法。<br>

如果一个对象有then方法，那这个对象我们称之为thenable对象，所有的promise对象都是thenable对象，反之则不是。<br>

每次调用then方法或catch方法都会创建一个新任务（微任务），当Promise被解决时执行。<br>

执行器错误<br>
每个执行器都隐含一个try-catch块，所以错误会被捕获并传入到拒绝处理程序。<br>

全局的Promise拒绝处理<br>
nodejs环境的拒绝处理<br>
在node.js中，处理promise拒绝时会触发process对象上的两个事件：<br>
unhandledRejection：在一个事件循环中，当promise被拒绝时，并且没有提供拒绝处理程序时，触发该事件；<br>
rejectionHandled：在一个事件循环中，当promise被拒绝时，若拒绝处理程序被调用，触发该事件。<br>
设计这些事件时用来识别那些被拒绝却又没被处理过的promise的。<br>
通过事件rejectionHandled和事件unhandledRejection将潜在未处理的拒绝存储为一个列表，等待一段时间后检查列表便能够正确地跟踪潜在的未处理拒绝。<br>

Promise.all()<br>
当所有promise对象返回的都是成功的对象才会执行；<br>

Promise.race()<br>
只要有一个promise被解决返回的promise就被解决，无须等到所有Promise都被完成。<br>