
Pipenv & 虚拟环境
=======================

本教程将引导您完成安装和使用 Python 包。

它将向您展示如何安装和使用必要的工具，并就最佳做法做出强烈推荐。请记住，
Python 用于许多不同的目的。准确地说，您希望如何管理依赖项可能会根据
您如何决定发布软件而发生变化。这里提供的指导最直接适用于网络服务
（包括 Web 应用程序）的开发和部署，但也非常适合管理任意项目的开发和测试环境。

.. note:: 本指南是针对 Python 3 编写。但如果您由于某种原因仍然使用 Python 2.7，
  这些指引应该能够正常工作。

确保您已经有了 Python 和 pip
---------------------------------

在您进一步之前，请确保您有 Python，并且可从您的命令行中获得。
您可以通过简单地运行以下命令来检查：

.. code-block:: console

    $ python --version

您应该得到像 ``3.6.2`` 之类的一些输出。如果没有 Python，请从 `python.org`_ 
安装最新的 3.x 版本，或参考本指南的 `安装 Python`_ 一节。

.. Note:: 如果您是新手，您会得到如下错误：
    
    .. code-block:: python

        >>> python
        Traceback (most recent call last):
          File "<stdin>", line 1, in <module>
        NameError: name 'python' is not defined

    这是因为此命令要在 *shell* （也称为 *终端* 或 *控制台*）中运行。有关使用操作系统的
    shell 并和 Python 进行交互的介绍，请参阅面向 Python 新手的 `入门教程`_。

另外，您需要确保 `pip`_ 是可用的。您可以通过运行以下命令来检查：

.. code-block:: console

    $ pip --version

如果您使用 `python.org`_ 或 `Homebrew`_ 的安装程序来安装 Python，您应该已经有 pip 了。
如果您使用的是Linux，并使用操作系统的包管理器进行安装，则可能需要单独
`安装 pip <https://pip.pypa.io/en/stable/installing/>`_。

.. _入门教程: https://opentechschool.github.io/python-beginners/en/getting_started.html#what-is-python-exactly
.. _python.org: https://python.org
.. _pip: https://pypi.org/project/pip/
.. _Homebrew: https://brew.sh
.. _安装 Python: https://docs.python-guide.org/starting/installation/


安装 Pipenv
-----------------

`Pipenv`_ 是 Python 项目的依赖管理器。如果您熟悉 Node.js 的 `npm`_ 或
Ruby 的 `bundler`_，那么它们在思路上与这些工具类似。尽管 `pip`_ 可以安装 Python 包，
但仍推荐使用 Pipenv，因为它是一种更高级的工具，可简化依赖关系管理的常见使用情况。

使用 ``pip`` 来安装 Pipenv：

.. code-block:: console

    $ pip install --user pipenv


.. Note:: 这进行了 `用户安装`_，以防止破坏任何系统范围的包。如果安装后, shell 中没有
    ``pipenv``，则需要将 `用户基础目录`_ 的 二进制文件目录添加到 ``PATH`` 中。
    
    在 Linux 和 macOS 上，您可以通过运行 ``python -m site --user-base`` 找到
    用户基础目录，然后把 ``bin`` 加到目录末尾。比如，上述命令典型地会打印出
    ``~/.local`` （ ``~`` 会扩展为您的家目录的绝对路径），然后将 ``~/.local/bin``
    添加到 ``PATH`` 中。您可以通过 `修改 ~/.profile`_ 永久地设置 ``PATH``。

    在 Windows 上，您通过运行 ``py -m site --user-site`` 找到用户基础目录，然后
    将 ``site-packages`` 替换为 ``Scripts``。比如，上述命令可能返回为
    ``C:\Users\Username\AppData\Roaming\Python36\site-packages``，然后您需要在
    ``PATH`` 中包含 ``C:\Users\Username\AppData\Roaming\Python36\Scripts``。
    您可以在 `控制面板`_ 中永久设置用户的 ``PATH``。您可能需要登出 ``PATH`` 更改才能生效。

.. _Pipenv: https://pipenv.kennethreitz.org/
.. _npm: https://www.npmjs.com/
.. _bundler: http://bundler.io/
.. _用户基础目录: https://docs.python.org/3/library/site.html#site.USER_BASE
.. _用户安装: https://pip.pypa.io/en/stable/user_guide/#user-installs
.. _修改 ~/.profile: https://stackoverflow.com/a/14638025
.. _控制面板: https://msdn.microsoft.com/en-us/library/windows/desktop/bb776899(v=vs.85).aspx

为您的项目安装包
------------------------------------

Pipenv 管理每个项目的依赖关系。要安装软件包时，请更改到您的项目目录（或只是本教程中的
一个空目录）并运行：

.. code-block:: console

    $ cd project_folder
    $ pipenv install requests

Pipenv 将在您的项目目录中安装超赞的 `Requests`_ 库并为您创建一个 `Pipfile`_。
``Pipfile`` 用于跟踪您的项目中需要重新安装的依赖，例如在与他人共享项目时。
您应该得到类似的输出（尽管显示的确切路径会有所不同）：

.. _Pipfile: https://github.com/pypa/pipfile

.. code-block:: text

    Creating a Pipfile for this project...
    Creating a virtualenv for this project...
    Using base prefix '/usr/local/Cellar/python3/3.6.2/Frameworks/Python.framework/Versions/3.6'
    New python executable in ~/.local/share/virtualenvs/tmp-agwWamBd/bin/python3.6
    Also creating executable in ~/.local/share/virtualenvs/tmp-agwWamBd/bin/python
    Installing setuptools, pip, wheel...done.

    Virtualenv location: ~/.local/share/virtualenvs/tmp-agwWamBd
    Installing requests...
    Collecting requests
      Using cached requests-2.18.4-py2.py3-none-any.whl
    Collecting idna<2.7,>=2.5 (from requests)
      Using cached idna-2.6-py2.py3-none-any.whl
    Collecting urllib3<1.23,>=1.21.1 (from requests)
      Using cached urllib3-1.22-py2.py3-none-any.whl
    Collecting chardet<3.1.0,>=3.0.2 (from requests)
      Using cached chardet-3.0.4-py2.py3-none-any.whl
    Collecting certifi>=2017.4.17 (from requests)
      Using cached certifi-2017.7.27.1-py2.py3-none-any.whl
    Installing collected packages: idna, urllib3, chardet, certifi, requests
    Successfully installed certifi-2017.7.27.1 chardet-3.0.4 idna-2.6 requests-2.18.4 urllib3-1.22

    Adding requests to Pipfile's [packages]...
    P.S. You have excellent taste! ✨ 🍰 ✨

.. _Requests: http://docs.python-requests.org/en/master/


使用安装好的包
------------------------

现在安装了 Requests，您可以创建一个简单的 ``main.py`` 文件来使用它：

.. code-block:: python

    import requests

    response = requests.get('https://httpbin.org/ip')

    print('Your IP is {0}'.format(response.json()['origin']))

然后您就可以使用 ``pipenv run`` 运行这段脚本：

.. code-block:: console

    $ pipenv run python main.py

您应该获取到类似的输出：

.. code-block:: text

    Your IP is 8.8.8.8

