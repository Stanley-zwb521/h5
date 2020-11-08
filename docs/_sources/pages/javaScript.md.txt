.. sectnum::
   :start: 4

##################################
Javascript基础学习
##################################

HTML中使用Javascript
========================================

JavaScript代码可以直接嵌在网页的任何地方，不过通常我们都把JavaScript代码放到 ``<head>`` 的 ``<script>`` 标签中

- HTML中使用Javascript
  
.. code-block:: html

   <html>
   <head>
   <title>HTML中使用Javascript</title>
   <script>
      alert('Hello, Javascript');
   </script>
   </head>
   <body>
   ...
   </body>
   </html>

- Javascript放在一个单独的.js文件

.. code-block:: html

   <html>
   <head>
   <title>HTML中使用Javascript</title>
   <script src="example1.js"></script>
   <script src="example2.js"></script>
   </head>
   <body>
   ...
   </body>
   </html>



基本概念
====================

变量
********************************************

声明一个变量的语法是在 ``var`` 或 ``let`` 或 ``const`` 关键字之后加上这个变量的名字, 并用 ``=`` 赋值：

三者区别:

- 使用var声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象；或者可以说var声明变量要么是全局的，要么是函数级的，而无法是块级 ``{}`` 的。

.. code-block:: javascript

   var a=1;
   console.log(a);  //1
   console.log(window.a);  //1


   function test(){
   　　var b=2;
   　　function print(){
   　　　　console.log(a,b);
   　　}
      print();
   }
   test();  //1  2
   console.log(b);  //Uncaught ReferenceError: b is not defined


   for(var i=0;i<=10;i++){ 
      var sum=0; 
      sum+=i; 
   } 
   console.log(i);  //11
   console.log(sum);  //10  声明在for循环内部的i和sum，跳出for循环一样可以使用。

- 使用let声明的变量，其作用域为该语句所在的代码块 ``{}`` 内，不存在变量提升；

.. code-block:: javascript

   let a=1;
   console.log(a); //1
   console.log(window.a); //undefined


   function test(){
   　　let b=2;
   　　function print(){
   　　　　console.log(a,b); //1 2
   　　}
      print();
   }
   test(); 
   console.log(b); //Uncaught ReferenceError: b is not defined


   for(let i=0;i<=10;i++){ 
      let sum=0; 
      sum+=i; 
   } 
   console.log(i);  //Uncaught ReferenceError: i is not defined
   console.log(sum); //Uncaught ReferenceError: sum is not defined

- 使用const声明的是常量并且必须再申明时赋值，其作用域为该语句所在的代码块 ``{}`` 内, 在后面出现的代码中不能再修改该常量的值。

.. code-block:: javascript

   if (true) {
      var a = 2;
      const b = 3; // 包含在 if 中的块作用域常量
      a = 3; // 正常 !
      b = 4; // Uncaught TypeError: Assignment to constant variable.
   } 
   console.log( a ); // 3
   console.log( b ); // Uncaught ReferenceError: b is not defined


数据类型
********************************************

- 七种基本数据类型:
  
   - 布尔值（Boolean），有2个值分别是：true 和 false.
  
   - null ， 一个表明 null 值的特殊关键字。 JavaScript 是大小写敏感的，因此 null 与 Null、NULL或变体完全不同。
   
   - undefined ，和 null 一样是一个特殊的关键字，undefined 表示变量未定义时的属性。
   
   - 数字（Number），整数或浮点数，例如： 42 或者 3.14159。
   
   - 任意精度的整数 (BigInt) ，可以安全地存储和操作大整数，甚至可以超过数字的安全整数限制。BigInt是通过在整数末尾附加 n 或调用构造函数来创建的。
   
   - 字符串（String），字符串是一串表示文本值的字符序列，例如："Howdy" 。
   
   - 代表（Symbol） ( 在 ECMAScript 6 中新添加的类型).。一种实例是唯一且不可改变的数据类型。

- 以及对象（Object）。

typeof操作符可以返回变量的类型

