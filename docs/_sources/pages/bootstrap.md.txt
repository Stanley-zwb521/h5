.. sectnum::
   :start: 3

#################
Bootstrap学习
#################

Bootstrap是全球最受欢迎的前端组件库，用于开发响应式布局、移动设备优先的WEB项目。

Bootstrap是一个用于 HTML、CSS 和 JavaScript 开发的开源工具包。它提供了很多功能，帮助开发者快速地开发出产品原型或构建整个App应用。Bootstrap的内容除了组件库外，还有页面布局和公共样式，这些功能针对开发者来讲，可以一站式解决WEB页面开发的实际问题。下面分别介绍下这些内容。

Bootstrap 环境搭建
=========================
Hello, World!模板，详细见：https://code.z01.com/v4/docs/

学习Bootstrap的公共样式
==========================
Bootstrap的公共样式适用与页面中的任何元素，大到页面布局，小到某一个细节元素。
Bootstrap中内置了很多公共样式，这些公共样式其实就是原子样式的合集，方便开发者直接拿来适用。公共样式里面的包含的内容有很多，如：针对元素边框的样式、文字颜色的样式、文本的样式，元素规格的样式等，本书选取其中部分内容做介绍。

学习文本处理的样式
***********************
Bootstrap的文本公共样式主要是处理文本对齐方式、文本溢出换行、字母大小写转换、字体粗细和斜体效果、重置文本颜色和文字装饰等效果的样式。下面介绍其中的几种。

文本的对齐方式
--------------------
关于文本的对齐方式，示例代码如下：

 .. code-block:: html

    <p class="text-justify">这个样式表示将文本重新对齐到组件：Bootstrap是一个用于 HTML、CSS 和 JavaScript
        开发的开源工具包。它提供了很多功能，帮助开发者快速地开发出产品原型或构建整个App应用。
        Bootstrap的内容除了组件库外，还有页面布局和公共样式，这些功能针对开发者来讲，
        可以一站式解决WEB页面开发的实际问题。</p>
    <p class="text-left">在所有视窗尺寸上的左对齐文本。</p>
    <p class="text-center">在所有视窗尺寸上居中对齐文本。</p>
    <p class="text-right">在所有视窗尺寸上的右对齐文本。</p>

    <p class="text-sm-left">在SM（小尺寸）或更宽的视窗上左对齐文字。</p>
    <p class="text-md-left">在MD（中型）或更大尺寸的视窗上左对齐文字。</p>
    <p class="text-lg-left">LG（大）或更宽的视窗上的左对齐文本。</p>
    <p class="text-xl-left">在XL（特大号）或更大尺寸的视窗上的左对齐文本。</p>

文本溢出换行的样式
--------------------

文本长度大于所在的组件宽度时，可以使用溢出换行的样式。示例代码如下：

 .. code-block:: html

    <div class="badge badge-primary text-wrap" style="width: 6rem;">
        这段文本换行的效果
    </div>

上述代码显示的效果如图19-1所示：

  .. image:: images/Figure19-1.png
   :width: 150px

  图19-1 文本换行的样式


字母大小写转换的样式
-----------------------
字母大小写转换的样式可以使英文（不支持中文）文本在大小写之间转换。示例代码如下：

 .. code-block:: html

    <!-- 页面显示：lowercased text. -->
    <p class="text-lowercase">Lowercased text.</p>

    <!-- 页面显示：UPPERCASED TEXT. -->
    <p class="text-uppercase">Uppercased text.</p>

    <!-- 页面显示：CapiTaliZed Text. -->
    <p class="text-capitalize">CapiTaliZed text.</p>

text-capitalize样式的效果是使每个单词的第一个字母转为大写，而其它字母不受影响。

简化Margin与Padding的间距处理
*********************************
Bootstrap中提供了一组缩写CSS的规范，对元素的 margin 或 padding 属性里的单个属性项、所有属性项以及垂直、水平等属性项进行赋值，距离单位是在采用 0.25rem 到 3rem之间的数字。具体的规则如下：

针对不同的屏幕宽度，分为两类表示法。
对于xs屏幕，使用固定格式{property}{sides}-{size} 命名CSS，对于 sm、md、lg、xl 大小的屏幕，使用 {property}{sides}-{breakpoint}-{size}格式命名CSS。

* property的值是“margin”或者“padding”，二选一；规定采用简写的方式：“m”表示“margin”，“p”表示“padding”;
* sides的值表示方向，如：top、bottom、left和right。同样的，规定采用简写的方式：取各个单词的首字母，如果同时表示left和right，用"横向"单词首字母“x”表示，同理，同时表示top和bottom，用"纵向"单词的首字母“y”表示；sides的值也可以不写，留空，表示4个方向；
* size的值范围为数字0到5整数，还可以是“auto”值，表示按浏览器默认值自由展现；
* breakpoint取值为sm、md、lg、xl和xs的一种。