使用 ``$ pipenv run`` 可确保您的安装包可用于您的脚本。我们还可以生成一个新的 shell，
确保所有命令都可以使用 ``$ pipenv shell`` 访问已安装的包。


下一步
----------

恭喜，您现在知道如何安装和使用Python包了！ ✨ 🍰 ✨



更低层次: virtualenv
=======================

`virtualenv <http://pypi.org/project/virtualenv>`_ 是一个创建隔绝的Python环境的
工具。virtualenv创建一个包含所有必要的可执行文件的文件夹，用来使用Python工程所需的包。

它可以独立使用，代替Pipenv。

通过pip安装virtualenv：

.. code-block:: console

  $ pip install virtualenv

测试您的安装：

.. code-block:: console

   $ virtualenv --version

基本使用
--------------

1. 为一个工程创建一个虚拟环境：

.. code-block:: console

   $ cd project_folder
   $ virtualenv venv

``virtualenv venv`` 将会在当前的目录中创建一个文件夹，包含了Python可执行文件，
以及 ``pip`` 库的一份拷贝，这样就能安装其他包了。虚拟环境的名字（此例中是 ``venv`` ）
可以是任意的；若省略名字将会把文件均放在当前目录。

在任何您运行命令的目录中，这会创建Python的拷贝，并将之放在叫做 :file:`venv` 
的文件中。

您可以选择使用一个Python解释器（比如 ``python2.7`` ）：

.. code-block:: console

   $ virtualenv -p /usr/bin/python2.7 venv

或者使用 ``~/.bashrc`` 的一个环境变量将解释器改为全局性的：

.. code-block:: console

   $ export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python2.7


2. 要开始使用虚拟环境，其需要被激活：

.. code-block:: console

   $ source venv/bin/activate

当前虚拟环境的名字会显示在提示符左侧（比如说 ``(venv)您的电脑:项目目录 用户名$``）
以让您知道它是激活的。从现在起，任何您使用pip安装的包将会放在 ``venv`` 文件夹中，
与全局安装的Python隔绝开。

对于Windows，可以使用步骤1中提到的相同命令来创建虚拟环境。 只是需要稍微不同的命令来激活环境。

假设您在项目目录中：

.. code-block:: console

   C:\Users\SomeUser\project_folder> venv\Scripts\activate

使用 ``pip`` 命令来安装包：

.. code-block:: console

    $ pip install requests


3. 如果您在虚拟环境中暂时完成了工作，则可以停用它：

.. code-block:: console

   $ deactivate

这将会回到系统默认的Python解释器，包括已安装的库也会回到默认的。

要删除一个虚拟环境，只需删除它的文件夹。（要这么做请执行  ``rm -rf venv`` ）

然后一段时间后，您可能会有很多个虚拟环境散落在系统各处，您将有可能忘记它们的名字或者位置。

其他注意事项
--------------

运行带 ``--no-site-packages`` 选项的 ``virtualenv`` 将不会包括全局安装的包。
这可用于保持包列表干净，以防以后需要访问它。（这在 ``virtualenv`` 1.7及之后是默认行为）

为了保持您的环境的一致性，“冷冻住（freeze）”环境包当前的状态是个好主意。要这么做，请运行：

.. code-block:: console

    $ pip freeze > requirements.txt

这将会创建一个 :file:`requirements.txt` 文件，其中包含了当前环境中所有包及
各自的版本的简单列表。您可以使用 ``pip list`` 在不产生requirements文件的情况下，
查看已安装包的列表。这将会使另一个不同的开发者（或者是您，如果您需要重新创建这样的环境）
在以后安装相同版本的相同包变得容易。

.. code-block:: console

    $ pip install -r requirements.txt

这能帮助确保安装、部署和开发者之间的一致性。

最后，记住在源码版本控制中排除掉虚拟环境文件夹，可在ignore的列表中加上它。
（查看 :ref:`版本控制忽略<version_control_ignores>`）

.. _virtualenvwrapper-ref:

virtualenvwrapper
-----------------

`virtualenvwrapper <https://virtualenvwrapper.readthedocs.io/en/latest/index.html>`_ 
提供了一系列命令使得和虚拟环境工作变得愉快许多。它把您所有的虚拟环境都放在一个地方。

安装（确保 **virtualenv** 已经安装了）：

.. code-block:: console

  $ pip install virtualenvwrapper
  $ export WORKON_HOME=~/Envs
  $ source /usr/local/bin/virtualenvwrapper.sh

(`virtualenvwrapper 的完整安装指引 <https://virtualenvwrapper.readthedocs.io/en/latest/install.html>`_.)

对于Windows，您可以使用 `virtualenvwrapper-win <https://github.com/davidmarble/virtualenvwrapper-win/>`_ 。

安装（确保 **virtualenv** 已经安装了）：

.. code-block:: console

  $ pip install virtualenvwrapper-win

在Windows中，WORKON_HOME默认的路径是 %USERPROFILE%\\Envs 。

基本使用
--------------

1. 创建一个虚拟环境：

.. code-block:: console

   $ mkvirtualenv project_folder

这会在 :file:`~/Envs` 中创建 :file:`project_folder` 文件夹。

2. 在虚拟环境上工作：

.. code-block:: console

   $ workon project_folder

或者，您可以创建一个项目，它会创建虚拟环境，并在 ``$WORKON_HOME`` 中创建一个项目目录。
当您使用 ``workon project_folder`` 时，会 ``cd`` 到项目目录中。

.. code-block:: console

   $ mkproject myproject

**virtualenvwrapper** 提供环境名字的tab补全功能。当您有很多环境，
并且很难记住它们的名字时，这就显得很有用。

``workon`` 也能停止您当前所在的环境，所以您可以在环境之间快速的切换。

3. 停止是一样的：

.. code-block:: console

   $ deactivate

4. 删除：

.. code-block:: console

   $ rmvirtualenv project_folder

其他有用的命令
-------------------

``lsvirtualenv``
  列举所有的环境。

``cdvirtualenv``
  导航到当前激活的虚拟环境的目录中，比如说这样您就能够浏览它的 :file:`site-packages` 。

``cdsitepackages``
  和上面的类似，但是是直接进入到 :file:`site-packages` 目录中。

``lssitepackages``
  显示 :file:`site-packages` 目录中的内容。

`virtualenvwrapper 命令的完全列表 <https://virtualenvwrapper.readthedocs.io/en/latest/command_ref.html>`_ 。

virtualenv-burrito
------------------

有了 `virtualenv-burrito <https://github.com/brainsik/virtualenv-burrito>`_ ，
您就能使用单行命令拥有virtualenv + virtualenvwrapper的环境。

direnv
-------
当您 ``cd`` 进入一个包含 :file:`.env` 的目录中，就会 `direnv <https://direnv.net>`_ 
自动激活那个环境。

使用 ``brew`` 在Mac OS X上安装它：

.. code-block:: console

   $ brew install direnv

在Linux上，根据 `direnv.net <https://direnv.net>` 上的指南进行。

Linegame代码规范
=======================
当一位富有经验的Python开发人员（Pythonista）指出某段代码并不 “Pythonic”时，
通常意味着这些代码并没有遵循通用的指导方针，也没有用最佳的（最可读的）方式
来表达意图。


