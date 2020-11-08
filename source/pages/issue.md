.. sectnum::
   :start: 10

#########################
错误集锦
#########################

一般情况下，命令执行过程中的错误都有详细的描述，如：Node.JS环境下的错误。发生错误不可怕，认真的读提示的错误信息，检查执行命令的正确如否，确保命令在英文环境下执行等，这些基本上可以避免一些常见的粗心错误。人非圣贤，孰能无过，下面例举了培训过程中，一些学员遇到的错误，供读者参考：

lite-server 相关错误
===================================

Unexpected end of JSON input
****************************************

.. code-block:: sh

    C:\Users\JUNBOMA\test1\docs>node -v
    v12.18.2
    C:\Users\JUNBOMA\test1\docs>npm -v
    6.14.5
    C:\Users\JUNBOMA\test1\docs>npm install lite-server -g
    npm WARN deprecated chokidar@2.1.8: Chokidar 2 will break on node v14+. Upgrade to chokidar 3 with 15x less dependencies.
    npm ERR! Unexpected end of JSON input while parsing near '...}},"1.4.0":{"name":"m'
    npm ERR! A complete log of this run can be found in:
    npm ERR!     C:\Users\JUNBOMA\AppData\Roaming\npm-cache\_logs\2020-07-06T06_31_10_878Z-debug.log

 解决方案：

    将本机的Regional换成非日语的（如：English），然后再试试。

旧文件没有删干净
***************************

.. code-block:: sh

    C:\Users\YanYan\H5-Homework3\docs>node -v
    v12.18.1
    C:\Users\YanYan\H5-Homework3\docs>npm -v
    6.14.5
    C:\Users\YanYan\H5-Homework3\docs>npm install lite-server -g
    npm WARN deprecated chokidar@2.1.8: Chokidar 2 will break on node v14+. Upgrade to chokidar 3 with 15x less dependencies.
    npm WARN deprecated fsevents@1.2.13: fsevents 1 will break on node v14+ and could be using insecure binaries. 
    Upgrade to fsevents 2.
    npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated
    npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated
    npm WARN rollback Rolling back bs-recipes@1.3.4 failed (this is probably harmless): EPERM: operation not 
    permitted, scandir 'C:\Users\YanYan\AppData\Roaming\npm\node_modules\lite-server\node_modules'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.2.7 
    (node_modules\lite-server\node_modules\chokidar\node_modules\fsevents):
    npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.13: wanted {"os":"darwin",
    "arch":"any"} (current: {"os":"win32","arch":"x64"})
    npm ERR! code EEXIST
    npm ERR! path C:\Users\YanYan\AppData\Roaming\npm\node_modules\lite-server\bin\lite-server
    npm ERR! dest C:\Users\YanYan\AppData\Roaming\npm\lite-server
    npm ERR! EEXIST: file already exists, cmd shim 'C:\Users\YanYan\AppData\Roaming\npm\node_modules\lite-server\bin\lite-server' -> 
    'C:\Users\YanYan\AppData\Roaming\npm\lite-server'
    npm ERR! File exists: C:\Users\YanYan\AppData\Roaming\npm\lite-server
    npm ERR! Remove the existing file and try again, or run npm
    npm ERR! with --force to overwrite files recklessly.
    npm ERR! A complete log of this run can be found in:
    npm ERR!     C:\Users\YanYan\AppData\Roaming\npm-cache\_logs\2020-07-06T06_40_54_461Z-debug.log
    C:\Users\YanYan\H5-Homework3\docs>lite-server
    internal/modules/cjs/loader.js:969
    throw err;
    ^
    Error: Cannot find module 'C:\Users\YanYan\AppData\Roaming\npm\node_modules\lite-server\bin\lite-server'
    [90m    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:966:15)[39m
    [90m    at Function.Module._load (internal/modules/cjs/loader.js:842:27)[39m
    [90m    at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:71:12)[39m
    [90m    at internal/main/run_main_module.js:17:47[39m {
    code: [32m'MODULE_NOT_FOUND'[39m,
    requireStack: []
    }

 解决方案：

    按照提示，
    npm ERR! File exists: C:\Users\YanYan\AppData\Roaming\npm\lite-server
    npm ERR! Remove the existing file and try again, or run npm # 删除文上面的文件
    然后再试试。


FullyQualifiedErrorId : UnauthorizedAccess
****************************************************

 .. image:: images/lite-server-1.png
    :width: 800px

.. code-block:: sh

 解决方案：

    用管理员权限运行powershell， 执行这个命令就行： Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
    详细参考link：https://go.microsoft.com/fwlink/?LinkId=135170


网页显示不出来
*****************

输入lite-server，命令行这里显示好像是正常的，但是网页显示不出来

.. code-block:: sh

 解决方案：

    原因是：执行命令的目录下，压根就没有网页！因此，需要创建一个index.html文件。

.. admonition:: 统一环境相当于站在了巨人的肩膀上

    为了统一以及消除环境给大伙带来的困惑，Windows用户建议统一使用 `Babun <https://babun.github.io/>`__ 命令窗口，Mac用户默认使用Terminal。