下面通过代码例举说明：

 .. code-block:: html

    <h2>Margin与Padding</h2>
    <p class="ml-3 text-white bg-primary">1、P元素距离左边3个空位置开始</p>
    <p class="ml-1 text-white bg-primary">2、P元素距离左边1个空位置开始</p>
    <p class="mr-3 text-white bg-primary">3、P元素距离右边3个空位置截止</p>
    <p class="mx-auto text-white bg-primary" style="width: 200px;">4、P元素居中</p>

    <div class="mx-auto text-white bg-primary" style="width: 200px;">
        <p class="text-center">5、文字居中</p>
    </div>

运行上述代码后，显示的效果如图19-2所示：

  .. image:: images/Figure19-2.png
   :width: 600px

  图19-2 Margin与Padding


掌握Flex弹性布局
*********************
Flex是Flexible Box的缩写，意为"弹性布局"，用来提供一个更加有效的方式实现响应式布局。任何一个容器都可以指定为Flex布局。

采用Flex布局的元素，称为Flex容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为Flex项目（flex item），简称"项目"。容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。

我们先来了解下一个简单的Flex弹性布局，请看如下的示例代码：

 .. code-block:: html

    <div class="container mt-3">
      <h2>Flex</h2>
      <p>使用 d-flex 类创建一个弹性盒子容器，并设置三个弹性子元素：</p>
      <div class="d-flex p-3 bg-secondary text-white">
          <div class="p-2 bg-info">Flex item 1</div>
          <div class="p-2 bg-warning">Flex item 2</div>
          <div class="p-2 bg-primary">Flex item 3</div>
      </div>
    </div>

上述代码中，父<div>的样式“d-flex”就是我们上面介绍的Flex容器样式，在它下面有3个子<div>标签，它们代表着容器成员，称为Flex子元素。

Flex容器样式的值有两种，一种是“d-flex”，另一种是“d-inline-flex”，俗称“行内 Flex”。

我们将“d-flex”和“d-inline-flex”样式放在一起对比，这样从视觉上可以很容易的区别它们的差异。复制一份上述代码，新的代码中，将Flex容器样式值换成“d-inline-flex”样式，运行上述代码后，显示的效果如图19-3所示：

  .. image:: images/Figure19-3.png
   :width: 600px

  图19-3 Flex容器样式
  
  
可以根据不同的设备，设置Flex布局样式，从而实现页面响应式布局。使用 .d-{breakpoint}-flex 或者 .d-{breakpoint}-inline-flex 格式来表达其CSS样式。其中{breakpoint}代表着设备型号，分别对应sm（小型设备）、md（中型设备），lg（大型设备）和 xl（超大型设备）。

确定了设备后，接着可以在容器上设置样式，来限制容器成员的布局方式，请看如下的示例代码：

 .. code-block:: html

    <div class="container mt-3">
      <h2>水平方向</h2>
      <p>使用 .flex-row 类设置弹性子元素水平显示：</p>
      <div class="d-flex flex-row bg-secondary mb-3">
          <div class="p-2 bg-info">Flex item 1</div>
          <div class="p-2 bg-warning">Flex item 2</div>
          <div class="p-2 bg-primary">Flex item 3</div>
      </div>
      <p>.flex-row-reverse 设置右对齐方向:</p>
      <div class="d-flex flex-row-reverse bg-secondary">
          <div class="p-2 bg-info">Flex item 1</div>
          <div class="p-2 bg-warning">Flex item 2</div>
          <div class="p-2 bg-primary">Flex item 3</div>
      </div>
    </div>

上述代码中，分别使用了 .flex-row 和 .flex-row-reverse 类设置弹性子元素水平显示方式。运行上述代码后，显示的效果如图19-4所示：

  .. image:: images/Figure19-4.png
   :width: 600px

  图19-4 Flex容器样式水平方向对齐方式
  