若想要 **linegame项目变得持续** 且可维护，请后续Linegame开发人员在开发过程中遵循如下规范。


Linegame代码的一般要求
-------------------------

明确的代码
--------------

在存在各种黑魔法的Python中，我们提倡最明确和直接的编码方式。

**糟糕**

.. code-block:: python

    def make_linegame(*args):
        x, y = args
        return dict(**locals())

**优雅**

.. code-block:: python

    def make_linegame(x, y):
        return {'x': x, 'y': y}

在上述优雅的代码中，x和y以明确的字典形式返回给调用者。Linegame开发人员在使用
这个函数的时候通过阅读第一和最后一行，能够正确地知道该做什么。而在
糟糕的例子中则没有那么明确。

每行一个声明
~~~~~~~~~~~~~~~~~~~~~~

复合语句（比如说列表推导）因其简洁和表达性受到推崇，但在同一行代码中写
两条独立的语句是糟糕的。

**糟糕**

.. code-block:: python

    print 'one'; print 'two'

    if x == 1: print 'one'

    if <complex comparison> and <other complex comparison>:
        # do something

**优雅**

.. code-block:: python

    print 'one'
    print 'two'

    if x == 1:
        print 'one'

    cond1 = <complex comparison>
    cond2 = <other complex comparison>
    if cond1 and cond2:
        # do something

函数参数
~~~~~~~~~~~~~~~~~~

将参数传递给函数有四种不同的方式：

1. **位置参数** 是强制的，且没有默认值。 它们是最简单的参数形式，而且能被用在
   一些这样的函数参数中：它们是函数意义的完整部分，其顺序是自然的。比如说：对
   函数的使用者而言，记住 ``send(message, recipient)`` 或 ``point(x, y)`` 需要
   两个参数以及它们的参数顺序并不困难。

在这两种情况下，当调用函数的时候可以使用参数名称，也可以改变参数的顺序，比如说
``send(recipient='World', message='Hello')`` 和 ``point(y=2, x=1)``。但和 ``send(
'Hello', 'World')`` 和 ``point(1, 2)`` 比起来，这降低了可读性，而且带来了
不必要的冗长。

2. **关键字参数** 是非强制的，且有默认值。它们经常被用在传递给函数的可选参数中。
   当一个函数有超过两个或三个位置参数时，函数签名会变得难以记忆，使用带有默认参数
   的关键字参数将会带来帮助。比如，一个更完整的 ``send`` 函数可以被定义为
   ``send(message, to, cc=None, bcc=None)``。这里的 ``cc`` 和 ``bcc`` 是可选的，
   当没有传递给它们其他值的时候，它们的值就是None。

Python中有多种方式调用带关键字参数的函数。比如说，我们可以按定义中的参数顺序而无需
明确的命名参数来调用函数，就像 ``send('Hello', 'World', 'Cthulhu', 'God')`` 是将密件
发送给上帝。我们也可以使用命名参数而无需遵循参数顺序来调用函数，就像 
``send('Hello again', 'World', bcc='God', cc='Cthulhu')`` 。如果没有任何强有力的理由
不去遵循最接近函数定义的语法：``send('Hello', 'World', cc='Cthulhu', bcc='God')`` 那么
这两种方式都应该是要极力避免的。

作为附注，请遵循 `YAGNI <http://en.wikipedia.org/wiki/You_ain't_gonna_need_it>`_ 原则。
通常，移除一个用作“以防万一”但却看起来从未使用的可选参数（以及它在函数中的逻辑），比
添加一个所需的新的可选参数和它的逻辑要来的困难。

3. **任意参数列表** 是第三种给函数传参的方式。如果函数的目的通过带有数目可扩展的
   位置参数的签名能够更好的表达，该函数可以被定义成 ``*args`` 的结构。在这个函数体中， 
   ``args`` 是一个元组，它包含所有剩余的位置参数。举个例子， 我们可以用任何容器作为参数去
   调用 ``send(message, *args)`` ，比如 ``send('Hello', 'God', 'Mom', 'Cthulhu')``。
   在此函数体中， ``args`` 相当于 ``('God','Mom', 'Cthulhu')``。

尽管如此，这种结构有一些缺点，使用时应该予以注意。如果一个函数接受的参数列表具有
相同的性质，通常把它定义成一个参数，这个参数是一个列表或者其他任何序列会更清晰。
在这里，如果 ``send`` 参数有多个容器（recipients），将之定义成 ``send(message, recipients)``
会更明确，调用它时就使用 ``send('Hello', ['God', 'Mom', 'Cthulhu'])``。这样的话，
函数的使用者可以事先将容器列表维护成列表（list）形式，这为传递各种不能被转变成
其他序列的序列（包括迭代器）带来了可能。


4. **任意关键字参数字典** 是最后一种给函数传参的方式。如果函数要求一系列待定的
   命名参数，我们可以使用 ``**kwargs`` 的结构。在函数体中， ``kwargs`` 是一个
   字典，它包含所有传递给函数但没有被其他关键字参数捕捉的命名参数。

和 *任意参数列表* 中所需注意的一样，相似的原因是：这些强大的技术是用在被证明确实
需要用到它们的时候，它们不应该被用在能用更简单和更明确的结构，来足够表达函数意图
的情况中。

编写函数的时候采用何种参数形式，是用位置参数，还是可选关键字参数，是否使用形如任意参数
的高级技术，这些都由程序员自己决定。如果能明智地遵循上述建议，就可能且非常享受地写出
这样的Python函数：

* 易读（名字和参数无需解释）

* 易改（添加新的关键字参数不会破坏代码的其他部分）

避免魔法方法
~~~~~~~~~~~~~~~~~~~~~~

Python对高手来说是一个强有力的工具，它拥有非常丰富的钩子（hook）和工具，允许
您施展几乎任何形式的技巧。比如说，它能够做以下每件事：


* 改变对象创建和实例化的方式

* 改变Python解释器导入模块的方式

* 甚至可能（如果需要的话也是被推荐的）在Python中嵌入C程序

尽管如此，所有的这些选择都有许多缺点。使用更加直接的方式来达成目标通常是更好的
方法。它们最主要的缺点是可读性不高。许多代码分析工具，比如说 pylint 或者 
pyflakes，将无法解析这种“魔法”代码。

我们认为Linegame的开发人员应该知道这些近乎无限的可能性，因为它为我们灌输了没有不可能
完成的任务的信心。然而，知道如何，尤其是何时 **不能** 使用它们是非常重要的。

就像一位功夫大师，一个Pythonista知道如何用一个手指杀死对方，但从不会那么去做。

返回值
~~~~~~~~~~~~~~~~

当一个函数变得复杂，在函数体中使用多返回值的语句并不少见。然而，为了保持函数
的明确意图以及一个可持续的可读水平，更建议在函数体中避免使用返回多个有意义的值。

在函数中返回结果主要有两种情况：函数正常运行并返回它的结果，以及错误的情况，要么
因为一个错误的输入参数，要么因为其他导致函数无法完成计算或任务的原因。