.. code-block:: javascript

   // 数值
   typeof 37 === 'number';
   typeof 3.14 === 'number';
   typeof(42) === 'number';
   typeof Math.LN2 === 'number';
   typeof Infinity === 'number';
   typeof NaN === 'number'; // 尽管它是 "Not-A-Number" (非数值) 的缩写
   typeof Number(1) === 'number'; // Number 会尝试把参数解析成数值

   typeof 42n === 'bigint';

   // 字符串
   typeof '' === 'string';
   typeof 'bla' === 'string';
   typeof `template literal` === 'string';
   typeof '1' === 'string'; // 注意内容为数字的字符串仍是字符串
   typeof (typeof 1) === 'string'; // typeof 总是返回一个字符串
   typeof String(1) === 'string'; // String 将任意值转换为字符串，比 toString 更安全

   // 布尔值
   typeof true === 'boolean';
   typeof false === 'boolean';
   typeof Boolean(1) === 'boolean'; // Boolean() 会基于参数是真值还是虚值进行转换
   typeof !!(1) === 'boolean'; // 两次调用 ! (逻辑非) 操作符相当于 Boolean()

   // Symbols
   typeof Symbol() === 'symbol';
   typeof Symbol('foo') === 'symbol';
   typeof Symbol.iterator === 'symbol';

   // Undefined
   typeof undefined === 'undefined';
   typeof declaredButUndefinedVariable === 'undefined';
   typeof undeclaredVariable === 'undefined'; 

   // 对象
   typeof {a: 1} === 'object';

   // 使用 Array.isArray 或者 Object.prototype.toString.call
   // 区分数组和普通对象
   typeof [1, 2, 4] === 'object';

   typeof new Date() === 'object';
   typeof /regex/ === 'object'; 

   // 下面的例子令人迷惑，非常危险，没有用处。避免使用它们。
   typeof new Boolean(true) === 'object';
   typeof new Number(1) === 'object';
   typeof new String('abc') === 'object';

   // 函数
   typeof function() {} === 'function';
   typeof class C {} === 'function'
   typeof Math.sin === 'function';


操作符
********************************************
- <, >, <=, >=, ==, === 
- ++, --, +=, -=
- 三元运算符, ``condition ? exprIfTrue : exprIfFalse`` 表示如果表达式condition的计算结果是true，那么表达式 exprIfTrue 将会被求值否则exprIfFalse 将会被执行
- &&运算是与运算，只有所有都为true，&&运算结果才是true
- ||运算是或运算，只要其中有一个为true，||运算结果就是true
- !运算是非运算，它是一个单目运算符，把true变成false，false变成true
  
.. code-block:: javascript

   var num1 = 2, num2 = 20;
   var num3 = --num1 + num2; // 等于21, --在前, 先执行减法再返回值
   var num4 = num1 + num2; // 等于21

   var num1 = 2, num2 = 20;
   var num3 = num1-- + num2; // 等于22, --在后, 先返回再执行减法
   var num4 = num1 + num2; // 等于21

- =,==,===的区别
  
   ``=`` 是赋值运算符; ``==`` 与 ``=== `` 是比较运算符, 当进行 ``==`` 比较时候：先检查两个操作数数据类型，如果相同， 则进行 ``===`` 比较， 如果不同， 则愿意为你进行一次类型转换， 转换成相同类型后再进行比较， 而 ``===`` 比较时， 如果类型不同，直接就是false.

   .. code-block:: javascript

      var n1= 1, n2 ='1';
      console.log(n1 == n2);//true
      console.log(n1 === n2);//false

      myname = 123456;
      var password;
      var user = null;

      console.log('undefined == null', password == user);//true
      console.log('undefined === null', password === user);//false
      password = 123456;

      console.log('myname == password', myname == password);//true
      console.log('myname === password', myname === password);//true

语句
********************************************

if-else语句
-------------------

当指定条件为真，if 语句会执行一段语句。如果条件为假，则执行另一段语句。

.. code-block:: javascript

   if (cipher_char === from_char) {
      result = result + to_char;
      x++;
   } else {
      result = result + clear_char;
   }

do-while语句
-------------------

do...while 语句创建一个执行指定语句的循环，直到condition值为 false。在执行statement 后检测condition，所以指定的statement至少执行一次。

.. code-block:: javascript

   var result = '';
   var i = 0;
   do {
      i += 1;
      result += i + ' ';
   } while (i < 5);

while语句
-------------------

while 语句可以在某个条件表达式为真的前提下，循环执行指定的一段代码，直到那个表达式不为真时结束循环。

.. code-block:: javascript

   let n = 0;

   while (n < 3) {
      n++;
   }

for语句
-------------------

for 语句用于创建一个循环，它包含了三个可选的表达式，这三个表达式被包围在圆括号之中，使用分号分隔，后跟一个用于在循环中执行的语句（通常是一个块语句）。

.. code-block:: javascript

   let str = "";

   for (let i = 0; i < 9; i++) {
      str = str + i;
   }

for-in语句
-------------------

for...in语句以任意顺序遍历一个对象的除Symbol以外的可枚举属性。