关于作用在容器上的样式有很多，下面对Flex布局样式的常见值进行归纳，便于读者分辨和理解它们的使用场景。如表19-1所示：

 .. list-table:: 表19-1 Flex布局容器样式一览表
   :widths: 5 10 20

   * - 功能
     - 样式
     - 说明
   * - 弹性容器
     - .d-{breakpoint}-flex
     - 根据不同的屏幕设备创建弹性盒子容器
   * - 
     - .d-{breakpoint}-inline-flex
     - 根据不同的屏幕设备创建行内弹性盒子容器
   * - 水平方向
     - .flex-{breakpoint}-row
     - 根据不同的屏幕设备在水平方向显示弹性子元素
   * - 
     - .flex-{breakpoint}-row-reverse
     - 根据不同的屏幕设备在水平方向显示弹性子元素，且右对齐
   * - 垂直方向
     - .flex-{breakpoint}-column
     - 根据不同的屏幕设备在垂直方向显示弹性子元素
   * - 
     - .flex-{breakpoint}-row-reverse
     - 根据不同的屏幕设备在水平方向显示弹性子元素，且方向相反
   * - 内容排列方式
     - .justify-content-{breakpoint}-start
     - 根据不同屏幕设备在开始位置显示弹性子元素 (左对齐)
   * - 
     - .justify-content-{breakpoint}-end
     - 根据不同屏幕设备在尾部显示弹性子元素 (右对齐)
   * - 
     - .justify-content-{breakpoint}-center
     - 根据不同屏幕设备在容器中显示子元素（居中）
   * - 
     - .justify-content-{breakpoint}-between
     - 根据不同屏幕设备在容器中显示子元素（两端对齐）
   * - 
     - .justify-content-{breakpoint}-around
     - 根据不同屏幕设备在容器中显示子元素（间隔相等对齐）
   * - 等宽
     - .flex-{breakpoint}-fill
     - 根据不同的屏幕设备强制等宽
   * - 包裹
     - .flex-{breakpoint}-nowrap
     - 不同的屏幕设备不设置包裹元素
   * - 
     - .flex-{breakpoint}-wrap
     - 根据不同的屏幕设备设置包裹元素
   * - 
     - .flex-{breakpoint}-wrap-reverse
     - 根据不同的屏幕设备设置扩展反转包裹元素
   * - 元素对齐
     - .align-items-{breakpoint}-start
     - 根据不同屏幕设备，让元素在头部显示在同一行
   * - 
     - .align-items-{breakpoint}-end
     - 根据不同屏幕设备，让元素在尾部显示在同一行
   * - 
     - .align-items-{breakpoint}-center
     - 根据不同屏幕设备，让元素在中间位置显示在同一行
   * - 
     - .align-items-{breakpoint}-baseline
     - 根据不同屏幕设备，让元素在基线上显示在同一行
   * - 
     - .align-items-{breakpoint}-stretch
     - 根据不同屏幕设备，让元素延展高度并显示在同一行


表19-1例举的样式是作用在Flex容器上的，对于它的容器子元素也有对应的样式，请看如下的示例代码：

 .. code-block:: html

    <div class="container mt-3">
      <h2>外边距</h2>
      <p>.mr-auto 类可以设置子元素右外边距为 auto，.ml-auto 类可以设置子元素左外边距为 auto，</p>
      <div class="d-flex mb-3 bg-secondary">
          <div class="p-2 mr-auto bg-info">Flex item 1</div>
          <div class="p-2 bg-warning">Flex item 2</div>
          <div class="p-2 bg-primary">Flex item 3</div>
      </div>
      <div class="d-flex mb-3 bg-secondary">
          <div class="p-2  bg-info">Flex item 1</div>
          <div class="p-2 bg-warning">Flex item 2</div>
          <div class="p-2 ml-auto bg-primary">Flex item 3</div>
      </div>
    </div>

运行上述代码后，显示的效果如图19-5所示：

  .. image:: images/Figure19-5.png
   :width: 600px

  图19-5 Flex容器子元素水平方向对齐方式
  

Flex布局容器子元素样式也有多种，下表19-2汇总常见的子元素样式：

 .. list-table:: 表19-2 Flex布局容器子元素样式一览表
   :widths: 5 10 20

   * - 功能
     - 样式
     - 说明
   * - 扩展
     - .flex-{breakpoint}-grow-0
     - 不同的屏幕设备不设置扩展（默认）
   * - 
     - .flex-{breakpoint}-grow-1
     - 根据不同的屏幕设备设置扩展
   * - 收缩
     - .flex-{breakpoint}-shrink-0
     - 不同的屏幕设备不设置收缩
   * - 
     - .flex-{breakpoint}-shrink-1
     - 根据不同的屏幕设备设置收缩（默认）
   * - 排序
     - .order-1 到 .order-12
     - 设置容器子元素的排序
   * - 外边距
     - .mr-auto
     - 设置容器子元素右外边距为 auto
   * - 
     - .ml-auto
     - 设置容器子元素左外边距为 auto
   * - 对齐
     - .align-self-{breakpoint}-start
     - 根据不同屏幕设备，指定子元素显示在头部
   * - 
     - .align-self-{breakpoint}-end
     - 根据不同屏幕设备，指定子元素显示在尾部
   * - 
     - .align-self-{breakpoint}-center
     - 根据不同屏幕设备，指定子元素显示在居中位置
   * - 
     - .align-self-{breakpoint}-baseline
     - 根据不同屏幕设备，指定子元素显示在基线位置
   * - 
     - .align-self-{breakpoint}-stretch
     - 根据不同屏幕设备，延展子元素显示



.. admonition:: 提示

  父容器可以统一设置子元素的排列方式，子元素也可以单独设置自身的排列方式，如果两者同时设置，以子元素的设置为准。


Flex布局贯穿着Bootstrap布局的方方面面，在Bootstrap中，无论是页面、组件还是具体的元素都使用到了Flex布局。