如果您在面对第二种情况时不想抛出异常，返回一个值（比如说None或False）来表明
函数无法正确运行，可能是需要的。在这种情况下，越早返回所发现的不正确上下文越好。
这将帮助扁平化函数的结构：在“因为错误而返回”的语句后的所有代码能够假定条件满足
接下来的函数主要结果的运算。有多个这样的返回结果通常是需要的。

尽管如此，当一个函数在其正常过程中有多个主要出口点时，它会变得难以调试和返回其
结果，所以保持单个出口点可能会更好。这也将有助于提取某些代码路径，而且多个出口点
很有可能意味着这里需要重构。

.. code-block:: python

   def complex_linegame_function(a, b, c):
       if not a:
           return None  # 抛出一个异常可能会更好
       if not b:
           return None  # 抛出一个异常可能会更好
       
       # 一些复杂的代码试着用a,b,c来计算x 
       # 如果成功了，抵制住返回x的诱惑
       if not x:
           # 一些关于x的计算的Plan-B
       return x  # 返回值x只有一个出口点有利于维护代码


习语（Idiom）
------------

编程习语，说得简单些，就是写代码的 *方式*。编程习语的概念在 `c2 <http://c2.
com/cgi/wiki?ProgrammingIdiom>`_ 和 `Stack Overflow <http://stackoverflow.
com/questions/302459/what-is-a-programming-idiom>`_ 上有充足的讨论。

采用习语的Python代码通常被称为 *Pythonic*。

尽管通常有一种 --- 而且最好只有一种 --- 明显的方式去写得Pythonic；对Linegame开发者来说，写出习语式的Python代码的 *方式* 并不明显。所以，好的习语必须
有意识地获取。

如下有一些常见的Python习语：

.. _unpacking-ref:

解包（Unpacking）
~~~~~~~~~~~~~~~~~~~~~~~~~~~

如果您知道一个列表或者元组的长度，您可以将其解包并为它的元素取名。比如，
``enumerate()`` 会对list中的每个项提供包含两个元素的元组：

.. code-block:: python

    for index, item in enumerate(some_list):
        # 使用index和item做一些工作

您也能通过这种方式交换变量：

.. code-block:: python

    a, b = b, a

嵌套解包也能工作：

.. code-block:: python

   a, (b, c) = 1, (2, 3)

在Python 3中，扩展解包的新方法在 :pep:`3132` 有介绍：

.. code-block:: python

   a, *rest = [1, 2, 3]
   # a = 1, rest = [2, 3]
   a, *middle, c = [1, 2, 3, 4]
   # a = 1, middle = [2, 3], c = 4

创建一个被忽略的变量
~~~~~~~~~~~~~~~~~~~~~~~~~~

如果您需要赋值但不需要这个变量，请使用
``__``:

.. code-block:: python

    filename = 'linegame.txt'
    basename, __, ext = filename.rpartition('.')

.. note::

   许多Python风格指南建议使用单下划线的 "``_``" 而不是这里推荐的双下划线 "``__``" 来
   指示废弃变量。问题是， "``_``" 常用在作为私有函数的别名，也被用在交互式命令行中记录最后一次操作的值。相反，使用双下划线
   十分清晰和方便，而且能够消除使用其他这些用例所带来的意外干扰的风险。

创建一个含N个对象的列表
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

使用Python列表中的 ``*`` 操作符：

.. code-block:: python

    four_nones = [None] * 4

创建一个含N个列表的列表
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

因为列表是可变的，所以 ``*`` 操作符（如上）将会创建一个包含N个且指向 *同一个* 
列表的列表，这可能不是您想用的。取而代之，请使用列表解析：

.. code-block:: python

    four_lists = [[] for __ in xrange(4)]

注意：在 Python 3 中使用 range() 而不是 xrange()

根据列表来创建字符串
~~~~~~~~~~~~~~~~~~~~~~~~~~~

创建字符串的一个常见习语是在空的字符串上使用 `str.join` 。

.. code-block:: python

    letters = ['s', 'p', 'a', 'm']
    word = ''.join(letters)

这会将 *word* 变量赋值为 'spam'。这个习语可以用在列表和元组中。

在集合体（collection）中查找一个项
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

有时我们需要在集合体中查找。让我们看看这两个选择：列表和集合（set）。

用如下代码举个例子：

.. code-block:: python

    s = set(['s', 'p', 'a', 'm'])
    l = ['s', 'p', 'a', 'm']

    def lookup_set(s):
        return 's' in s

    def lookup_list(l):
        return 's' in l

即使两个函数看起来完全一样，但因为 *查找集合* 是利用了Python中的集合是可哈希的
特性，两者的查询性能是非常不同的。为了判断一个项是否在列表中，Python将会查看
每个项直到它找到匹配的项。这是耗时的，尤其是对长列表而言。另一方面，在集合中，
项的哈希值将会告诉Python在集合的哪里去查找匹配的项。结果是，即使集合很大，查询
的速度也很快。在字典中查询也是同样的原理。想了解更多内容，请见
`StackOverflow <https://stackoverflow.com/questions/513882/python-list-vs-dict-for-look-up-table>`_ 。想了解在每种数据结构上的多种常见操作的花费时间的详细内容，
请见 `此页面 <https://wiki.python.org/moin/TimeComplexity?>`_。

因为这些性能上的差异，在下列场合在使用集合或者字典而不是列表，通常会是个好主意：

* 集合体中包含大量的项

* 您将在集合体中重复地查找项

* 您没有重复的项

对于小的集合体，或者您不会频繁查找的集合体，建立哈希带来的额外时间和内存的
开销经常会大过改进搜索速度所节省的时间。



Python之禅
-------------

又名 :pep:`20`, Python设计的指导原则。

.. code-block:: pycon

    >>> import this
    The Zen of Python, by Tim Peters

    Beautiful is better than ugly.
    Explicit is better than implicit.
    Simple is better than complex.
    Complex is better than complicated.
    Flat is better than nested.
    Sparse is better than dense.
    Readability counts.
    Special cases aren't special enough to break the rules.
    Although practicality beats purity.
    Errors should never pass silently.
    Unless explicitly silenced.
    In the face of ambiguity, refuse the temptation to guess.
    There should be one-- and preferably only one --obvious way to do it.
    Although that way may not be obvious at first unless you're Dutch.
    Now is better than never.
    Although never is often better than *right* now.
    If the implementation is hard to explain, it's a bad idea.
    If the implementation is easy to explain, it may be a good idea.
    Namespaces are one honking great idea -- let's do more of those!

    Python之禅 by Tim Peters
 
    优美胜于丑陋（Python以编写优美的代码为目标）
    明了胜于晦涩（优美的代码应当是明了的，命名规范，风格相似）
    简洁胜于复杂（优美的代码应当是简洁的，不要有复杂的内部实现）
    复杂胜于凌乱（如果复杂不可避免，那代码间也不能有难懂的关系，要保持接口简洁）
    扁平胜于嵌套（优美的代码应当是扁平的，不能有太多的嵌套）
    间隔胜于紧凑（优美的代码有适当的间隔，不要奢望一行代码解决问题）
    可读性很重要（优美的代码是可读的）
    即便假借特例的实用性之名，也不可违背这些规则（这些规则至高无上）
    不要包容所有错误，除非您确定需要这样做（精准地捕获异常，不写 except:pass 风格的代码）
    当存在多种可能，不要尝试去猜测
    而是尽量找一种，最好是唯一一种明显的解决方案（如果不确定，就用穷举法）
    虽然这并不容易，因为您不是 Python 之父（这里的 Dutch 是指 Guido ）
    做也许好过不做，但不假思索就动手还不如不做（动手之前要细思量）
    如果您无法向人描述您的方案，那肯定不是一个好方案；反之亦然（方案测评标准）
    命名空间是一种绝妙的理念，我们应当多加利用（倡导与号召）