.. code-block:: javascript

   var obj = {a:1, b:2, c:3};
      
   for (var prop in obj) {
      console.log("obj." + prop + " = " + obj[prop]);
   }

for-of语句
-------------------

for...of语句在可迭代对象（包括 Array，Map，Set，String，TypedArray，arguments 对象等等）上创建一个迭代循环，调用自定义迭代钩子，并为每个不同属性的值执行语句

.. code-block:: javascript

   const array1 = ['a', 'b', 'c'];

   for (const element of array1) {
      console.log(element);
   }

continue和break语句
-------------------

continue 声明终止当前循环或标记循环的当前迭代中的语句执行，并在下一次迭代时继续执行循环。
break 语句中止当前循环，switch语句或label 语句，并把程序控制流转到紧接着被中止语句后面的语句。

.. code-block:: javascript

   function testBreak(x) {
   var i = 0;

   while (i < 10) {
      if (i == 5) {
         break;
      }
      
      if (i == 3) {
         continue;
      }
      i += 1;
   }

   return i * x;
   }

switch语句
-------------------

switch 语句评估一个表达式，将表达式的值与case子句匹配，并执行与该情况相关联的语句。

.. code-block:: javascript

   const expr = 'Papayas';
   switch (expr) {
      case 'Oranges':
         console.log('Oranges are $0.59 a pound.');
         break;
      case 'Mangoes':
      case 'Papayas':
         console.log('Mangoes and papayas are $2.79 a pound.');
         // expected output: "Mangoes and papayas are $2.79 a pound."
         break;
      default:
         console.log('Sorry, we are out of ' + expr + '.');
   }

return语句
-------------------

当在函数体中使用return语句时，函数将会停止执行。如果指定一个值，则这个值返回给函数调用者。

.. code-block:: javascript

   function square(x) {
      return x * x;
   }
   var demo = square(3);


函数
=========================================

函数表达式
********************************

function 关键字可以用来在一个表达式中定义一个函数, 后跟一组参数和函数体。

可以使用 Function 构造函数和一个函数声明来定义函数(不推荐)。
下面的例子定义了一个匿名函数并把它赋值给变量x。这个函数返回它参数的平方：

.. code-block:: javascript

   var x = function(y) {
      return y * y;
   };

   var x = function sum(...args) {
      let total = args.reduce((acc, elem) => acc + elem, 0)
      console.log(total);
   };
   sum(1,3);
   sum(1,2,3);


箭头函数表达式
********************************
箭头函数表达式的语法比函数表达式更简洁. 箭头函数表达式更适用于那些本来需要匿名函数的地方，并且它不能用作构造函数。

.. code-block:: javascript

   var func = x => x * x;                  
   // 简写函数 省略return

   var func = (x, y) => { return x + y; }; 
   //常规编写 明确的返回值

递归函数
********************************

在程序中函数直接或间接调用自己

.. code-block:: javascript

   function factorial(n) {
      if (n <= 1)
         return 1;
      return n * factorial(n - 1);
   }
   var newFactorial = factorial; 
   factorial = null; 
   newFactorial(4);  

这段代码会出错, 因为factorial = null的时候, newFactorial函数内部调用factorial的时候, factorial已经不是函数了

- 使用arguments.callee解决这个问题

.. code-block:: javascript

   function factorial(n) {
      if (n <= 1)
         return 1;
      return n * arguments.callee(n - 1);
   }
   var newFactorial = factorial; 
   factorial = null; 
   newFactorial(4);  

- 使用命名函数解决, 函数名称将会（且只会）作为函数体（作用域内）的本地变量

.. code-block:: javascript

  var factorial = function factorial(n) {
      if (n <= 1)
         return 1;
      return n * factorial(n - 1);
   }
   var newFactorial = factorial; 
   factorial = null; 
   newFactorial(4);


函数参数默认值
********************************
检查函数参数是否存在。

.. code-block:: javascript

   function missingArg(){
      throw new Error("required args")
   }

   function square( a= missingArg()){
      console.log(a*a)
   }

   square(10)
   square()

函数表达式
********************************
IIFE（Immediately Invoked Function Expression，立即调用函数表达式）是一个JavaScript函数，一旦被定义，它就会运行。语法定义如下：

.. code-block:: javascript

   (function () {
      statements
   })();


将函数转化成为一个函数表达式，函数表达式立即执行。表达式中的变量不能从其外部访问。

.. code-block:: javascript

   (function () {
      var aName = "Barry";
   })();
   // Variable aName is not accessible from the outside scope
   aName // throws "Uncaught ReferenceError: aName is not defined"

