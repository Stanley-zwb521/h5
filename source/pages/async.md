.. sectnum::
   :start: 5

##################################
Javascript异步编程
##################################


同步与异步
^^^^^^^^^^^^^

Javascript语言的执行环境是"单线程"（single thread，就是指一次只能完成一件任务。如果有多个任务，就必须排队，前面一个任务完成，再执行后面一个任务，以此类推）。

这种模式的好处是实现起来比较简单，执行环境相对单纯；坏处是只要有一个任务耗时很长，后面的任务都必须排队等着，会拖延整个程序的执行。常见的浏览器无响应（假死），往往就是因为某一段Javascript代码长时间运行（比如死循环），导致整个页面卡在这个地方，其他任务无法执行。

为了解决这个问题，Javascript语言将任务的执行模式分成两种： 同步（Synchronous） 和  异步（Asynchronous）。

" **同步模式** " 就是上一段的模式，后一个任务等待前一个任务结束，然后再执行，程序的执行顺序与任务的排列顺序是一致的、同步的；" **异步模式** "则完全不同，每一个任务有一个或多个回调函数（callback），前一个任务结束后，不是执行后一个任务，而是执行回调函数，后一个任务则是不等前一个任务结束就执行，所以程序的执行顺序与任务的排列顺序是不一致的、异步的。

"异步模式" 非常重要。在浏览器端，耗时很长的操作都应该异步执行，避免浏览器失去响应，最好的例子就是Ajax操作。在服务器端，"异步模式"甚至是唯一的模式，因为执行环境是单线程的，如果允许同步执行所有http请求，服务器性能会急剧下降，很快就会失去响应。

异步调用并不会阻止代码的顺序执行，而是在将来的某一个时刻触发设置好的逻辑，所以我们

- 并不知道逻辑什么时候会被调用
- 只能定义当触发的时候逻辑是什么
- 只能等待，同时可以去处理其他的逻辑

Javascript异步编程方法
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ES 6以前：

* 回调函数
* 事件监听(事件发布/订阅)
* Promise对象

ES 6：

* Generator函数(协程coroutine)

ES 7:

* async和await

.. note:: ECMAScript 6（以下简称ES6）是JavaScript语言的下一代标准，已经在2015年6月正式发布了。Mozilla公司将在这个标准的基础上，推出JavaScript 2.0。ECMAScript和JavaScript到底是什么关系？很多初学者会感到困惑，简单来说，ECMAScript是JavaScript语言的国际标准，JavaScript是ECMAScript的实现。

回调函数
^^^^^^^^^^^^^^^^^

回调概念
=========

回调是一个函数被作为一个参数传递到另一个函数里，在那个函数执行完后再执行。

假定有两个函数f1和f2，先调用f1，然后调用f2。 

::

	function f1(){
	    console.log("I am f1");
	}
	
	function f2(){
	    console.log("I am f2");
	}
	
	f1();
	f2();

运行结果如下：

::

	I am f1
	I am f2

下面咱们看看代码怎么实现回调。

::

	function f1(callback){
	    console.log("I am f1");
	    callback();  //调用该函数
	}
	 
	function f2(){
	   console.log("I am f2");
	}
	
	f1(f2);
		
f2函数被作为参数传递到f1函数里，在f1函数执行完后，再执行f2。这应该是最简单的回调了，我想大家应该明白回调的释义了吧。

回调函数和异步
==================
相信上面的f1，f2函数的例子我们已经明白，回调并不一定就是异步。他们自己并没有直接关系。
下面我们可以理解下同步回调和异步回调。

**同步回调:**

就是上面的f1 f2函数例子，它们就是同步的回调。

**异步回调:**

因为js是单线程的，但是有很多情况的执行步骤（ajax请求远程数据，IO等）是非常耗时的，如果一直单线程的堵塞下去会导致程序的等待时间过长页面失去响应，影响用户体验了。

假定有三个函数f1, f2和f3.

f1执行很耗时，而f2需要在f1执行完之后执行。
为了不影响f3的执行，我们可以把f2写成f1的回调函数。

::

	//最原始的写法-同步写法 
	f1(); //耗时很长，严重堵塞
	f2(); 
	f3(); //导致f3执行受到影响
	 
	 
	//改进版-异步写法
	function f1(callback){
	　　setTimeout(function () {
	　　　　// f1的任务代码
	　　　　callback();
	　　}, 1000);
	}
	 
	f1(f2); //	 
	f3();


上面的写法是利用 setTimeOut把f1的逻辑包括起来，实现javascript中的异步编程。这样的话，f1异步了，不再堵塞f3的执行。
顺道说下，js是单线程的，这里所谓的异步也是伪异步，并不是开了多线程的异步。它是什么原理呢，其实是任务栈，setTimeOut方法的原理是根据后面的定时时间，过了这个定时时间后，将f1加入任务栈，注意仅仅是加入任务栈，并不是放进去就执行，而是根据任务栈里的任务数量来确定的。

promise对象（promise 模式）
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
#. promise对象是commonJS工作组提出的一种规范，一种模式，目的是为了异步编程提供统一接口。

