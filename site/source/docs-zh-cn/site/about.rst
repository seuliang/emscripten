.. _about-this-site:

===============
关于本站
===============

本站编译构建的工具为 `Sphinx <http://sphinx-doc.org/latest/index.html>`_ (1.2.2), 一个构建了Python官方文档和其他网站的开源工具. 它是一个成熟稳定的工具, 因此脱颖而出被选中, 它支持定义 API 条目并从代码中链接它们.

本站使用自定义的界面主题, 基于 :ref:`read-the-docs-theme`.

.. _about-this-site-search:

本站搜索
==================

搜索会返回包含 **所有** 设置的关键字的话题.

.. tip:: 搜索时使用 *单个* 单词, 像 "interacting" 或 "compiling". 一般这样就足够找到相关的文档了. 如果没找到, 可以添加另外的关键词重新搜索.

.. note:: 搜索包含 "-" 和 "+" 字符是无效的. 并不支持逻辑操作符号.

报告 bugs
==============

请到 :ref:`report documentation bugs <site-and-documentation-bug-reports>` 报告任何 Emscripten bug. 帮助 :ref:`fix them <writing-and-updating-articles>` 更新文档或者创建新的文档.

.. _about-this-site-contributing:

贡献帮助
========================

:ref:`贡献 <contributing>` 到此网址, 欢迎贡献帮助 (任何有关 Emscripten) !

查看一下文档了解如何参与贡献 :ref:`build the site <building-the-site>` 和 :ref:`write and update articles <writing-and-updating-articles>`.


.. _building-the-site:

编译本站
=================

本站的源代码保存在 `GitHub <https://github.com/emscripten-core/emscripten/tree/incoming/site>`_. 修改和添加应该提交到这个分支, 对其他部分的修改也是一样.

The site is published to the **emscripten-core/emscripten-site** *gh-pages* branch (GitHub pages).

.. note:: Remember to update the :ref:`about-build-versions` for *public* builds.

安装 Sphinx
-----------------

安装 Sphinx 教程在 `here <http://sphinx-doc.org/install.html>`_.


Ubuntu
++++++

Ubuntu 软件包仓库 (apt-get) 中的 Sphinx 在编译生成站点时会失败. 这是因为 Sphinx 早期版本 (1.1.3), 依赖于旧版本的 Jinja templating library.

解决办法是使用 *Python package installer* (pip) 获取版本 1.7.8, 然后进行升级 (注意, 应该先卸载 Sphinx 先): ::

  pip install sphinx==1.7.9


.. _about-site-builds:

编译方法
-----------

本站可以在 Ubuntu 和 Windows 平台上从源文件编译生成, 进入 */emscripten/site* 目录然后使用命令: ::

  make clean
  make html


.. _about-sdk-builds:

编译 SDK 
----------

SDK 编译方法基本相同于 :ref:`about-site-builds`. 主要的不同是在 SDk 编译时 :ref:`home page <home-page>` 会明确知道是 SDk 编译.

SDK 编译要设置 ``sdkbuild`` 标签. 通过设置 ``SPHINXOPTS`` 环境变量来实现: ::

  # 设置 sdkbuild 标签.
  set SPHINXOPTS=-t sdkbuild
  make html

  # 取消设置 SPHINXOPTS
  set SPHINXOPTS=

.. _about-build-versions:

Build 版本
-------------

文档的版本需要与 Emscripten 版本相同. 一般编译时标签会设置为 `Emscripten version <https://github.com/emscripten-core/emscripten/blob/incoming/emscripten-version.txt>`_. SDK 编译时的版本是 Emscripten 的版本.

版本信息和发布信息在文档的多处地方用到, 例如 :ref:`emscripten-authors`.

版本信息定义在 **conf.py** — 查看变量 ``version`` 和 ``release``. 变量可以被覆盖通过设置 ``SPHINXOPTS`` 环境变量. 例如, 为更新 ``release`` 变量通过命令行在Windows平台: ::

  # 设置 SPHINXOPTS
  set SPHINXOPTS=-D release=6.40
  make html

  # 取消设置 SPHINXOPTS
  set SPHINXOPTS=


.. _writing-and-updating-articles:

编写和更新文章
=============================

.. note:: Sphinx `文档全面 <http://sphinx-doc.org/latest/index.html>`_. 本节强调本站使用的特殊风格和特性.

  :ref:`building-the-site` 节解释了如何找到文章的源文件和编译本站点.


本站内容编写的语法为 :term:`reStructured text`. 推荐阅读下列文章了解语法:

* `reStructured text primer <http://sphinx-doc.org/rest.html>`_.
* `Sphinx Domains <http://sphinx-doc.org/domains.html>`_ (定义和连接代码条目).
* `Inline markup <http://sphinx-doc.org/markup/inline.html>`_.



界面风格指导
-----------

本节包含一些简单意见来帮助作者使用同一的风格.

.. tip:: 在贡献方面, 我们更看重你的编码和内容写作而不是完美的散文! 尽力而为, 然后 :ref:`ask for editorial review <contact>`.

**Spelling:** Where possible use US-English spelling.

**Avoid idiomatic expressions**: These can be particularly confusing to non-native speakers (for example "putting your foot in your mouth" actually means "saying something embarrassing").

**Emphasis:**

  - **Bold** : use for file names, and UI/menu instructions (for example: "Press **OK** to do something").
  - *Italic* : use for tool names - e.g. *Clang*, *emcc*, *Closure Compiler*.
  - ``monotype`` : use for inline code (where you can't link to the API reference) and for demonstrating tool command line options.

  .. note:: Other than the above rules, emphasis should be used sparingly.


**Lists**: Use a colon on the lead-in to the list where appropriate. Capitalize the first letter and use a full-stop for each item.


如何连接文章和标题
------------------------------------

To link to a page, first define a globally unique reference before the page title (e.g. ``_my-page-reference``) then link to it using the `ref <http://sphinx-doc.org/markup/inline.html#ref-role>`_ role as shown: ::

  .. _my-page-reference:

  My Page Title
  =============

  This is the text of the section.

  To link to page use either of the options below:
    ref:`my-reference-label` - the link text is the heading name after the reference
    ref:`some text <my-reference-label>` - the link text is "some text"

This is a better approach than linking to documents using the *:doc:* role, because the links do not get broken if the articles are moved.

This approach is also recommended for linking to arbitrary headings in the site.

.. note:: There are a number of other roles that are useful for linking — including `Sphinx Domains <http://sphinx-doc.org/domains.html>`_ for linking to code items, and **term** for linking to glossary terms.



Recommended section/heading markup
----------------------------------

reStructured text `defines <http://sphinx-doc.org/rest.html#sections>`_ section headings using a separate line of punctuation characters after (and optionally before) the heading text. The line of characters must be at least as long as the heading. For example: ::

  A heading
  =========

Different punctuation characters are used to specify nested sections. Although the system does not mandate which punctuation character is used for each nested level, it is important to be consistent. The recommended heading levels are: ::

  =======================================
  Page title (top and bottom bars of "=")
  =======================================

  Level 1 heading (single bar of "=" below)
  =========================================

  Level 2 heading (single bar of "-" below)
  -----------------------------------------

  Level 3 heading (single bar of "+" below)
  +++++++++++++++++++++++++++++++++++++++++

  Level 4 heading (single bar of "~" below)
  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


使用 markdown
-------------------

New articles may be authored and discussed on the `wiki <https://github.com/emscripten-core/emscripten/wiki>`_ using Markdown syntax before being included in the documentation set. The easiest way to convert these to restructured text is to use a tool like `Pandoc <http://johnmacfarlane.net/pandoc/try/?text=&from=markdown_github&to=rst>`_.

.. note:: The *get_wiki.py* tool (**/site/source/get_wiki.py**) can be used to automate getting a snapshot of the wiki. It clones the wiki and calls *pandoc* on each file. The output is copied to a folder **wiki_static**. The tool also adds a heading, a note stating that the file is a "wiki snapshot", and fixes up links marked as "inline code" to matching links in the API Reference.


.. _read-the-docs-theme:

查看文档界面主题
===================

The site uses a modification of the `Read the docs theme <http://read-the-docs.readthedocs.org/en/latest/theme.html>`_ (this can be found in the source at */emscripten/site/source/_themes/emscripten_sphinx_rtd_theme*).

The main changes to the original theme are listed below.

- **Footer.html**

  - Copyright changed to link to Emscripten authors (some code was broken by translation markup)
  - Added footer menu bar

- **Layout.html**

  - Added header menu bar with items

- **Breadcrumb.html**

  - Changed the text of the first link from "docs" to "Home"
  - Moved the "View Page Source" code into the bottom footer

- **theme.css**

  - Changed to support 4 levels of depth in sidebar toc.
  - Centred theme. Made sidebar reach bottom of page using absolute positioning.


Site license
============

The site is licensed under the same :ref:`emscripten-license` as the rest of Emscripten. Contributors to the site should add themselves to :ref:`emscripten-authors`.