学习Bootstrap的布局
==========================
如果将Flex布局视为原始的基础，在它之上，Bootstrap专门设计了页面级的Container容器布局和响应式的用于排列组件的栅格系统布局，下面分别介绍它们。

Container容器
********************
Container容器是页面窗口级布局的元素，使用.container或.container-fluid类来定义其样式。默认的.container类样式声明是一个响应式容器，它有固定宽度和最大宽度（max-width）的设置，并支持响应式断点，一般使用它作为整个<div>的最外层容器：

* .container类样式用于声明固定宽度且居中显示的响应式容器；
* .container-fluid类样式用于声明全屏宽度的容器；
* .container-{breakpoint}类样式用于声明根据不同屏幕设备，显示固定的宽度比例的响应式容器。

在前面的示例代码中，我们用到了Container容器，代码示例如下：

 .. code-block:: html

    <div class="container mt-3">
      固定宽度且居中显示的响应式容器
    </div>
    <div class="container-fluid">
      全屏宽度的响应式容器
    </div>
    <div class="container-md">
      支持响应式断点，显示中等屏幕固定的宽度比例的响应式容器
    </div>



响应式栅格系统
********************
Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视区（viewport）尺寸的增加，系统会自动分为最多12列。栅格系统通过一系列的行（row）与列（col）的组合来创建页面布局。通过“行”在水平方向创建一组“列”，“列”作为“行”的直接子元素，“列”可以通过“col-n”或“col-{breakpoint}-n”来设置列宽，其中n为1到12的整数。

列宽布局
-----------
下面来演示响应式栅格系统的列宽布局，请看如下的示例代码：

 .. code-block:: html

    <div class="container mt-3">
        <h2>等宽布局</h2>
        <div class="row">
            <div class="col bg-info">
                1 of 2
            </div>
            <div class="col bg-warning">
                2 of 2
            </div>
        </div>
        <div class="row bg-secondary mt-3">
            <div class="col bg-info">
                1 of 3
            </div>
            <div class="col bg-warning">
                2 of 3
            </div>
            <div class="col bg-primary">
                3 of 3
            </div>
        </div>
        <h2>设置一列宽度</h2>
        <div class="row">
            <div class="col bg-info">
                1 of 3
            </div>
            <div class="col-6 bg-warning">
                2 of 3 (12格中占6格，其它6格另外两列平分)
            </div>
            <div class="col bg-primary">
                3 of 3
            </div>
        </div>
        <div class="row  mt-3">
            <div class="col bg-info">
                1 of 3
            </div>
            <div class="col-5 bg-warning">
                2 of 3 (12格中占5格,其它7格另外两列平分)
            </div>
            <div class="col bg-primary">
                3 of 3
            </div>
        </div>
        <h2>可变列宽度</h2>
        <div class="row justify-content-md-center">
            <div class="col col-sm-2 bg-info">
                1 of 3
            </div>
            <div class="col-sm-auto bg-warning">
                可变宽度内容自由伸张，左右宽度不变
            </div>
            <div class="col col-sm-2 bg-primary">
                3 of 3
            </div>
        </div>
        <div class="row mt-3">
            <div class="col bg-info">
                1 of 3
            </div>
            <div class="col-sm-auto bg-warning">
                可变宽度内容自由伸张,左列宽度变化(右列绑定col-sm-2栅格数)
            </div>
            <div class="col col-sm-2 bg-primary">
                3 of 3
            </div>
        </div>

        <h2>等宽多行</h2>
        <div class="row">
            <div class="col bg-info">col</div>
            <div class="col bg-warning">col</div>
            <div class="w-100"></div>
            <div class="col bg-primary">col</div>
            <div class="col bg-secondary">col</div>
        </div>
    </div>

运行上述代码后，显示的效果如图19-6所示：

  .. image:: images/Figure19-6.png
   :width: 800px

  图19-6 栅格系统的列宽布局



垂直和水平对齐
----------------------
下面来演示响应式栅格系统的垂直和水平对齐布局，请看如下的示例代码：

 .. code-block:: html

    <div class="container mt-3">
        <h2>垂直对齐</h2>
        <div class="row" style="height:10vh">
            <div class="col align-self-start bg-info">
                上边对齐
            </div>
            <div class="col align-self-center bg-warning">
                上下居中对齐
            </div>
            <div class="col align-self-end bg-primary">
                下边对齐
            </div>
        </div>
        <h2>水平对齐</h2>
        <div class="row justify-content-start">
            <div class="col-4 bg-info">
                左对齐
            </div>
            <div class="col-4 bg-warning">
                左对齐
            </div>
        </div>
        <div class="row justify-content-center">
            <div class="col-4 bg-info">
                居中对齐
            </div>
            <div class="col-4 bg-warning">
                居中对齐
            </div>
        </div>
        <div class="row justify-content-end">
            <div class="col-4 bg-info">
                右对齐
            </div>
            <div class="col-4 bg-warning">
                右对齐
            </div>
        </div>
        <div class="row justify-content-around">
            <div class="col-4 bg-info">
                间隔相等对齐
            </div>
            <div class="col-4 bg-warning">
                间隔相等对齐
            </div>
        </div>
        <div class="row justify-content-between">
            <div class="col-4 bg-info">
                两端对齐
            </div>
            <div class="col-4 bg-warning">
                两端对齐
            </div>
        </div>
    </div>