将IIFE赋值给一个变量，存储的是函数的返回值，而不是函数定义本身。

.. code-block:: javascript

   var result = (function () {
      var name = "Barry"; 
      return name; 
   })(); 
   // Immediately creates the output: 
   result; // "Barry"

   // 箭头函数写法
   var a = (()=> aName = "Barry")();

引用类型
=======================================

Object类型
************************************

创建Object实例有多种方法, 

new操作符后跟Object构造函数创建对象
-------------------------------------------

.. code-block:: javascript

   var o = new Object();
   o.name = "Tom";
   o.sayHello= () => console.log("你好,Object");

对象字面量创建对象
------------------------------------------

.. code-block:: javascript

   var user = {
      name: "Tom",
      age: 29,
      sayHello: () => console.log("你好,user")
   };

   var address = {}; 
   address.zip = 123456;

虽然Object 构造函数或对象字面量都可以用来创建单个对象，但这些方式有个明显的缺点：使用同一个接口创建很多对象，会产生大量的重复代码。

构造函数和原型模式创建对象
--------------------------------------

每个函数都有一个prototype（原型）属性，这个属性是一个指针，指向一个对象，
而这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法。如果按照字面意思来理解，那
么prototype 就是通过调用构造函数而创建的那个对象实例的原型对象。使用原型对象的好处是可以
让所有对象实例共享它所包含的属性和方法。换句话说，不必在构造函数中定义对象实例的信息，而是
可以将这些信息直接添加到原型对象中，如下面的例子所示。

.. code-block:: javascript

   //构造函数   
   function Person(firstName,lastName){
      this.firstName = firstName; //new操作符创建一个新对象时,会将构造函数的作用域赋给新对象, 因此this 就指向了这个新对象；
      this.lastName = lastName;    
   }
   //prototype原型
   Person.prototype.hobbies = ['Playing chess','Playing Cricket'];

   Person.prototype.greetPerson = (firstName,lastName) => {
      return 'Hello ,' + firstName + " " + lastName; 
   }

   let person1 = new Person('Madhu','Samala');
   console.log(person1.greetPerson(person1.firstName,person1.lastName));
   let person2 = new Person('Sachin','Groover');
   console.log(person2.hobbies);

class类创建对象
-----------------------------------

.. code-block:: javascript

   class Contact{      
      constructor(id,name,email,contactno){
         this.id = id;
         this.name = name;
         this.email = email;
         this.contactno = contactno;
      }

      getContactInfo(){
         return this.name  + "'s E-mail Id :" + this.email;
      }
   }

   let contact1 = new Contact(1,'StackRoute','info@stackroute.com',34534534);
   contact1.address = 'United States';
   console.log(contact1.getContactInfo());
   console.log(contact1);  

对象属性调用
************************************************

对象属性调用可以通过点 ``.`` 和中括号方式 ``[]``, 比如 ``user.name``, ``user['name']``, 两者的区别如下:

1. 点方法后面的必须是一个指定的属性名称，而中括号方法里面可以是变量。例如

.. code-block:: javascript

   var t = "name";
   obj.t; // 报错
   obj[t]; 
 
2.中括号方法里面的属性名可以是数字，而点方法后面的属性名不可以是数字

3.当动态为对象添加属性时，必须使用中括号[]，不可用点方法


Array类型
************************************************

js中数组的每一项可以保存任何类型的数据。可以用数组的第一个位置来保存字符串，用第二位置来保存数值，用第三个位置来保存对象等等。js中数组的大小是可以动态调整的，即可以随着数据的添加自动增长以容纳新增数据。

创建数组
----------------------------------------------------------------

.. code-block:: javascript

   var names = new Array("Tom", "Jerry");
   var fruits = ["Apple", "Banana"];


通过索引访问数组元素
----------------------------------------------------------------

在读取和设置数组的值时，要使用方括号并提供相应值的基于0的数字索引

.. code-block:: javascript

   var fruits = ["Apple", "Banana"];
   
   var first = fruits[0];
   // Apple, 数组中的第一个元素

   var last = fruits[fruits.length - 1];
   // Banana, 数组中的最后一个元素

遍历数组
----------------------------------------------------------------

``forEach()`` 对数组中的每一项运行给定函数

.. code-block:: javascript

   fruits.forEach(function (item, index, array) {
      console.log(item, index);
   });
   // Apple 0
   // Banana 1


添加元素到数组的末尾
----------------------------------------------------------------

