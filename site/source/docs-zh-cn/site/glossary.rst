========
词汇表
========

通用
=======

.. glossary::
  :sorted:

  XHR
    ``XMLHttpRequest`` 的缩写. Emscripten 用 XHRs 来异步下载二进制数据.

  LLVM backend
    是 (*Clang*) 编译器后端将 :term:`LLVM` 中间表示物 (IR) 转换为特定机器或者语言的代码. 在 Emscripten 中, 目标是 JavaScript.

  Minifying
    `Minification <http://en.wikipedia.org/wiki/Minification_(programming)>`_ 在 JavaScript 中是指去除源代码中的标点符号而不改变函数功能的过程. 在高度At higher optimisation levels Emscripten uses the :term:`Closure Compiler` to minify Emscripten code.

  Relooping
    Recreate high-level loop and ``if`` structures from the low-level labels and branches that appear in LLVM assembly (definition taken from `this paper <https://github.com/emscripten-core/emscripten/blob/master/docs/paper.pdf?raw=true>`_).

  SDL
    `多媒体库 <https://www.libsdl.org/>`_ (SDL) 是一个跨平台开发库提供对音响,键盘,鼠标,手柄和图形显卡(通过 OpenGL 和 Direct3D)的访问.

  Typed Arrays Mode 2
    *Typed Arrays Mode 2* 是当前 :ref:`emscripten-memory-model` 使用的方法. 是 (current) :ref:`Fastcomp <LLVM-Backend>` 编译器唯一支持的内存模型, 而且是 :ref:`old compiler <original-compiler-core>` 默认的内存模型.

    原来的编译器支持多种内存模型和编译模型 (查看 `Code Generation Modes <https://github.com/emscripten-core/emscripten/wiki/Code-Generation-Modes>`_) 但是 *Typed Arrays Mode 2* 提供了对任意代码最好的支持, 和其他一些好处.


  Load-store consistency
    加载存储一致性 (LSC), 是指当变量以一种类型写入内存, 读取那个内存后得到相同类型. 所以当一个变量包含一个32位浮点数, 那么加载和存储这个变量都会是32位浮点数, 不会是16位无符号整数或者其他类型.

    .. note:: 这个定义来自 `Emscripten: An LLVM-to-JavaScript Compiler <https://github.com/emscripten-core/emscripten/blob/master/docs/paper.pdf?raw=true>`_ (section 2.1.1). 这篇文章中还有更多细节.


Emscripten 工具和依赖
=================================

.. glossary::
  :sorted:

  Clang
    Clang 是编译器前端, 针对 C, C++, 和使用 :term:`LLVM` 作为后端的其他语言.

  emcc
    The :ref:`emccdoc`. Emscripten 的编译器用于直接替换像 *gcc* 编译器.

  Emscripten Command Prompt
    The :ref:`emcmdprompt` 用来在Windows下命令行调用 Emscripten 工具.

  Compiler Configuration File
    The :ref:`编译器控制文件 <compiler-configuration-file>` 存储 :term:`激活 <Active Tool/SDK>` 的工具和 SDKs 和 :term:`emsdk activate <emsdk>` 中定义的一样.

  LLVM
    `LLVM <http://en.wikipedia.org/wiki/LLVM>`_ 是编译器基础设施用于优化任意语言写的程序.

  Fastcomp
    :ref:`Fastcomp <LLVM-Backend>` 是 Emscripten 当前的编译器核心.

  node.js
    **Node.js** 跨平台运行时环境,用于服务器端和 JavaScript 写的网络运用. 本质上它让 JavaScript 运用可以在浏览器外运行.

  Python
    Python 是脚本语言用来写了许多 Emscripten 的工具. 需要的版本列在 :ref:`toolchain requirements <central-list-of-emscripten-tools-and-dependencies>`.

  Java
    `Java <http://www.java.com/en/download/faq/whatis_java.xml>`_ 是一种编程语言和计算平台. Emscripten 在提供一些高级优化的代码中使用. 需要的版本列在 :ref:`toolchain requirements <central-list-of-emscripten-tools-and-dependencies>`.

  JavaScript
    `JavaScript <http://en.wikipedia.org/wiki/JavaScript>`_ (`ECMAScript <http://en.wikipedia.org/wiki/ECMAScript>`_) 是一种编程语言,主要在浏览器中使用, 在客户端提供设备访问. 和 :term:`node.js` 同时使用, 它可以用在服务器端的网络编程中.

    `asm.js <http://asmjs.org/faq.html>`_ JavaScript 的子集,是 Emscripten 的目标语言.

  Closure Compiler
    闭包编译器用来最小化 Emscripten 生成的代码并使用高级优化.

  Git
    `Git <http://en.wikipedia.org/wiki/Git_(software)>`_ 是分布式版本控制系统. Emscripten 存储在 :term:`GitHub` 用 git 客户端更新和优化.

  GitHub
    `GitHub <https://github.com/>`_ 是 :term:`Git` 仓库网站, 同时提供基于项目的合作包括wikis,任务管理,bug追踪.

    Emscripten 存放在 GitHub.

  lli
  LLVM Interpreter
    `LLVM 解释器 (LLI) <http://llvm.org/releases/3.0/docs/CommandGuide/html/lli.html>`_ 使用 :term:`LLVM` 二进制代码执行程序. 这个工具不再维护,奇怪的错误会导致运行失败.

    Emscripten 提供了替换的工具, 查看 :term:`LLVM Nativizer`.

  LLVM Nativizer
    The LLVM 净化器 (`tools/nativize_llvm.py <https://github.com/emscripten-core/scripten/blob/master/tools/nativize_llvm.py>`_) 将 LLVM 二进制文件编译为原生可执行文件. 此链接到主机的库，因此将输出与 emscripten 生成的比较不一定是相同.

    角色与 :term:`LLVM Interpreter` 类似.

    .. note:: 这个工具的输出有时会失败. 这个工具是给开发人员修复 bugs 用的.


SDK Terms
=========

使用到 SDK 和 :ref:`emsdk` 时会用到下面的概念:

.. glossary::

  emsdk
    :ref:`emsdk` 用来完成所有的 SDK 维护, 可以安装,更新,添加,移除和 :term:`使用 <Active Tool/SDK>` :term:`SDKs <SDK>` 和 :term:`工具 <Tool>`. 大部分操作形式类似于 ``./emsdk command``. 获取 *emsdk* 脚本, 运行 :term:`Emscripten Command Prompt`.

  Tool
    在 :term:`SDK` 中捆绑的基本软件单元. 一个工具有名字和版本. 例如, **clang-3.2-32bit** 是一个工具包含32位版本 *Clang* v3.2 编译器. *Emscripten* 使用的其他工具包括 :term:`Java`, :term:`Git`, :term:`node.js`, 等等.

  SDK
    :term:`tools <Tool>` 的集合. 例如, **sdk-1.5.6-32bit** 是包含如下工具的 SDK : clang-3.2-32bit, node-0.10.17-32bit, python-2.7.5.1-32bit 和 emscripten-1.5.6.

    有很多不同的Emscripten SDK 包. 可以从 :ref:`here <sdk-download-and-install>` 下载.

  Active Tool/SDK
    :term:`emsdk` 可以存储多个版本的 :term:`tools <Tool>` 和 :term:`SDKs <SDK>`. The active tools/SDK 是使用 *Emscripten Command Prompt* 时默认使用的 tools 集合. 这个编译器配置存放在用户确定的持久文件中 (**~/.emscripten**) ,可以使用 *emsdk* 来修改.

  emsdk root directory
    :term:`emsdk` 可以管理任意多个 :term:`tools <Tool>` 和 :term:`SDKs <SDK>`, 它们存放在 :term:`subdirectories <SDK root directory>` 在目录 *emsdk 根目录*.  **emsdk 根目录** 在第一次安装 SDK 时确定.

  SDK root directory
    :term:`emsdk` 可以存储任意多个 tools 和 SDKs. *SDK 根目录* 用于存储特定 :term:`SDK`. 位置在相对于 :term:`emsdk root directory` 的目录: **<emsdk root>\\emscripten\\<sdk root directory>\\**


Site / Sphinx
==============

.. glossary::
  :sorted:

  reStructured text
    本站内容使用标记语言表示. 查看 `reStructured text primer <http://sphinx-doc.org/rest.html>`_.