运行上述代码后，显示的效果如图19-7所示：

  .. image:: images/Figure19-7.png
   :width: 600px

  图19-7 栅格系统的垂直和水平对齐

注意上述示例代码中，我们在垂直对齐中，对row的定义了一个高度样式，目的是拉开行的高度，让我们区别垂直上、垂直中和垂直下的布局效果。


[示例 bootstrap-ex100] bootstrap的响应式栅格系统
************************************************************

1. 新建index.html文件，并将其更改为以下内容：

 .. code-block:: HTML
          
  <!doctype html>
  <html lang="en">

  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
      crossorigin="anonymous">

    <title>Bootstrap响应式</title>
  </head>

  <body>
    <div class="container-fluid">
      <h1>水平堆叠</h1>
      <p>调整浏览器窗口的大小以查看效果</p>
      <p>这个例子在小型、中型、大型和超大型设备上演示了“75%/25%”的分割。在超小的设备上，它将堆叠（100%宽度）。</p>
      <div class="container-fluid">
        <div class="row">
          <div class="col-sm-9 col-lg-6 bg-success">col-sm-9</div>
          <div class="col-sm-3 col-lg-6 bg-warning">col-sm-3</div>
        </div>
      </div>
      <br>
      <p>这个例子演示了在小型、中型、大型和超大型设备上33%的分割。在超小的设备上，它将堆叠（100%宽度）。</p>
      <div class="container-fluid">
        <div class="row">
          <div class="col-sm bg-success">col-sm</div>
          <div class="col-sm bg-warning">col-sm</div>
          <div class="col-sm bg-success">col-sm</div>
        </div>
      </div>
    </div>

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js"
      crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"
      crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"
      crossorigin="anonymous"></script>
  </body>

  </html>


2. 用浏览器打开index.html文件，观察页面，显示效果如图3-9所示。

  .. image:: images/Figure3-9.png
   :width: 500px

  图3-9 水平堆叠


在上面的示例bootstrap-ex100中，完成了以下内容：

#. 第一个div元素，分别引用了2个不同的样式：col-sm-9和col-lg-6；
#. 第一个div元素引用了col-sm样式。



学习Bootstrap的组件
==========================

按钮Buttons
***********************

使用 Bootstrap 自定义按钮样式到表单、对话框等操作，并支持多种按钮大小、状态等

.. code-block:: html 

  <button type="button" class="btn btn-primary">Primary</button>
  <button type="button" class="btn btn-secondary">Secondary</button>
  <button type="button" class="btn btn-success">Success</button>
  <button type="button" class="btn btn-danger">Danger</button>
  <button type="button" class="btn btn-warning">Warning</button>
  <button type="button" class="btn btn-info">Info</button>
  <button type="button" class="btn btn-light">Light</button>
  <button type="button" class="btn btn-dark">Dark</button>

  <button type="button" class="btn btn-link">Link</button>

大小
------------------

想要较大或较小的按钮？加入 .btn-lg 或 .btn-sm 来应用尺寸。

.. code-block:: html 

  <button type="button" class="btn btn-primary btn-lg">Large button</button>
  <button type="button" class="btn btn-secondary btn-sm">Small button</button>


启用状态
----------------------------

当启用时，按钮将出现按压（背景较暗、边框较暗、内阴影）。 沒有必要在 <button>添加一个 Class，因为它们使用伪类。但是，如果你需要以动态方式改变状态，则可以使用 .active (并包括 aria-pressed="true" 属性) 应用相同的启用外观。

.. code-block:: html 

  <a href="#" class="btn btn-primary btn-lg active" role="button" aria-pressed="true">Primary link</a>
  <a href="#" class="btn btn-secondary btn-lg active" role="button" aria-pressed="true">Link</a>


停用状态
--------------------

通过将 disabled 布林属性添加到任何 <button> 元素，使按钮看起来处于停用状态。

.. code-block:: html 

  <button type="button" class="btn btn-lg btn-primary" disabled>Primary button</button>
  <button type="button" class="btn btn-secondary btn-lg" disabled>Button</button>


使用 <a> 元素的停用略有不同：

- <a>不支持 disabled 属性，所以你必须添加 .disabled 使它在视觉上看起来被禁用。
- 包括友善的样式行为设计，以禁用<a>按钮上的所有pointer-events 在支持该属性的浏览器中，会看不到禁用的图标。
- 禁用按钮应包含 aria-disabled="true" 属性来向辅助性技术指示元素的状态。