想要了解一些Python优雅风格的例子，请见 `这些来自于Python用户的幻灯片 
<https://github.com/hblanks/zen-of-python-by-example>`_.




PEP 8
--------

:pep:`8` 是Python事实上的代码风格指南，我们可以在 `pep8.org <http://pep8.org/>`_
上获得高质量的、易读的PEP 8版本。

强烈推荐阅读这部分。整个Python社区都尽力遵循本文档中规定的准则。一些项目可能受其影响，
而其他项目可能 `修改其建议 <http://docs.python-equests.org/en/master/dev/contributing/kenneth-reitz-s-code-style>`_。

也就是说，让您的 Python 代码遵循 PEP 8 通常是个好主意，这也有助于在与其他开发人员
一起工作时使代码更加具有可持续性。命令行程序 pycodestyle `<https://github.com/PyCQA/pycodestyle>`_ 
（以前叫做``pep8``），可以检查代码一致性。在您的终端上运行以下命令来安装它：

.. code-block:: console

    $ pip install pycodestyle

然后，对一个文件或者一系列的文件运行它，来获得任何违规行为的报告。

.. code-block:: console

    $ pycodestyle optparse.py
    optparse.py:69:11: E401 multiple imports on one line
    optparse.py:77:1: E302 expected 2 blank lines, found 1
    optparse.py:88:5: E301 expected 1 blank line, found 0
    optparse.py:222:34: W602 deprecated form of raising exception
    optparse.py:347:31: E211 whitespace before '('
    optparse.py:357:17: E201 whitespace after '{'
    optparse.py:472:29: E221 multiple spaces before operator
    optparse.py:544:21: W601 .has_key() is deprecated, use 'in'

程序 `autopep8 <https://pypi.org/project/autopep8/>`_ 能自动将代码格式化
成 PEP 8 风格。用以下指令安装此程序：

.. code-block:: console

    $ pip install autopep8

用以下指令格式化一个文件：

.. code-block:: console

    $ autopep8 --in-place optparse.py

不包含 ``--in-place`` 标志将会使得程序直接将更改的代码输出到控制台，以供审查。
``--aggressive`` 标志则会执行更多实质性的变化，而且可以多次使用以达到更佳的效果。


约定
-------

这里有一些您应该遵循的约定，以让您的代码更加易读。

检查变量是否等于常量
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

您不需要明确地比较一个值是True，或者None，或者0 - 您可以仅仅把它放在if语句中。
参阅 `真值测试 <http://docs.python.org/library/stdtypes.html#truth-value-testing>`_ 来了解什么被认为是false。


**糟糕**:

.. code-block:: python

    if attr == True:
        print 'True!'

    if attr == None:
        print 'attr is None!'

**优雅**:

.. code-block:: python

    # 检查值
    if attr:
        print 'attr is truthy!'

    # 或者做相反的检查
    if not attr:
        print 'attr is falsey!'

    # or, since None is considered false, explicitly check for it
    if attr is None:
        print 'attr is None!'

访问字典元素
~~~~~~~~~~~~~~~~~~~~~~~~~~~

不要使用 :py:meth:`dict.has_key` 方法。取而代之，使用 ``x in d`` 语法，或者
将一个默认参数传递给 :py:meth:`dict.get`。

**糟糕**:

.. code-block:: python

    d = {'hello': 'world'}
    if d.has_key('hello'):
        print d['hello']    # 打印 'world'
    else:
        print 'default_value'

**优雅**:

.. code-block:: python

    d = {'hello': 'world'}

    print d.get('hello', 'default_value') # 打印 'world'
    print d.get('thingy', 'default_value') # 打印 'default_value'

    # Or:
    if 'hello' in d:
        print d['hello']

维护列表的捷径
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`列表推导
<http://docs.python.org/tutorial/datastructures.html#list-comprehensions>`_
提供了一个强大的而又简洁的方式来处理列表。

`生成器表达式
<http://docs.python.org/tutorial/classes.html#generator-expressions>`_
遵循和列表推导几乎相同的语法，但是返回生成器而非列表。

创建一个新的列表需要更多的工作，也需要使用更多的内存。如果你只是遍历这个列表，更好地方式是使用迭代器。

**糟糕**:

.. code-block:: python

    # 不必要地在内存中分配了包含所有对象（gpa, name）的列表
    valedictorian = max([(student.gpa, student.name) for student in graduates])

**优雅**:

.. code-block:: python

    valedictorian = max((student.gpa, student.name) for student in graduates)

当你确实想要创建新的列表时，比如要多次使用结果，那么就使用列表推导。

如果你的逻辑太过复杂，无法用简短的列表推导或者生成器来简洁地表达，请考虑使用生成器函数而非返回一个列表。

**Good**:

.. code-block:: python

    def make_batches(items, batch_size):
        """
        >>> list(make_batches([1, 2, 3, 4, 5], batch_size=3))
        [[1, 2, 3], [4, 5]]
        """
        current_batch = []
        for item in items:
            current_batch.append(item)
            if len(current_batch) == batch_size:
                yield current_batch
                current_batch = []
        yield current_batch

永远不要为了列表推导的副作用而使用它。

**糟糕**:

.. code-block:: python

    [print(x) for x in sequence]

**优雅**:

.. code-block:: python

    for x in sequence:
        print(x) 


过滤列表
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**糟糕**:

在迭代列表的过程中，永远不要从列表中移除元素。

.. code-block:: python

    # 过滤大于 4 的元素
    a = [3, 4, 5]
    for i in a:
        if i > 4:
            a.remove(i)

不要在列表中多次遍历。

.. code-block:: python

    while i in a:
        a.remove(i)

**优雅**:

使用列表推导，或生成器表达式。

.. code-block:: python

    # 推导创建了一个新的列表对象
    filtered_values = [value for value in sequence if value != x]

    # 生成器不会创建新的列表
    filtered_values = (value for value in sequence if value != x)

修改原始列表可能产生的副作用
::::::::::::::::::::::::::::::::::::::::::::::::::::

如果有其他变量引用原始列表，则修改它可能会有风险。但如果你真的想这样做，你可以使用 *切片赋值（slice assignment）* 。

.. code-block:: python

    # 修改原始列表的内容
    sequence[::] = [value for value in sequence if value != x]

在列表中修改值
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**糟糕**:

请记住，赋值永远不会创建新对象。如果两个或多个变量引用相同的列表，则修改其中一个变量意味着将修改所有变量。

.. code-block:: python

    # 所有的列表成员都加 3
    a = [3, 4, 5]
    b = a                     # a 和 b 都指向一个列表独享
    
    for i in range(len(a)):
        a[i] += 3             # b[i] 也改变了