.. code-block:: javascript

   var newLength = fruits.push('Orange');
   // newLength:3; fruits: ["Apple", "Banana", "Orange"]

删除数组末尾的元素
----------------------------------------------------------------

.. code-block:: javascript

   var last = fruits.pop(); // remove Orange (from the end)
   // last: "Orange"; fruits: ["Apple", "Banana"];

删除数组最前面（头部）的元素
----------------------------------------------------------------

.. code-block:: javascript

   var first = fruits.shift(); // remove Apple from the front
   // first: "Apple"; fruits: ["Banana"];

添加元素到数组的头部
----------------------------------------------------------------

.. code-block:: javascript

   var newLength = fruits.unshift('Strawberry') // add to the front
   // ["Strawberry", "Banana"];

找出某个元素在数组中的索引
----------------------------------------------------------------

.. code-block:: javascript

   fruits.push('Mango');
   // ["Strawberry", "Banana", "Mango"]

   var pos = fruits.indexOf('Banana');
   // 1


查找数组中满足提供的测试函数的第一个元素的值
----------------------------------------------------------------

.. code-block:: javascript

   var item = fruits.find(element => element == "Banana");
   //Banana


一个元素是否存在于数组中
----------------------------------------------------------------

.. code-block:: javascript

   console.log(fruits.includes('Banana'));
   //true
   console.log(fruits.includes('Cherry'));
   //false

通过索引删除某个元素
----------------------------------------------------------------

.. code-block:: javascript

   var removedItem = fruits.splice(pos, 1); // this is how to remove an item

   // ["Strawberry", "Mango"]


从一个索引位置删除多个元素
----------------------------------------------------------------

.. code-block:: javascript

   var vegetables = ['Cabbage', 'Turnip', 'Radish', 'Carrot'];
   console.log(vegetables); 
   // ["Cabbage", "Turnip", "Radish", "Carrot"]

   var pos = 1, n = 2;

   var removedItems = vegetables.splice(pos, n);
   // this is how to remove items, n defines the number of items to be removed,
   // from that position(pos) onward to the end of array.

   console.log(vegetables); 
   // ["Cabbage", "Carrot"] (the original array is changed)

   console.log(removedItems); 
   // ["Turnip", "Radish"]

复制一个数组
----------------------------------------------------------------

.. code-block:: javascript

   var shallowCopy = fruits.slice(); // this is how to make a copy 
   // ["Strawberry", "Mango"]

   // 或
   shallowCopy = [...fruits]


合并两个或多个数组
----------------------------------------------------------------

.. code-block:: javascript

   const array1 = ['a', 'b', 'c'];
   const array2 = ['d', 'e', 'f'];
   const array3 = array1.concat(array2);

   console.log(array3);
   // expected output: Array ["a", "b", "c", "d", "e", "f"]


检测数组
----------------------------------------------------------------

``Array.isArray()`` 确定某个值到底是不是数组

.. code-block:: javascript

   // 下面的函数调用都返回 true
   Array.isArray([]);
   Array.isArray([1]);
   Array.isArray(new Array());
   Array.isArray(new Array('a', 'b', 'c', 'd'))
   // 鲜为人知的事实：其实 Array.prototype 也是一个数组。
   Array.isArray(Array.prototype); 

   // 下面的函数调用都返回 false
   Array.isArray();
   Array.isArray({});
   Array.isArray(null);
   Array.isArray(undefined);
   Array.isArray(17);
   Array.isArray('Array');
   Array.isArray(true);
   Array.isArray(false);
   Array.isArray(new Uint8Array(32))
   Array.isArray({ __proto__: Array.prototype });

JSON
========================

JSON 结构
**************************
JSON 是一种纯数据格式, 它只包含属性，没有方法。 JSON 要求有两头的 { } 来使其合法。 与JavaScript 的对象字面量相比，JSON 对象有两个地方不一样。首先，没有声明变量（JSON 中没
有变量的概念）。其次，没有末尾的分号（因为这不是JavaScript 语句，所以不需要分号）。
对象的属性必须加双引号。

.. code-block:: javascript

   {
   "squadName" : "Super hero squad",
   "homeTown" : "Metro City",
   "formed" : 2016,
   "secretBase" : "Super tower",
   "active" : true,
   "members" : [
      {
         "name" : "Molecule Man",
         "age" : 29,
         "secretIdentity" : "Dan Jukes",
         "powers" : [
         "Radiation resistance",
         "Turning tiny",
         "Radiation blast"
         ]
      },
      {
         "name" : "Madame Uppercut",
         "age" : 39,
         "secretIdentity" : "Jane Wilson",
         "powers" : [
         "Million tonne punch",
         "Damage resistance",
         "Superhuman reflexes"
         ]
      },
      {
         "name" : "Eternal Flame",
         "age" : 1000000,
         "secretIdentity" : "Unknown",
         "powers" : [
         "Immortality",
         "Heat Immunity",
         "Inferno",
         "Teleportation",
         "Interdimensional travel"
         ]
      }
   ]
   }