#. promise是一种模式，promise可以帮忙管理异步方式返回的代码。他讲代码进行封装并添加一个类似于事件处理的管理层。我们可以使用promise来注册代码，这些代码会在在promise成功或者失败后运行。

#. promise完成之后，对应的代码也会执行。我们可以注册任意数量的函数再成功或者失败后运行，也可以在任何时候注册事件处理程序。

#. promise有两种状态：1、等待（pending）；2、完成（settled）。promise会一直处于等待状态，直到它所包装的异步调用返回/超时/结束。

#. 这时候promise状态变成完成。完成状态分成两类：1、解决（resolved）；2、拒绝（rejected）。

#. promise解决（resolved）：意味着顺利结束。promise拒绝（rejected）意味着没有顺利结束。

我们先看一个最简单的Promise例子：生成一个0-2之间的随机数，如果小于1，则等待一段时间后返回成功，否则返回失败：

::

	function test(resolve, reject) {
	    var timeOut = Math.random() * 2;
	    log('set timeout to: ' + timeOut + ' seconds.');
	    setTimeout(function () {
	        if (timeOut < 1) {
	            log('call resolve()...');
	            resolve('200 OK');
	        }
	        else {
	            log('call reject()...');
	            reject('timeout in ' + timeOut + ' seconds.');
	        }
	    }, timeOut * 1000);
	}
	
这个test()函数有两个参数，这两个参数都是函数，如果执行成功，我们将调用resolve('200 OK')，如果执行失败，我们将调用reject('timeout in ' + timeOut + ' seconds.')。可以看出，test()函数只关心自身的逻辑，并不关心具体的resolve和reject将如何处理结果。

有了执行函数，我们就可以用一个Promise对象来执行它，并在将来某个时刻获得成功或失败的结果：

::

	var p1 = new Promise(test);
	var p2 = p1.then(function (result) {
	    console.log('成功：' + result);
	});
	var p3 = p2.catch(function (reason) {
	    console.log('失败：' + reason);
	});

变量p1是一个Promise对象，它负责执行test函数。由于test函数在内部是异步执行的，当test函数执行成功时，我们告诉Promise对象：

::

	// 如果成功，执行这个函数：
	p1.then(function (result) {
	    console.log('成功：' + result);
	});

当test函数执行失败时，我们告诉Promise对象：

::

	p2.catch(function (reason) {
	    console.log('失败：' + reason);
	});
	
Promise对象可以串联起来，所以上述代码可以简化为：

::

	new Promise(test).then(function (result) {
	    console.log('成功：' + result);
	}).catch(function (reason) {
	    console.log('失败：' + reason);
	});

Promise还可以做更多的事情，比如，有若干个异步任务，需要先做任务1，如果成功后再做任务2，任何任务失败则不再继续并执行错误处理函数。

要串行执行这样的异步任务，不用Promise需要写一层一层的嵌套代码。有了Promise，我们只需要简单地写：

::

	job1.then(job2).then(job3).catch(handleError);

其中，job1、job2和job3都是Promise对象。

async和await
^^^^^^^^^^^^^^^^^

#. await后面接一个会return new promise的函数并执行它
#. await只能放在async函数里


**声明async函数的几个方法**

- 普通的函数声明

::

	async function A(){}

- 声明一个函数表达式

::

	let A=async function(){}

- async形式的箭头函数

::

	let A=async ()=>{}

下面我们来看一个例子：

::

	function 摇色子(){
	    return new Promise((resolve, reject)=>{
	        let sino = parseInt(Math.random() * 6 +1)
	        setTimeout(()=>{
	            resolve(sino)
	        },3000)
	    })
	}
	async function test(){
	    let n =await 摇色子()
	    console.log(n)
	}
	test()

上面这段代码async中使await 摇色子()先执行，等到三秒后执行完再把得到的结果赋值给左边的n，也就是说test函数需要三秒钟才执行完成，所以test函数是异步的，因此前面必须写async

**await与async大多数人的误区**

这个误区在一道面试题那篇文章中详细讲解过，但是还是想提一下。
看一段代码:

::

	async function async1(){
	    console.log('async1 start')
	    await async2()
	    console.log('async1 end')
	  }
	async function async2(){
	    console.log('async2')
	}
	async1();
	console.log('i am koala')
	
我想会有一些开发者认为await是把同步变为异步，执行顺序是这样

::

	async1 start
	async2
	async1 end
	i am koala

然而并不是，正确的执行顺序是

::

	async1 start
	async2
	i am koala
	async1 end

解释一下原因：

::

    “async 函数返回一个 Promise 对象，当函数执行的时候，一旦遇到 await 就会先返回，等到触发的异步操作完成，再接着执行函数体内后面的语句。” ——阮一峰ES6

简单的说，先去执行后面的同步任务代码，执行完成后，也就是表达式中的 Promise 解析完成后继续执行 async 函数并返回解决结果。（其实还是本轮循环promise的问题，最后的resolve属于异步，位于本轮循环的末尾。）