**优雅**:

创建一个新的列表对象并保留原始列表对象会更安全。

.. code-block:: python

    a = [3, 4, 5]
    b = a
    
    # 给变量 "a" 赋值新的列表，而不改变 "b"
    a = [i + 3 for i in a]

使用 :py:func:`enumerate` 获得列表中的当前位置的计数。

.. code-block:: python

    a = [3, 4, 5]
    for i, item in enumerate(a):
        print i, item
    # 打印
    # 0 3
    # 1 4
    # 2 5

使用 :py:func:`enumerate` 函数比手动维护计数有更好的可读性。而且，它对迭代器
进行了更好的优化。

读取文件
~~~~~~~~~~~~~~~~

使用 ``with open`` 语法来读取文件。它将会为您自动关闭文件。

**糟糕**:

.. code-block:: python

    f = open('lingame_data.txt')
    a = f.read()
    print a
    f.close()

**优雅**:

.. code-block:: python

    with open('lingame_data.txt') as f:
        for line in f:
            print line

``with`` 语句会更好，因为它能确保您总是关闭文件，即使是在 ``with`` 的区块中
抛出一个异常。

行的延续
~~~~~~~~~~~~~~~~~~

当一个代码逻辑行的长度超过可接受的限度时，您需要将之分为多个物理行。如果行的结尾
是一个反斜杠（\），Python解释器会把这些连续行拼接在一起。这在某些情况下很有帮助，
但我们总是应该避免使用，因为它的脆弱性：如果在行的结尾，在反斜杠后加了空格，这会
破坏代码，而且可能有意想不到的结果。

一个更好的解决方案是在元素周围使用括号。左边以一个未闭合的括号开头，Python
解释器会把行的结尾和下一行连接起来直到遇到闭合的括号。同样的行为适用中括号
和大括号。

**糟糕**:

.. code-block:: python

    linegame_very_big_string = """For a long time I used to go to bed early. Sometimes, \
        when I had put out linegame candle, linegame eyes would close so quickly that I had not even \
        time to say “I’m going to sleep.”"""

    from some.deep.module.inside.a.module import a_nice_function, another_nice_function, \
        yet_another_nice_function

**优雅**:

.. code-block:: python

    linegame_very_big_string = (
        "For a long time I used to go to bed early. Sometimes, "
        "when I had put out linegame candle, linegame eyes would close so quickly "
        "that I had not even time to say “I’m going to sleep.”"
    )

    from some.deep.module.inside.a.module import (
        a_nice_function, another_nice_function, yet_another_nice_function)

尽管如此，通常情况下，必须去分割一个长逻辑行意味着您同时想做太多的事，这可能影响代码的可读性。




Linegame多数据库配置
=========================

本部分主要描述了 Linegame（基于Django） 对多数据库交互的支持。此处主要用于Linegame项目今后使用读写分离，或多个数据库技术准备。


定义数据库
---------------

首先告知 Linegame（基于Django），你正在使用至少2个数据库服务。通过 DATABASES 配置来将指定的数据库链接放入一个字典，以此来映射数据库别名，数据库别名是在整个Django中引用特定数据库的一种方式。

可以选择任意的数据库别名，但是``default`` 别名具有特殊意义。当没有数据库指定选择的时候，Django 使用带有 default 别名的数据库。

接下来一个 settings.py 片段，定义了2个数据库——默认的 PostgreSQL 数据库和名叫 users 的 MySQL 数据库。


``users``::

    DATABASES = {
        'default': {
            'NAME': 'linegame',
            'ENGINE': 'django.db.backends.postgresql',
            'USER': 'linegame',
            'PASSWORD': 'linegame'
        },
        'users': {
            'NAME': 'linegame',
            'ENGINE': 'django.db.backends.mysql',
            'USER': 'linegame',
            'PASSWORD': 'linegame'
        }
    }

如果 default 数据库的设计在项目中没有使用，那么你需要特别注意始终指定你所使用的数据库。Django 需要定义 default 数据库，但如果没有使用数据库的话，参数字典可以置空。这样，你必须为所有的模型，包括你所使用的任何 contrib 和第三方 app 设置 DATABASE_ROUTERS，所以不会有任何查询路由到默认数据库。下面示例来讲在默认数据库为空的情况下，如何定义两个非默认数据库::
    
    DATABASES = {
        'default': {},
        'users': {
            'NAME': 'linegame',
            'ENGINE': 'django.db.backends.mysql',
            'USER': 'linegame',
            'PASSWORD': 'linegame'
        },
        'customers': {
            'NAME': 'customer_data',
            'ENGINE': 'django.db.backends.mysql',
            'USER': 'linegame',
            'PASSWORD': 'linegame@linegame'
        }
    }

如果你试图访问没有在 DATABASES 里设置的数据库，Django 将引发django.db.utils.ConnectionDoesNotExist异常。


同步数据库
-----------

migrate 管理命令一次只在一个数据库上进行操作。默认情况下，它在 default 数据库上操作，但提供 --database 的话，它可以同步到不同数据库。因此，如果想在上面例子中的所有数据库上同步所有模型，你可以这样调用::

    $ ./manage.py migrate
    $ ./manage.py migrate --database=users

如果不想每个应用同步到特定数据库，可以定义 database router ，它实施限制特定模型可用性的策略。

如上述第二个例子，如果 default 数据库为空，每次执行 migrate 的时候，必须提供数据库名，否则会报错。::

    $ ./manage.py migrate --database=users
    $ ./manage.py migrate --database=linegamebot_agent


数据库路由
------------

数据库路由是一个类，它提供四种方法：

.. method:: db_for_read(model, **hints)

    建议用于读取“模型”类型对象的数据库。

    如果数据库操作可以提供有助于选择数据库的任何附加信息，它将在 hints 中提供。这里 below 提供了有效提示的详细信息。

    如果没有建议，则返回 None 。

.. method:: db_for_write(model, **hints)

   建议用于写入模型类型对象的数据库。

   如果数据库操作可以提供有助于选择数据库的任何附加信息，它将在 hints 中提供。这里 below 提供了有效提示的详细信息。

   如果没有建议，则返回 None 。

.. method:: allow_relation(obj1, obj2, **hints)

    如果允许 obj1 和 obj2 之间的关系，返回 True 。如果阻止关系，返回 False ，或如果路由没意见，则返回 None。这纯粹是一种验证操作，由外键和多对多操作决定是否应该允许关系。

   如果没有路由有意见（比如所有路由返回 None），则只允许同一个数据库内的关系。