解析
****************

使用JSON对象的 ``stringify()`` 方法可以把JavaScript对象序列化为JSON 字符串。

.. code-block:: javascript

   var myJSON = { "name" : "Chris", "age" : "38" };
   var myString = JSON.stringify(myJSON);

序列化
********************

使用JSON对象的 ``parse()`` 方法可以把JSON字符串解析为原生JavaScript值。

.. code-block:: javascript

   var myString = '{ "name" : "Chris", "age" : "38" }';
   var myJSON = JSON.parse(myJSON);


文档对象模型DOM
=========================

在浏览器标签中当前载入的文档用文档对象模型来表示。这是一个由浏览器生成的“树结构”，使编程语言可以很容易的访问HTML结构 — 例如浏览器自己在呈现页面时，使用它将样式和其他信息应用于正确的元素，而页面呈现完成以后，开发人员可以用JavaScript操作DOM。

DOM树如下所示：

.. image:: ./images/dom-screenshot.png
   :width: 800px

文档中每个元素和文本在树中都有它们自己的入口 — 称之为节点。你将用不同的术语来描述节点的类型和它们相对于其他节点的位置：

- 元素节点: 一个元素，存在于DOM中。

- 根节点: 树中顶层节点，在HTML的情况下，总是一个HTML节点（其他标记词汇，如SVG和定制XML将有不同的根元素）。

- 子节点: 直接位于另一个节点内的节点。例如上面例子中，IMG是SECTION的子节点。

- 后代节点: 位于另一个节点内任意位置的节点。例如 上面例子中，IMG是SECTION的子节点，也是一个后代节点。IMG不是BODY的子节点，因为它在树中低了BODY两级，但它是BODY的后代之一。

- 父节点: 里面有另一个节点的节点。例如上面的例子中BODY是SECTION的父节点。

- 兄弟节点: DOM树中位于同一等级的节点。例如上面例子中，IMG和P是兄弟。

- 文本节点: 包含文字串的节点


查找元素
********************

- querySelector(selectors)

   参数selectors包含一个或多个要匹配的选择器的 DOM字符串DOMString。 该字符串必须是有效的CSS选择器字符串；
   返回文档中与指定的一组CSS选择器匹配的第一个元素的 html元素Element对象。

   这个例子中，会返回当前文档中第一个类名为 "myclass" 的元素：
   
   .. code-block:: javascript

      var el = document.querySelector(".myclass");

   选择器也可以非常强大，如以下示例所示.

   这里, 一个class属性为"user-panel main"的div元素 ``<div>(<div class="user-panel main">)`` 内包含一个name属性为"login"的input元素 ``<input> (<input name="login"/>)`` ，如何选择，如下所示:

   .. code-block:: javascript

      var el = document.querySelector("div.user-panel.main input[name='login']");

- getElementById(id)
  
   参数id是大小写敏感的字符串，代表了所要查找的元素的唯一ID.
   返回一个匹配到 ID 的 DOM Element 对象。
   
   例如 ``<p id="myId">My paragraph</p>``。ID作为参数传递给函数，即 

   .. code-block:: javascript
   
      var elementRef = document.getElementById('myId');

- getElementsByTagName(name)

   参数name 是一个代表元素的名称的字符串。特殊字符 ``"*"`` 代表了所有元素。
   返回页面中包含的所有已知类型元素的数组。
   
   如 ``<p>s``, ``<a>``。元素类型作为参数传递给函数，即
   
   .. code-block:: javascript
   
      var elementRefArray = document.getElementsByTagName('p');



更新元素
********************

- 方法一使用innerHTML

.. code-block:: javascript

   // 获取<p id="p-id">...</p>
   var p = document.getElementById('p-id');
   // 设置文本为abc:
   p.innerHTML = 'ABC'; // <p id="p-id">ABC</p>
   // 设置HTML:
   p.innerHTML = 'ABC <span style="color:red">RED</span> XYZ';
   // <p>...</p>的内部结构已修改

- 方法二使用innerText或textContent