.. code-block:: html 

  <a href="#" class="btn btn-primary btn-lg disabled" tabindex="-1" role="button" aria-disabled="true">Primary link</a>
  <a href="#" class="btn btn-secondary btn-lg disabled" tabindex="-1" role="button" aria-disabled="true">Link</a>


轮播Carousel
********************

用于图片元素、幻灯片或包含文本的轮播元件

包含控制项
---------------------------

加入向前及向后的控制项：

.. code-block:: html 

  <div id="carouselExampleControls" class="carousel slide" data-ride="carousel">
    <div class="carousel-inner">
      <div class="carousel-item active">
        <img src="..." class="d-block w-100" alt="...">
      </div>
      <div class="carousel-item">
        <img src="..." class="d-block w-100" alt="...">
      </div>
      <div class="carousel-item">
        <img src="..." class="d-block w-100" alt="...">
      </div>
    </div>
    <a class="carousel-control-prev" href="#carouselExampleControls" role="button" data-slide="prev">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a class="carousel-control-next" href="#carouselExampleControls" role="button" data-slide="next">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>


包含指示器
-------------------

你还可以将指示器与控制项一起添加到轮播中。

.. code-block:: html 

  <div id="carouselExampleIndicators" class="carousel slide" data-ride="carousel">
    <ol class="carousel-indicators">
      <li data-target="#carouselExampleIndicators" data-slide-to="0" class="active"></li>
      <li data-target="#carouselExampleIndicators" data-slide-to="1"></li>
      <li data-target="#carouselExampleIndicators" data-slide-to="2"></li>
    </ol>
    <div class="carousel-inner">
      <div class="carousel-item active">
        <img src="..." class="d-block w-100" alt="...">
      </div>
      <div class="carousel-item">
        <img src="..." class="d-block w-100" alt="...">
      </div>
      <div class="carousel-item">
        <img src="..." class="d-block w-100" alt="...">
      </div>
    </div>
    <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-slide="prev">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-slide="next">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>

包含字幕
------------------------

在.carousel-item 中使用 .carousel-caption 添加字幕到你的幻灯片。 它们会隐藏在较小的 viewport 上，如下所示，可用的显示工具。 我们最初用.d-none 隐藏它们，并将它们显示在中型的设置上 （使用 .d-md-block）。

.. code-block:: html 

  <div id="carouselExampleCaptions" class="carousel slide" data-ride="carousel">
    <ol class="carousel-indicators">
      <li data-target="#carouselExampleCaptions" data-slide-to="0" class="active"></li>
      <li data-target="#carouselExampleCaptions" data-slide-to="1"></li>
      <li data-target="#carouselExampleCaptions" data-slide-to="2"></li>
    </ol>
    <div class="carousel-inner">
      <div class="carousel-item active">
        <img src="..." class="d-block w-100" alt="...">
        <div class="carousel-caption d-none d-md-block">
          <h5>First slide label</h5>
          <p>Nulla vitae elit libero, a pharetra augue mollis interdum.</p>
        </div>
      </div>
      <div class="carousel-item">
        <img src="..." class="d-block w-100" alt="...">
        <div class="carousel-caption d-none d-md-block">
          <h5>Second slide label</h5>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
        </div>
      </div>
      <div class="carousel-item">
        <img src="..." class="d-block w-100" alt="...">
        <div class="carousel-caption d-none d-md-block">
          <h5>Third slide label</h5>
          <p>Praesent commodo cursus magna, vel scelerisque nisl consectetur.</p>
        </div>
      </div>
    </div>
    <a class="carousel-control-prev" href="#carouselExampleCaptions" role="button" data-slide="prev">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a class="carousel-control-next" href="#carouselExampleCaptions" role="button" data-slide="next">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>


超大屏幕Jumbotron
*******************
这是一个轻量极的、灵活的元件，用于调用对特色内容或信息的额外关注。

.. code-block:: html

  <div class="jumbotron">
    <h1 class="display-4">Hello, world!</h1>
    <p class="lead">This is a simple hero unit, a simple jumbotron-style component for calling extra attention to featured content or information.</p>
    <hr class="my-4">
    <p>It uses utility classes for typography and spacing to space content out within the larger container.</p>
    <a class="btn btn-primary btn-lg" href="#" role="button">Learn more</a>
  </div>

要想让广告屏占满萤幕宽度、不带有圆角，请加 .jumbotron-fluid ，并在裡面添加一个 .container 或 .container-fluid 。

.. code-block:: html

  <div class="jumbotron jumbotron-fluid">
    <div class="container">
      <h1 class="display-4">Fluid jumbotron</h1>
      <p class="lead">This is a modified jumbotron that occupies the entire horizontal space of its parent.</p>
    </div>
  </div>


导航Navs
******************************

基础样式
--------------------------------------

Bootstrap框架中制作导航条主要通过“.nav”样式。默认的“.nav”样式不提供默认的导航样式，必须附加另外一个样式才会有效，比如“nav-tabs”、“nav-pills”之类。

.. code-block:: html

  <ul class="nav">
    <li class="nav-item">
      <a class="nav-link active" href="#">Active</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link</a>
    </li>
    <li class="nav-item">
      <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
    </li>
  </ul>

标签形tab导航
--------------------------------------

标签形导航是通过“nav-tabs”样式来实现。在制作标签形导航时需要在原导航“nav”上追加此类名.

.. code-block:: html

  <ul class="nav nav-tabs">
    <li class="nav-item">
      <a class="nav-link active" href="#">Active</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link</a>
    </li>
    <li class="nav-item">
      <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
    </li>
  </ul>

胶囊形(pills)导航
--------------------------------------

只需要把类名“nav-tabs”换成“nav-pills”即可

.. code-block:: html

  <ul class="nav nav-pills">
    <li class="nav-item">
      <a class="nav-link active" href="#">Active</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link</a>
    </li>
    <li class="nav-item">
      <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
    </li>
  </ul>

自适应导航
--------------------------------------

自适应导航指的是导航占据容器全部宽度，而且菜单项可以像表格的单元格一样自适应宽度。使用class nav-justified实现,需要和“nav-tabs”或者“nav-pills”配合在一起使用。

.. code-block:: html

  <ul class="nav nav-pills nav-justified">
    <li class="nav-item">
      <a class="nav-link active" href="#">Active</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Much longer nav link</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link</a>
    </li>
    <li class="nav-item">
      <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
    </li>
  </ul>

下拉菜单
--------------------------------------

只需要将li当作父容器，使用类名“dropdown”，同时在li中嵌套一个div

.. code-block:: html

  <ul class="nav nav-pills">
    <li class="nav-item">
      <a class="nav-link active" href="#">Active</a>
    </li>
    <li class="nav-item dropdown">
      <a class="nav-link dropdown-toggle" data-toggle="dropdown" href="#" role="button" aria-haspopup="true" aria-expanded="false">Dropdown</a>
      <div class="dropdown-menu">
        <a class="dropdown-item" href="#">Action</a>
        <a class="dropdown-item" href="#">Another action</a>
        <a class="dropdown-item" href="#">Something else here</a>
        <div class="dropdown-divider"></div>
        <a class="dropdown-item" href="#">Separated link</a>
      </div>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Link</a>
    </li>
    <li class="nav-item">
      <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
    </li>
  </ul>

  

导航条Navbar
************************************

- 导航栏需要包装 .navbar 并通过.navbar-expand{-sm|-md|-lg|-xl} 用于响应式折叠和 配色方案 类。.
- 默认情况下，Navbars及其内容是浮动的。 使用 optional containers 限制它们的水平宽度。
- 使用我们的间距和 Flex 工具用于控制导航栏中间距和对齐。
- 默认情况下，导航栏会响应，但你可以轻松修改它们以更改它。 响应行为取决于我们的Collapse JavaScript插件。
- 打印时默认隐藏导航栏。 强制他们通过添加打印 .d-print 在 navbar上。 查看 工具->显示 了解更多。
- 使用 <nav> 元素确保亲和性，或者如果使用更通用的元素，如 <div>，在导览列中添加一个 role="navigation" ，为使用者的辅助技术明确标识为导览区域。

支持的内容
-----------------

Navbars内置了对少数子组件的支持。 根据需要选择以下内容：

- .navbar-brand 适用于你的公司，产品或项目名称
- .navbar-nav 用于全高度和轻量级导航（包括对下拉菜单的支持）。
- .navbar-toggler 用于我们的折叠插件和其他 navigation toggling 行为。
- .form-inline 用于任何表单控制元件和操作。
- .navbar-text 用于垂直居中的文本字串。
- .collapse.navbar-collapse 用于通过父断点对导航栏内容进行分组和隐藏。

.. code-block:: html

  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item active">
          <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Link</a>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
            Dropdown
          </a>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown">
            <a class="dropdown-item" href="#">Action</a>
            <a class="dropdown-item" href="#">Another action</a>
            <div class="dropdown-divider"></div>
            <a class="dropdown-item" href="#">Something else here</a>
          </div>
        </li>
        <li class="nav-item">
          <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
        </li>
      </ul>
      <form class="form-inline my-2 my-lg-0">
        <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
        <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
      </form>
    </div>
  </nav>


品牌
-----------------------

The .navbar-brand 可以应用于大多数元素，但锚点效果最好，因为某些元素可能需要工具类或自定义样式。

.. code-block:: html

  <!-- As a link -->
  <nav class="navbar navbar-light bg-light">
    <a class="navbar-brand" href="#">Navbar</a>
  </nav>

  <!-- As a heading -->
  <nav class="navbar navbar-light bg-light">
    <span class="navbar-brand mb-0 h1">Navbar</span>
  </nav>

增加图片到 .navbar-brand 可能需要自定义样式或工具来正确调整大小。 

