.. sectnum::
   :start: 6

##################################
学习与HTTP交互
##################################

学习本章内容之后，学员能独自完成WEB信息系统的CRUD（增、删、改、查）操作。

课程须知
=========================
1. 了解HTTP协议
2. 对JS的基础知识掌握
3. 掌握JS操作DOM文档对象
4. 熟悉json-server，使用它模拟后端 RESTful API 数据
5. 熟悉fetch方法，使用 fetch 发起HTTP请求


搭建json-server 服务器
=========================
我们在前端开发工作中，不可避免的需要搭建本地web服务器或者模拟后端RestFul服务器，下面我们介绍一款常见的服务器。

json-server 是一个 Node.js 模块，运行 Express 服务器，你可以指定一个 json 文件作为 api 的数据源。
我们使用 json-server 在本地搭建一个JSON服务器，对外提供 RestFull API 服务，前端开发工程师，在无后端的情况下，可以用它来作为后端 API 服务器。 


**1. 全局安装json-server服务器的命令格式如下：**

::

    npm install -g json-server

**2. 具体使用**

1. 新建一个data文件夹，在data文件夹中创建一个db.json的文件::

    {
      "data":[]
    }

2. 启动json-server，使用如下命令::

    cd data
    json-server db.json

3. 控制台输出启动信息::

    \{^_^}/ hi!

    Loading db.json
    Done

    Resources
    http://localhost:3000/data

    Home
    http://localhost:3000

4. 上述信息表明我们的json-server 服务器已经启动成功。接下来可以通过postman及浏览器发送请求，获得相应数据。 如发送GET请求 http://localhost:3000/data

5. 增加数据。发送POST请求 http://localhost:3000/data ，请求数据如下：

  .. code-block:: json
   :linenos:
   
    {
        "username":"docedit.cn",
        "age":3
    }

  返回response 结果:

  .. code-block:: json
   :linenos:
   
    {
        "username": "docedit.cn",
        "age": 3,
        "id": 1
    }


什么是fetch
=================
Fetch API 提供了一个 JavaScript接口，用于访问和操纵HTTP管道的部分，例如请求和响应。它还提供了一个全局 fetch()方法，该方法提供了一种简单，合理的方式来跨网络异步获取资源。（取代传统的XMLHttpRequest的）
这种功能以前是使用 XMLHttpRequest实现的。Fetch提供了一个更好的替代方法，可以很容易地被其他技术使用，例如 Service Workers。
Fetch 还利用到了请求的异步特性——它是基于Promise的。

Fetch 提供了 Request 和 Response对象（以及与网络请求有关的其他内容）的一般定义。
Fetch API 提供了 fetch() 方法，它被定义在 DOM 的 window 对象中，你可以用它来发起对远程资源的请求。
fetch() 方法返回的是一个Promise对象，让你能够对请求的返回结果进行检索。

为什么要用fetch
***************
传统的XMLHttpRequest请求闲的非常的杂乱，而优雅的ajax又不得不额外加载jQuery这个80K左右的框架
那么Fetch API就应势而生，提供了一种新规范，用来取代善不完美的 XMLHttpRequest 对象

- 传统的xhr请求

.. code-block:: javascript
    :linenos:

    var xhr = new XMLHttpRequest();
    xhr.open('GET', url);
    xhr.responseType = 'json';

    xhr.onload = function() {
        console.log(xhr.response);
    };

    xhr.onerror = function() {
        console.log("Oops, error");
    };

    xhr.send();

- fetch()方法示例

.. code-block:: javascript
    :linenos:

    fetch('http://example.com/movies.json')
    .then(function(response) {
        return response.json();
    })
    .then(function(myJson) {
        console.log(myJson);
    })
    .catch(error => console.error(error));


fetch具体使用
**************

通过网络获取一个 JSON 文件并将其打印到控制台。最简单的用法是只提供一个参数用来指明想 fetch() 到的资源路径，然后返回一个包含响应结果的promise（一个 Response 对象）。

当然它只是一个 HTTP 响应，而不是真的JSON。为了获取JSON的内容，我们需要使用 json() 方法

.. code-block:: javascript
    :linenos:

    fetch('http://example.com/movies.json')
    .then(function(response) {
        return response.json();
    })
    .then(function(myJson) {
        console.log(myJson);
    });

将上面的代码封装为一个方法：

.. code-block:: javascript
    :linenos:

    const callRestAPI = async (url, opt = {}) => {
        return await fetch(url, opt).then(resp => {
            if (resp.ok) {
                return resp.json();
            }
            return Promise.reject(new Error('Dummy error from server'));
        });
    };

使用 fetch() 方法提交GET请求：

.. code-block:: javascript
    :linenos:

    const getList = () => callRestAPI(URL).then(resp => {
        list = [...resp];
        return list;
    }).catch(error => {
        return Promise.reject(Error(error.message));
    });

使用 fetch() 方法提交POST请求：

.. code-block:: javascript
    :linenos:

    callRestAPI(URL, {
            method: 'POST',
            headers: {
                'content-type': 'application/json'
            },
            body: JSON.stringify(data)
        }).then(resp => {
            return resp;
        }).catch(error => {
            return Promise.reject(Error(error.message));
        });

从上面的示例代码，我们可以看到：

1. fetch使用的promise对象可以使得我们使用同步的方式写异步函数
2. fetch api是可以结合 async 和 await 来使用的
3. fetch提供了对request和response对象的通用定义



参考
=========================
#. https://github.com/typicode/json-server
#. https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch
