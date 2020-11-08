.. sectnum::
   :start: 7

##################################
学习如何测试
##################################

mocha
=========================


现在最流行的JavaScript测试框架之一，在浏览器和Node环境都可以使用。

所谓"测试框架"，就是运行测试的工具。通过它，可以为JavaScript应用添加测试，从而保证代码的质量。


课程内容
==========

mocha 安装
***********

.. code-block:: javascript
    
    git clone https://github.com/ruanyf/mocha-demos.git
    cd mocha-demos
    npm install

断言库chai的安装
****************
.. code-block:: javascript

    npm install chai

编写测试脚本
*************
在单元测试前我们需要：一个js文件和一个test.js文件

- add.js

.. code-block:: javascript

    //add.js
    function add(x,y){
        return x+y;
    }
    module.exports = add;

- add.test.js

测试脚本中应包括一个或多个 describe块，每个describe块应该包括一个或多个it块。
describe块称为“测试套件”，表示一组相关的测试，他是一个函数，第一个参数是测试套件的名称（“加法函数的测试”），第二个参数是一个实际执行的函数。
it块称为“测试用例”，表示一个单独的测试，是测试的最小单位。它也是一个函数，第一个参数是测试用例的名称（“1加1应该等于2”），第二个参数是一个实际执行的函数。
执行该测试脚本时使用mocha add.test.js即可。add.test.js为你自己的测试脚本

.. code-block:: javascript

    //add.test.js
    var add = require('./add.js');                    //将待测试文件引入
    var expect = require('chai').expect;              //引入断言库，指定使用它的expect断言风格
    describe("加法函数测试", function() {              //测试套件
        it("1加1应该等于2", function() {               //测试用例
            expect(add(1, 1)).to.be.equal(2);        //断言
        })
    })






 
    
- cd进入测试文件对应文件夹，输入命令 mocha add.test.js
- 执行所有测试脚本
    一般来说，我们的测试脚本都会放在test下，所以mocha命令会执行test文件夹下的测试脚本，但是若test下有子文件夹，子文件夹下存在测试脚本的话，只使用mocha就不能全部执行了。这时需要使用mocha --recursive来执行test文件夹下所有测试脚本。

- 执行某一类测试脚本

    mocha ``test/**/*.js`` 该命令即是执行test下所有文件夹下的.js文件

- 帮助提示

    mocha --h或者mocha --help可以看到所有的参数提示，在使用时可参考使用

- 超时设置
    若运行时间过长，则可以使用-t 重置超时参数。命令为mocha -t 5000 timeout.text.js
    -s或-slow可设置超过该时间执行的部分高亮显示。命令为mocha -t 5000 -s 1000 timeout.test.js

- 生成报表及网页显示
    报表展示：mocha --recursive -R markdown > spec.md
    网页展示：mocha --recursive -R doc >spec.html