.. code-block:: javascript

   // 获取<p id="p-id">...</p>
   var p = document.getElementById('p-id');
   // 设置文本:
   p.innerText = '<script>alert("Hi")</script>';
   // HTML被自动编码，无法设置一个<script>节点:


创建元素
********************

document.createElement()方法可以创建新元素

.. code-block:: javascript

   var div = document.createElement("div");
   div.id = "myNewDiv";
   div.className = "box";

或者传入完整的元素标签，也可以包含属性

.. code-block:: javascript

   var div = document.createElement("<div id=\"myNewDiv\" class=\"box\"></div >");

要把新元素添加到文档树，可以使用 ``appendChild()``、 ``insertBefore()`` 或 ``replaceChild()`` 方法。下面的代码会把新创建的元素添加到文档的 ``<body>``元素中。 ``document.body.appendChild(div);``

- ``appendChild((Node or DOMString)... nodes)`` 方法将一个节点附加到指定父节点的子节点列表的末尾处。如果将被插入的节点已经存在于当前文档的文档树中，那么 appendChild() 只会将它从原先的位置移动到新的位置（不需要事先移除要移动的节点）。

- ``insertBefore(newNode, referenceNode)`` 方法在参考节点之前插入一个拥有指定父节点的子节点。如果给定的子节点是对文档中现有节点的引用，insertBefore() 会将其从当前位置移动到新位置（在将节点附加到其他节点之前，不需要从其父节点删除该节点）

- ``replaceChild(newChild, oldChild)`` 方法用指定的节点替换当前节点的一个子节点，并返回被替换掉的节点。


删除元素
********************

要删除一个节点，首先要获得该节点本身以及它的父节点，然后，调用父节点的removeChild()把自己删掉：

.. code-block:: javascript

   // 拿到待删除节点:
   var self = document.getElementById('to-be-removed');
   // 拿到父节点:
   var parent = self.parentElement;
   // 删除:
   var removed = parent.removeChild(self);
   removed === self; // true


操作下拉框
********************

.. code-block:: javascript

   //创建下拉框
   var sel = document.createElement("select");
   //创建两个下拉框选项
   var opt1 = document.createElement("option");
   var opt2 = document.createElement("option");

   //设置选项属性
   opt1.value = "1";
   opt1.text = "Option: Value 1";

   opt2.value = "2";
   opt2.text = "Option: Value 2";

   //将选项添加到下拉框
   sel.add(opt1, null);
   sel.add(opt2, null);

   /*
   结果会在页面上生成如下html代码

   <select>
      <option value="1">Option: Value 1</option>
      <option value="2">Option: Value 2</option>
   </select>
   */


操作表格
********************
下面的代码演示如何创建一个表格:

.. code-block:: javascript

   //创建table
   var table = document.createElement("table");
   table.border = 1;
   table.width = "100%";

   //创建tbody
   var tbody = document.createElement("tbody");
   table.appendChild(tbody);

   //创建第一行
   tbody.insertRow(0);
   tbody.rows[0].insertCell(0);
   tbody.rows[0].cells[0].appendChild(document.createTextNode("Cell 1,1"));
   tbody.rows[0].insertCell(1);
   tbody.rows[0].cells[1].appendChild(document.createTextNode("Cell 2,1"));

   //创建第二行
   tbody.insertRow(1);
   tbody.rows[1].insertCell(0);
   tbody.rows[1].cells[0].appendChild(document.createTextNode("Cell 1,2"));
   tbody.rows[1].insertCell(1);
   tbody.rows[1].cells[1].appendChild(document.createTextNode("Cell 2,2"));

   //将表格添加到文档主体中
   document.body.appendChild(table);

事件
===================================

JavaScript与HTML之间的交互是通过事件实现的。事件就是用户或浏览器自身执行的某种动作。诸如 ``click``、``load`` 和 ``mouseover``，都是事件的名字。可以使用侦听器（或处理程序）来预订事件，以便事件发生时执行相应的代码

事件绑定
*************************

为事件指定处理程序的方式有好几种。

- 第一种

某个元素支持的每种事件，都可以使用一个与相应事件处理程序同名的HTML 特性来指定。

.. code-block:: html

   <script type="text/javascript">
      function showMessage(){
         alert("真的点我了");
      }
   </script>

   <input type="button" value="点我" onclick="alert('点我了')" />
   <input type="button" value="再点我 " onclick="showMessage()" />

- 第二种

每个元素（包括window 和document）都有自己的事件处理程序属性，这些属性通常全部小写，
例如 ``onclick``。将这种属性的值设置为一个函数，就可以指定事件处理程序。

