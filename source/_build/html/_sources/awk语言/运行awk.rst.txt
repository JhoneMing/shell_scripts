2 运行awk
===============================

2.1 调用awk
----------------------------------

在前面我们已经提到了awk的调用方法。详细使用如下：

.. code-block:: bash

    gawk [ POSIX or GNU style options ] -f program-file [ -- ] file ...
    gawk [ POSIX or GNU style options ] [ -- ] program-text file ...

2.2 命令行选项
------------------------------------

awk即是一门语言，也是一个命令，是支持命令行的选项的。

-F                  指定字段分隔符
--field-separator   指定字段分隔符，同-F
-f                  指定源awk脚本文件
--file              指定源awk脚本文件，同-f
-v                  设定变量，使用-v var1="test"
--debug             调试awk
-l                  加载扩展
--load              加载扩展，同-l

2.3 通过标准输出流作为awk输入
------------------------------------

使用重定向技术，具体直接看样例把

.. code-block:: bash

    [root@centos74 test]$ cat mail-list 
    Amelia       555-5553     amelia.zodiacusque@gmail.com    F
    Anthony      555-3412     anthony.asserturo@hotmail.com   A
    Becky        555-7685     becky.algebrarum@gmail.com      A
    Bill         555-1675     bill.drowning@hotmail.com       A
    Broderick    555-0542     broderick.aliquotiens@yahoo.com R
    Camilla      555-2912     camilla.infusarum@skynet.be     R
    Fabius       555-1234     fabius.undevicesimus@ucb.edu    F
    Julie        555-6699     julie.perscrutabor@skeeve.com   F
    Martin       555-6480     martin.codicibus@hotmail.com    A
    Samuel       555-3430     samuel.lanceolis@shu.edu        A
    Jean-Paul    555-2127     jeanpaul.campanorum@nyu.edu     R
    [root@centos74 test]$ cat mail-list  | awk '$1 == "Amelia" {print $0}'
    Amelia       555-5553     amelia.zodiacusque@gmail.com    F

2.3 AWK环境变量
------------------------------------

2.3.1 AWKPATH环境变量
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

我这里使用的环境是centos7,机器上带的是gawk。默认的AWKPATH在/usr/share/awk，我们需要修改AWKPATH为`/usr/share/awk`即可

.. code-block:: bash

    [root@centos74 test]$ vim ~/.bash_profile 
    [root@centos74 test]$ cat ~/.bash_profile |grep AWK
    export AWKPATH="/usr/share/awk"

2.3.2 AWKLIBPATH环境变量
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

AWKLIBPATH的修改同上，只需要设定AWKLIBPATH="you_lib"


2.4 awk退出码
------------------------------------

和bash一样， 正确退出是返回0的，错误退出返回其他

2.5 包含其他文件到程序中
-------------------------------------

想在一个awk程序文件中代用另一个文件的程序，需要使用include语句，有点类似c语言的风格的。

.. code-block:: bash

    [root@centos74 test]$ vim test1.awk
    [root@centos74 test]$ rm -rf test1.awk test2.awk
    [root@centos74 test]$ vim test1.awk
    [root@centos74 test]$ cat test1.awk
    BEGIN { 
        print " this is test1.awk"
    }
    [root@centos74 test]$ vim test2.awk
    [root@centos74 test]$ cat test2.awk 
    @include "test1.awk"

    BEGIN { 
        print " this is test2.awk"
    }
    [root@centos74 test]$ gawk -f test2.awk 
    this is test1.awk
    this is test2.awk