.. code-block:: html

  <!-- Image and text -->
  <nav class="navbar navbar-light bg-light">
    <a class="navbar-brand" href="#">
      <img src="/docs/assets/brand/bootstrap-solid.svg" width="30" height="30" class="d-inline-block align-top" alt="">
      Bootstrap
    </a>
  </nav>

导航
--------------------------

导览的链接建立在我们的 .nav 选项上，并使用专属的 Class 并且需要使用 toggler classes 在响应式中作切换。 在导览列中的导览元件，也将佔用更多的水平空间，以保持你的导览列内容安全对齐。

活动状态 - 用 .active - 表示当前页面。可以用于 .nav-link 或 .nav-item。

.. code-block:: html

  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item active">
          <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Features</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Pricing</a>
        </li>
        <li class="nav-item">
          <a class="nav-link disabled" href="#">Disabled</a>
        </li>
      </ul>
    </div>
  </nav>


表单
-----------------------

将各种表单控件和组件放在导航栏中.form-inline。

.. code-block:: html

  <nav class="navbar navbar-light bg-light">
    <a class="navbar-brand">Navbar</a>
    <form class="form-inline">
      <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
      <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
    </form>
  </nav>


配色方案
---------------------

由于主题 class 和。 background-color 工具类 class 的结合，主题化导览列从未如此简单。 从 .navbar-light 用于浅色背景颜色, 或 .navbar-dark 深色背景颜色。 然后，自定义 .bg-* 工具。

.. code-block:: html

  <nav class="navbar navbar-dark bg-dark">
    <!-- Navbar content -->
  </nav>

  <nav class="navbar navbar-dark bg-primary">
    <!-- Navbar content -->
  </nav>

  <nav class="navbar navbar-light" style="background-color: #e3f2fd;">
    <!-- Navbar content -->
  </nav>


图标Icos
*********************

默认情况下，Bootstrap 不包含图标库.

推荐使用
- Font Awesome https://fontawesome.com/

Font Awesome 是一套绝佳的图标字体库和CSS框架。

Font Awesome 字体为您提供可缩放矢量图标,它可以被定制大小、颜色、阴影以及任何可以用CSS的样式。

要使用Font Awesome图标，请在HTML页面的 部分中添加以下行：

1、国内推荐 CDN：

`<link rel="stylesheet" href="https://cdn.staticfile.org/font-awesome/4.7.0/css/font-awesome.css">`

2、海外推荐 CDN

`<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">`

您可以将Font Awesome图标使用在几乎任何地方，只需要使用CSS前缀 fa ，再加上图标名称。 Font Awesome是为使用内联元素而设计的。我们通常更喜欢使用 <i> ，因为它更简洁。 但实际上使用 <span> 才能更加语义化。

https://fontawesome.dashgame.com 获取更多使用技巧.

.. code-block:: html

  <!DOCTYPE html>
    <html>
       <head>
          <title>Bootstrap 模板</title>
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
          <link rel="stylesheet" href="./css/styles.css">
          <!-- 引入 Bootstrap -->
          <link href="https://cdn.staticfile.org/twitter-bootstrap/4.3.1/css/bootstrap.min.css" rel="stylesheet">
          <link rel="stylesheet" href="https://cdn.staticfile.org/font-awesome/4.7.0/css/font-awesome.css">
          <style>
            footer{
            background-color: cadetblue;
            color:#fff;
          }
          </style>
       </head>
       <body>

      <footer class="footer-section" >
        <div class="container ">
                    <div class="row text-center">
                        <div class="col-sm-6 col-md-4 col-lg-4 p-5">
                            <h3>Contact Us</h3>
                            <h4>Our Address and contact Information</h4>
                        </div>
                        <div class="col-sm-6 col-md-4 col-lg-4 p-5">
                                <h3>Connect With us</h3>
                                <a href="#"><i class="fa fa-facebook"></i></a>
                                <a href="#"><i class="fa fa-linkedin"></i></a>
                                <a href="#"><i class="fa fa-twitter"></i></a>
                                <a href="#"><i class="fa fa-google"></i></a>
                                <a href="#"><i class="fa fa-youtube"></i></a>
                                
                        </div>
                        <div class="col-sm-6 col-md-4 col-lg-4 p-5">
                            <a href="#"><i class="fa fa-google"></i></a>
                        </div>
                    </div>
          </div>
        </footer>
          <!-- jQuery (Bootstrap 的 JavaScript 插件需要引入 jQuery) -->
          <script src="https://cdn.staticfile.org/jquery/3.2.1/jquery.min.js"></script>
          <script src="https://cdn.staticfile.org/twitter-bootstrap/4.3.1/js/bootstrap.min.js"></script>
       </body>
    </html>


参考
===========================
- `Bootstrap 中文教程 <https://code.z01.com/v4/docs/>`_
- `Bootstrap 官方教程 <https://getbootstrap.com/docs/4.4/getting-started/introduction>`_

- `Font Awesome 官方教程 <https://fontawesome.dashgame.com>`_