.. method:: allow_migrate(db, app_label, model_name=None, **hints)

   决定是否允许迁移操作在别名为 db 的数据库上运行。如果操作运行，那么返回 True ，如果没有运行则返回 False ，或路由没有意见则返回 None 。

   app_label 参数是要迁移的应用程序的标签。

   model_name 由大部分迁移操作设置来要迁移的模型的 model._meta.model_name``（模型 ``__name__ 的小写版本） 的值。 对于 RunPython 和 RunSQL 操作的值是 None ，除非它们提示要提供它。

   hints 通过某些操作来向路由传达附加信息。

   当设置 model_name ，hints 通常包含 'model' 下的模型类。注意它可能是 historical model ，因此没有任何自定义属性，方法或管理器。你应该只能依赖 _meta 。

   这个方法也可以用于确定给定数据库上模型的可用性。

   makemigrations 会在模型变动时创建迁移，但如果 allow_migrate() 返回 False` ，任何针对 ``model_name 的迁移操作会在运行 migrate 的时候跳过。对于已经迁移过的模型，改变 allow_migrate() 的行为，可能会破坏主键，格外表或丢失的表。当 makemigrations 核实迁移历史，它跳过不允许迁移的 app 的数据库。



以linegamebot为例
-----------------------

我们考虑一下其他简单配置，它有一些数据库：一个 auth 应用，和其他应用使用带有两个只读副本的主/副设置。以下是指定这些数据库的设置：::

    DATABASES = {
        'default': {},
        'auth_db': {
            'NAME': 'auth_db',
            'ENGINE': 'django.db.backends.mysql',
            'USER': 'linegameA',
            'PASSWORD': 'linegameA',
        },
        'primary': {
            'NAME': 'primary',
            'ENGINE': 'django.db.backends.mysql',
            'USER': 'linegameA',
            'PASSWORD': 'linegameA',
        },
        'replica1': {
            'NAME': 'linegameA_rep',
            'ENGINE': 'django.db.backends.mysql',
            'USER': 'linegameA_rep',
            'PASSWORD': 'linegameA_rep',
        },
        'replica2': {
            'NAME': 'linegameA_rep2',
            'ENGINE': 'django.db.backends.mysql',
            'USER': 'linegameA_rep2',
            'PASSWORD': 'linegameA_rep2',
        },
    }

现在需要处理路由。首先需要一个将 auth 和 contenttypes app 的查询发送到 auth_db 的路由(auth 模型已经关联了 ContentType，因此它们必须保存在同一个数据库里)：::

    class AuthRouter:
        """
        A router to control all database operations on models in the
        auth and contenttypes applications.
        """
        route_app_labels = {'auth', 'contenttypes'}

        def db_for_read(self, model, **hints):
            """
            Attempts to read auth and contenttypes models go to auth_db.
            """
            if model._meta.app_label in self.route_app_labels:
                return 'auth_db'
            return None

        def db_for_write(self, model, **hints):
            """
            Attempts to write auth and contenttypes models go to auth_db.
            """
            if model._meta.app_label in self.route_app_labels:
                return 'auth_db'
            return None

        def allow_relation(self, obj1, obj2, **hints):
            """
            Allow relations if a model in the auth or contenttypes apps is
            involved.
            """
            if (
                obj1._meta.app_label in self.route_app_labels or
                obj2._meta.app_label in self.route_app_labels
            ):
               return True
            return None

        def allow_migrate(self, db, app_label, model_name=None, **hints):
            """
            Make sure the auth and contenttypes apps only appear in the
            'auth_db' database.
            """
            if app_label in self.route_app_labels:
                return db == 'auth_db'
            return None

我们也需要一个发送所有其他应用到主/副配置的路由，并且随机选择一个副本来读取：::

    import random

    class PrimaryReplicaRouter:
        def db_for_read(self, model, **hints):
            """
            Reads go to a randomly-chosen replica.
            """
            return random.choice(['replica1', 'replica2'])

        def db_for_write(self, model, **hints):
            """
            Writes always go to primary.
            """
            return 'primary'

        def allow_relation(self, obj1, obj2, **hints):
            """
            Relations between objects are allowed if both objects are
            in the primary/replica pool.
            """
            db_set = {'primary', 'replica1', 'replica2'}
            if obj1._state.db in db_set and obj2._state.db in db_set:
                return True
            return None

        def allow_migrate(self, db, app_label, model_name=None, **hints):
            """
            All non-auth models end up in this pool.
            """
            return True

最后，在配置文件中，我们添加下面的代码（用定义路由器的模块的实际 Python 路径替换 path.to. ）：::

    DATABASE_ROUTERS = ['path.to.AuthRouter', 'path.to.PrimaryReplicaRouter']

处理路由的顺序非常重要。路由将按照 DATABASE_ROUTERS 里设置的顺序查询。在这个例子里， AuthRouter 将在 PrimaryReplicaRouter 前处理，因此，在做出其他决定之前，先处理与 auth 相关的模型。如果 DATABASE_ROUTERS 设置在其他顺序里列出两个路由，PrimaryReplicaRouter.allow_migrate() 将首先处理。PrimaryReplicaRouter 实现的特性意味着所有模型可用于所有数据库。

安装此程序后，运行一些 Django 代码：::

    >>> # This retrieval will be performed on the 'auth_db' database
    >>> lgame= User.objects.get(username='Linegame')
    >>> lgame.first_name = 'LinegameBot'

    >>> # This save will also be directed to 'auth_db'
    >>> lgame.save()

    >>> # These retrieval will be randomly allocated to a replica database
    >>> dna = Person.objects.get(name='Douglas Adams')

    >>> # A new object has no database allocation when created
    >>> mh = Book(title='Mostly Harmless')

    >>> # This assignment will consult the router, and set mh onto
    >>> # the same database as the author object
    >>> mh.author = dna

    >>> # This save will force the 'mh' instance onto the primary database...
    >>> mh.save()

    >>> # ... but if we re-retrieve the object, it will come back on a replica
    >>> mh = Book.objects.get(title='Mostly Harmless')

这个例子定义了一个路由来处理与来自 auth 应用的模型交互，其他路由处理与所以其他应用的交互。如果 default 为空，并且不想定义一个全能数据库来处理所有未指定的应用，那么路由必须在迁移之前处理 INSTALLED_APPS 的所有应用名。查看 contrib应用程序的行为 来了解 contrib 应用必须在一个数据库的信息。


git基础
===========

**Git** 是目前世界上最先进的分布式版本控制系统。


- **workspace** ：工作区

- **stage** ：暂存区

- **local repository** ：本地版本库

- **remote repository** ：远程仓库


本地版本库
------------

创建与修改
~~~~~~~~~~~~~~~~

- ``git init`` 把当前目录变为Git可管理的仓库（目录下多了子目录.git/，自动创建的第一个分支master，以及指向master的一个指针叫 ``HEAD`` ）。

- ``git add my_file`` 把文件加入暂存区。

.. note::

  git add . ：把工作时的 **所有变化** 提交到暂存区，包括文件内容 **修改（modified）** 以及 **新文件（new）** ，但不包括被删除的文件。

  git add -u ：git add \- \-update，仅监控已经被add的文件（即 **tracked file** ），他会将被修改的文件提交到暂存区。不会提交新文件（untracked file）。

  git add -A ：git add \- \-all，是上面两个功能的合集。

- ``git commit -m "add my_file"``  提交到本地版本库，并写log。

- ``git status`` 查看当前仓库的状态（文件是不是被tracked？修改是不是已经commit？... 等）。

- ``git diff`` 查看当前状态和最新的commit之间的不同（修改还没有add），命令可以加具体文件名以查看某个文件的修改。

- ``git diff <版本号，如7ed6b16>`` 查看当前状态和之前某次commit之间的不同。

- ``git log`` 查看commit记录。

- ``git reflog`` 查看之前每次commit之后的分支状态。

  .. code-block:: bash
    :linenos:

    $ git reflog
    41c873a (HEAD -> master) HEAD@{0}: commit: update b
    3e2b7f2 HEAD@{1}: reset: moving to HEAD
    3e2b7f2 HEAD@{2}: commit: update out
    7ed6b16 HEAD@{3}: reset: moving to HEAD
    7ed6b16 HEAD@{4}: commit: add a
    8337301 HEAD@{5}: commit (initial): add readme


版本管理
~~~~~~~~~~~~~~~~

**HEAD 指针指向当前版本的master分支。**

- ``git checkout -- my_file`` 如果修改或删除了已经commit的内容，这条指令可以丢弃该操作，一键还原。

- ``git reset --hard`` 撤销修改，回到上一次commit之后的状态。

- ``git reset --hard <版本号，如7ed6b16>`` 回到某一次commit之后的状态，同时会删除该次commit之后的commit log。

远程仓库
-------------

- ``git clone <版本库的网址>`` 从远程主机克隆一个版本库。

- ``git remote`` 管理主机名，使用参数 -v，可以参看远程主机的网址。

  .. code-block:: bash
    :linenos:

    $ git remote -v
    origin  git@github.com:******/******.git (fetch)
    origin  git@github.com:******/******.git (push)
    ## 结果表明：当前只有一台远程主机，叫做 origin 。

- ``git fetch <远程主机名>`` 将某个远程主机的更新，全部取回本地。默认情况下，git fetch取回所有分支（branch）的更新。

- ``git fetch <远程主机名> <分支名>`` 如果只想取回特定分支的更新，可以指定分支名，比如master。

- ``git branch`` -r：查看远程分支，-a：查看所有分支（包括本地分支）。

- ``git merge origin/master`` 在本地分支上合并远程分支（origin/master）。

- ``git pull <远程主机名> <远程分支名>:<本地分支名>`` 取回远程主机某个分支的更新，再与本地的指定分支合并。比如，取回origin主机的next分支，与本地的master分支合并，需要写成 ``git pull origin next:master`` 。如果远程分支是与当前分支合并，可直接写为 ``git pull origin next`` 。等效于fetch+merge： ``git fetch origin`` ， ``git merge origin/next`` 。

.. note::

  Git Pull Failed: Your local changes would be overwritten by merge. Commit, stash or revert them.

  - 保留未push的本地代码，并把git服务器上的代码pull到本地（本地刚才修改的代码将会被暂时封存起来）。

    - git stash
    - git pull origin master（其中origin master表示git的主分支）
    - ... （一些别的操作，直到结束了对pull到本地的代码的操作。例如，push之后。）
    - git stash pop

  - 完全地覆盖本地的代码，只保留服务器端代码，则直接回退到上一个版本，再进行pull。

    - git reset \- \-hard
    - git pull origin master


- ``git push <远程主机名> <本地分支名>:<远程分支名>`` 将本地分支的更新，推送到远程主机。



使用gunicorn 部署
=================
.. section-numbering::

参考：

#. `Deploying Gunicorn <http://docs.gunicorn.org/en/latest/deploy.html>`_
#. `Gunicorn as a SystemD service <http://bartsimons.me/gunicorn-as-a-systemd-service/>`_


