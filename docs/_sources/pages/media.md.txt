.. sectnum::
   :start: 2

#########################
学习自适应网页设计
#########################

起初，在传统的Web开发设计中，网页设计者会将网页设计为固定宽度。这是因为早期电脑显示器种类并不多，分辨率和屏幕比例较为统一 (常见为800x600或者1024x768)。而随着宽屏显示器、各种尺寸的笔记本以及移动智能设备的普及，目前市面中常见的屏幕尺寸大小不一，分辨率多种多样。

所以，在这样的背景下，如何让网站的内容能够自动适应多种屏幕尺寸，在不同的终端设备上都能良好地对网站内容进行重新排版，就成为了一种强烈的需求。这也是自适应页面 (也可以称之为响应式布局) 产生的背景。


关于网页布局的流行设计知识
====================================
响应式网页设计（RWD，Responsive Web Design）和自适应网页设计（AWD，Adaptive Web Design）在现阶段非常流行，它们是网页设计中的两种模式，简称：R+A模式，下面分别对它们进行介绍。

什么是响应式页面设计
***********************
响应式网页（RWD，Responsive Web Design）就是一个网站能够针对多个终端提供不同的显示样式，而不是针对每个终端制作一个特定的版本。
响应式页面就是随着设备属性（如宽高）的变化，网页的布局也随着变化。响应式页面用到的主要技术就是CSS，如：

#. 多使用 max-width、min-width等属性，不硬编码具体的宽度；
#. 使用媒体查询(Media Query)来响应不同屏幕尺寸和分辨率的设备；
#. 多使用流式网格布局。流式布局就是页面元素的宽度按照屏幕进行适配调整。简单来说，就是 HTML 页面中的元素会根据分辨率的不同而变化大小，但位置并不会有任何变化；
#. 多使用相对单位替换绝对单位，如设置宽度可以使用百分值替代px像素值；
#. 使用能够适应比例变化的图片，即图片可伸缩，不固定宽高；

响应式网页带来的优势就是比较灵活，一个页面适应不同终端。从运营和维护的便利性考虑，当网站交互少，功能少，升级不频繁时，建议使用响应式页面设计。如介绍公司的产品，宣传展示之类的网站。

什么是自适应网页设计
**************************
自适应网页（AWD，Adaptive Web Design）是指页面内容自动适应屏幕大小，指的是页面宽度不固定。自适应页面可以是响应式的，也可以不是响应式的。目前，各种新型设备(手机/平板电脑)、平台和浏览器都需要兼容显示WEB应用程序，需要一种设计兼容所有的设备。自适应网页设计应运而生，它提供不同的布局来为不同的设备提供最好的体验，它代表了一种必然的设计趋势。实现自适应一般是采用如下技术：

#. 使用媒体查询(Media Query)技术，但是仅是针对有限的设备进行设计；
#. 用 Javascript 来操作 HTML 内容；
#. 在服务器端操作 HTML 内容（比如为移动端减少内容，为桌面端提供更多内容）。

自适应网页的理念就是针对不同的设备进行一对一的设计，在不同的终端可能会有不一样的代码结构和体验。从页面个性化多功能方面考虑，当网站功能功能复杂、用户交互频繁、用户量较大，自适应网页设计更合适。如电商类网站，WEB桌面端和移动端为了提供较好的用户体验，针对显示的内容会有取舍。


什么是媒体查询
***************
媒体查询是CSS3中引入的一个新特性，它可以使用自定义的“@media”规则，根据一定条件来加载一段特定的CSS样式。
媒体查询可针对不同设备场景使用不同CSS，媒体查询技术的原理：通过匹配不同屏幕设备的特征，让不同特征下的CSS代码生效。

下面示例代码演示媒体查询的用法：

 .. code-block:: HTML

  <!DOCTYPE html>
  <html lang="en">
  <head>
    <title>媒体查询示例</title>
    <style>
      @media (max-width: 50em){
        body {
          background-color: red;
        }
      }
      @media (min-width: 50em) and (max-width: 80em) {
        body {
          background-color: blue;
        }
      }
    </style>
  </head>
  <body></body>
  </html>

在上面的示例中，完成了以下内容：

#. CSS样式“background-color”仅在满足“@media”条件时加载；
#. 当屏幕宽度值达到最大50em时，即小于或者等于50em时，页面背景色设置为红色；
#. 当屏幕宽度值位于50em到80em之间时，页面背景色设置为蓝色；

上面示例中的max-width和min-width称为媒体匹配特征（Media Feature），常见的媒体匹配特征如下表所示：

 .. list-table:: 常见的媒体匹配特征
   :widths: 5 10

   * - 特征名称
     - 说明
   * - max-width
     - 设置屏的最大宽度，表示屏宽小于或等于它的值时生效
   * - min-width
     - 设置屏的最小宽度，表示屏宽大于或等于它的值时生效
   * - width/height
     - 浏览器的宽度和高度
   * - device-width/device-height
     - 移动设备屏幕的宽度和高度
   * - resolution
     - 设备分辨率
   * - orientation（方向）
     - 它有两个值：portrait(纵向)和landscape(横向)

