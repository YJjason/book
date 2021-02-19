<!--
 * @Author: Jason_Ma
 * @Date: 2021-02-19 17:28:22
 * @LastEditors: Jason_Ma
 * @LastEditTime: 2021-02-19 17:35:07
 * @FilePath: /gitbook/Chapter4/event_loop_2.md
-->
[事件循环2]
==============
当我们调用一个函数时，它会被添加到称为调用栈的东西中。调用堆栈是JS引擎的一部分，这不是特定于浏览器的。它是一个堆栈，这意味着它是先进先出（例如一堆煎饼）。当一个函数返回一个值时，它会从堆栈中弹出
![](./imgs/gid1.6.gif)

该respond函数返回一个setTimeout函数。在setTimeout由Web API提供给我们：它让我们拖延的任务，而不会阻塞主线程。我们传递给该setTimeout函数的回调函数，箭头函数() => { return 'Hey'}已添加到Web API。同时，该setTimeout函数和response函数从堆栈中弹出，它们都返回了它们的值！
![](./imgs/gif2.1.gif)

在Web API中，计时器运行的时间与我们传递给它的第二个参数1000ms一样长。回调不会立即添加到调用堆栈中，而是会传递到队列中。
![](./imgs/gif3.1.gif)
这可能是一个令人困惑的部分：这并不意味着在1000毫秒后将回调函数添加到调用堆栈中（因此返回一个值）！它只是在1000毫秒后添加到队列中。但这是一个队列，该功能必须等待轮到它！

现在这是我们大家一直在等待的部分……是时候让事件循环执行其唯一的任务了：将队列与调用堆栈连接起来！如果调用堆栈为空，那么如果所有先前调用的函数都返回了它们的值并已从堆栈中弹出，则队列中的第一项将添加到调用堆栈中。在这种情况下，没有其他函数被调用，这意味着当回调函数成为队列中的第一项时，调用堆栈为空。
![](./imgs/gif4.gif)
回调被添加到调用堆栈中，被调用并返回一个值，并从堆栈中弹出。
![](./imgs/gif5.gif)

如果运行以下命令，请尝试找出登录到控制台的内容：
```javascript
const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"), 500);
const baz = () => console.log("Third");

bar();
foo();
baz();
```
![](./imgs/gif14.1.gif)

1. 我们调用bar。bar返回一个setTimeout函数。
2. 我们传递给的回调setTimeout被添加到Web API，该setTimeout函数中，并bar从调用堆栈中弹出。
3. 计时器运行，与此同时，它foo被调用并记录First。foo返回（未定义），baz被调用，并将回调添加到队列中。
4. baz日志Third。事件循环发现baz返回后调用栈为空，然后将回调添加到调用栈。
5. 回调日志Second。