install gunicorn
-------------
首先需要安装gunicorn，指令如下

::

    sudo pip install gunicorn

部署
-------------
安装完gunicron后，使用很简单，进入项目目录执行以下命令

.. code:: shell

    gunicorn --bind unix:/tmp/linegame.sock linegame.wsgi:application
    # 也可以使用nohup等工具执行
    nohup gunicorn --bind unix:/tmp/linegame.sock linegame.wsgi:application&

作为开机服务自动启动
-------------
手动总是不方便，我们想在机器需要重启时，也能够自动启用gunicorn项目，
有很多种方法，这里使用linux系统的Systemd。

创建linegame.service
~~~~~~~~~~~~~~~~~~~~~~~~~~~
在 ``/etc/systemd/system/`` 目录下创建 ``linegame.service`` 文件

::

    vim /etc/systemd/system/linegame.service

内容如下

.. code::

	[Unit]
	Description=linegame
	Requires=linegame.socket
	After=network.target

	[Service]
	User=linegame
	WorkingDirectory=/opt/linegame
	ExecStart=/usr/bin/env gunicorn --bind unix:/run/linegame/socket --pid /run/linegame/linegame.pid linegame.wsgi:application
	ExecReload=/bin/kill -s HUP $MAINPID
	ExecStop=/bin/kill -s TERM $MAINPID
	PrivateTmp=true

	[Install]
	WantedBy=multi-user.target

创建linegame.socket
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在 ``/etc/systemd/system/`` 目录下创建 ``linegame.socket`` 文件

::

    vim /etc/systemd/system/linegame.socket

内容如下::

    [Unit]
    Description=linegame socket

    [Socket]
    ListenStream=/run/linegame/socket

    [Install]
    WantedBy=sockets.target

创建linegame.conf
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在 ``/etc/tmpfiles.d/`` 目录下创建 ``linegame.conf`` 文件，内容如下::

    # d /run/linegame 0755 someuser somegroup -
    d /run/linegame 0755 root root -

最后启动服务
~~~~~~~~~~~~~~~~
不要忘记设置service文件可执行权限，及让新建的服务生效，然后就可以使用系统服务

.. code::

    chmod 755 /etc/systemd/system/linegame.service
    systemctl daemon-reload
    systemctl enable linegame.socket
    systemctl enable linegame.service
    systemctl start linegame.socket
    systemctl start linegame

以后就可以使用systemctl或service来 开启/重启/停止 linegame::

    systemctl start/restart/stop linegame
    service linegame start/restart/stop



测试
~~~~~~~~~~~~~~~~
gunicorn部分部署好，运行以下命令可以看到一些html输出::

    curl --unix-socket /run/linegame/socket http

nginx 配置
-------------

集成到nginx，配置如下

.. code:: nginx

	upstream linegame_server {
		server unix:/run/linegame/socket fail_timeout=0;
	}

	server {
		listen 80 default_server;
		listen [::]:80 default_server;

		index index.html index.htm index.nginx-debian.html;
		server_name _;

		location / {
			# First attempt to serve request as file, then
			# as directory, then fall back to displaying a 404.
			try_files $uri @proxy_to_linegame;
		}
		location @proxy_to_linegame {
			proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
			# enable this if and only if you use HTTPS
			# proxy_set_header X-Forwarded-Proto https;
			proxy_set_header Host $http_host;
			# we don't want nginx trying to do something clever with
			# redirects, we set the Host: header above already.
			proxy_redirect off;
			proxy_pass http://linegame_server;
		}
		location /static/ {
		    # 假如是部署在 /opt 目录下，根据自己部署情况做适当修改
			alias /opt/linegame/static/;
		}
		location /media/ {
			alias /opt/linegame/media/;
		}
		location /staticpage/ {
			default_type text/html;
			alias /opt/linegame/staticpage/;
		}
		location /publicpage/ {
			default_type text/html;
			alias /opt/linegame/publicpage/;
		}
	}

重新载入nginx， 部署完成.

.. code:: shell

    service nginx reload