本示例仅是带来读者了解媒体查询。“@media”语法中的“and”称为查询操作符，max-width和min-width的值表示设置屏幕的断点，通过媒体查询的语法，我们可以构造复杂的使用场景。有关媒体查询的详细语法，读者可以自行查阅相关文档。


什么是自适应页面
====================
请移步下列网站，将浏览器窗口宽度自由缩小放大，观察网页内元素布局的变化。

* https://mediaqueri.es/
* https://segmentfault.com/

如何实现网页的自适应效果
==============================

了解媒体查询 (Media Query)
********************************

媒体查询是CSS3中引入的一个新特性，它可以使用自定义的`@media`规则，根据一定条件来加载一段特定的CSS样式。

实例: 如果浏览器宽度小于等于600px，则将屏幕背景色设成浅蓝色。

.. code-block:: html

    @media only screen and (max-width: 600px) {
      body {
        background-color: lightblue;
      }
    }

上面例子中的CSS样式`background-color`仅在满足`@media`条件 (即屏幕宽度小于等于600px) 时加载。

加入viewport元标签
********************************

在移动浏览器中使用viewport元标签控制布局。

.. code-block:: html

    <meta name="viewport" content="width=device-width, initial-scale=1" />

此行代码将网页的默认宽度设置为屏幕设备宽度，且缩放比例为1，也就是将页面设置为100%屏幕宽度。




[示例 media-ex100] 演示使用媒体查询
**************************************

1. 新建index.html文件，并将其更改为以下内容：

 .. code-block:: HTML
          
  <!DOCTYPE html>
  <html lang="en">

  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Viewport</title>
    <style>
      body {
        margin: 0;
      }

      .c1,
      .c2,
      .c3 {
        height: 100vh;
        width: 100vw;
        font-size: 12em;
      }
      .container {
        display: flex;
        flex-wrap: wrap;
      }

      .c1 {
        background-color: red;
      }
      .c2 {
        background-color: yellow;
      }
      .c3 {
        background-color: blue;
      }


      @media (min-width: 600px) {
        .c1 {
          width: 60%;
          order: 2;
        }
        .c2 {
          width: 40%;
          order: 1;
        }
        .c3 {
          order: 3
        }
      }

      @media (min-width: 800px) {
        .c1 {
          width: 60%;
        }
        .c2,
        .c3 {
          width: 20%;
        }
      }
    </style>
  </head>

  <body>
    <div class="container">
      <section class="c1">c1</section>
      <section class="c2">c2</section>
      <section class="c3">c3</section>
    </div>
  </body>

  </html>

2. 用浏览器打开index.html文件，观察页面。

在上面的示例media-ex100中，完成了以下内容：

#. 设置了media的2个不同的尺寸；
#. 样式container里面使用了Flex弹性容器布局（display: flex;），使3个section在同一行中显示。



常见的自适应页面布局模式
==============================

Mostly fluid
********************************

Mostly fluid 模式主要由流动网格组成。在较大和中等屏幕上，它通常保持相同大小，只在更宽的屏幕上调整边距。

在较小屏幕上，流动网格使主内容自动重排，同时各列垂直排列。 此模式的一个主要优点是，在小屏幕和大屏幕之间通常只需要一个视图断点。

.. image:: ./images/mostly-fluid.svg
   :width: 800px

Column drop
********************************

对于全宽度的多列布局，当窗口宽度太窄不能容纳内容时，Column drop 就将各列垂直排列。

最终使所有列都垂直排列。为此布局模式选择视图断点时要依据内容，并随不同设计而改变。

.. image:: ./images/column-drop.svg
   :width: 800px

Layout shifter
********************************

Layout shifter 模式是自适应性最强的模式，在多种屏幕宽度上采用多个断点。

此布局的关键是内容移动的方式，而不是自动重排并放到其他列下面。 由于每个主要视图断点之间的显著差异，其维护更复杂，并且可能涉及元素内的更改，而不只是总体内容布局的更改。

.. image:: ./images/layout-shifter.svg
   :width: 800px

Tiny tweaks
********************************

Tiny tweaks 只对布局进行细微的更改，例如调整字体大小、调整图像大小或对内容进行极其细微的移动。

它在单列布局上表现很好，例如单页面线性网站和文本为主的文章。

.. image:: ./images/tiny-tweaks.svg
   :width: 800px

Off canvas
********************************

Off canvas 模式不是垂直排列内容，而是将不常用的内容（可能是导航或应用的菜单）放在屏幕之外，只在屏幕足够大时才显示。在较小屏幕上，只需点击就能显示内容。

.. image:: ./images/off-canvas.svg
   :width: 800px


参考链接
====================
1. https://www.w3schools.com/css/css_rwd_mediaqueries.asp
2. https://developers.google.com/web/fundamentals/design-and-ux/responsive/patterns?hl=zh-cn