.. code-block:: javascript

   var btn = document.getElementById("myBtn");
   btn.onclick = function(){
     alert("点我了");
   };

- 第三种
  
通过方法 ``addEventListener()`` 和 ``removeEventListener()``。所有DOM节点中都包含这两个方法，并且它们都接受3 个参数：要处理的事件名、作为事件处理程序的函数和一个布尔值。最后这个布尔值参数如果是true，表示在捕获阶段调用事件处理程序；如果是false，表示在冒泡阶段调用事件处理程序。要在按钮上为click 事件添加事件处理程序，可以使用下列代码：

.. code-block:: javascript 

   var btn = document.getElementById("myBtn");
   btn.addEventListener("click", function(){
     alert(this.id);
   }, false);


onload事件
*******************************

网页中某些javascript脚本均需要在文档内容加载完成后执行，否则会出现无法获取对象的情况，解决方式可以通过：

- 将js脚本放在网页末尾，可以确保运行脚本时，获取的对象已经加载完毕。

- 通过window.onload来执行脚本代码。

.. code-block:: html

   <!doctype html>
   <html>
   <head>
      <title>onload test</title>
      <script>
         function load() {
            var p = document.getElementById("p-id");
            if(!p){
               console.log("DOM未加载完成, 找不到p");
            }else{
            	console.log("DOM加载完成, 找到了p");
            }
         }

         load();

         const load1 = () => {
            console.log("load event detected!");
            load();
         } 
         window.onload = load1; 
      </script>
   </head>
   <body>
      <p id="p-id">The load event fires when the document has finished loading!</p>
   </body>
   </html>


参考
===========================

- `Mozilla开发者中心 - JavaScript开发文档 <https://getbootstrap.com/docs/4.4/getting-started/introduction>`_

- 金字塔练习参考

.. code-block:: javascript
   :linenos:

   const buildPyramid = (level) => {
      // Write your code here
      let n = level || 1;
      let output = "";
      let display = "";
      for (let i = 0; i < n; i += 1) {
         let space = "";
         for (let s = 0; s < (n - i); s += 1) {
               space += " ";
         }
         for (let j = 1; j <= i + 1; j += 1) {
               output += "*" + " ";
         }

         display += space + output + ' \n';
         output = "";
      }

      return display;
   };


   pyramid = (n = 1) => { //Input or number of rows
      let result = '';
      for (var i = 1; i <= n; i++) {
         var s = "";
         for (var j = 1; j <= n; j++) { ////For every each counter , there are exist n value
               (j >= n + 1 - i && j <= n - 1 + i) ? s += "* " : s += " "; //Check the result
         }
         result += ' ' + s + ' \n';
      }
      return result;
   }

   const buildPyramid = (n = 1) => {
      let result = '';
      for (let i = 1; i <= n; i++) {
         let str = ' '.repeat(n - i + 1);
         let str2 = '* '.repeat(i)
         result += str + str2 + ' \n'
      }
      return result;
   }


   let result = '';
   function p(h, w) {
      w = w || 1;
      if (h === 1) {
            console.log('* '.repeat(w));
            result +=  '* '.repeat(w);
      } else if (h > 1) {
            console.log(' '.repeat(h-1) + '* '.repeat(w));
            result +=  ' '.repeat(h-1) + '* '.repeat(w);
            p(h-1, w+1);
      }
   }

- 编写一个程序，根据给定的键将一个对象数组转换为一个对象。

.. code-block:: javascript
   :linenos:

   const convert = (arr, key) => {
      // Write your code here
      let result = {};
      if (!Array.isArray(arr)) {
            return null;
      }
      arr.forEach(function (arrItem) {
            result[arrItem[key]] = arrItem;
      });
      return result;
   };

- 编写一个程序来扁平化一个给定的n维数组。

.. code-block:: javascript
   :linenos:

   const flatten = (array) => {
      // Write your code here
      if (!Array.isArray(array)) {
            return null;
      }
      return array.reduce(function (memo, el) {
            let items = Array.isArray(el) ? flatten(el) : [el];
            return memo.concat(items);
      }, []);
   };

- 创建一个水果列表，并将其属性（name名称, color颜色, pricePerKg每公斤价格）转换为另一种格式，以便对一个给定的水果名称快速检索其颜色和每公斤价格值。

.. code-block:: javascript
   :linenos:

   const convert = (array, name) => {
      // Write your code here
      let found = array.find(x => x.name === name);
      return { 'color': found.color, 'pricePerKg': found.pricePerKg };
   };