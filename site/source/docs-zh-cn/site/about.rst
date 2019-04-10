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

:ref:`Contributions <contributing>` 到此网址, 欢迎贡献帮助 (任何有关 Emscripten) !

查看一下文档了解如何参与贡献 :ref:`build the site <building-the-site>` 和 :ref:`write and update articles <writing-and-updating-articles>`.


.. _building-the-site:

编译本站
=================

本站的源代码保存在 `GitHub <https://github.com/emscripten-core/emscripten/tree/incoming/site>`_. 修改和添加应该提交到这个分支, 对其他部分的修改也是一样.

The site is published to the **emscripten-core/emscripten-site** *gh-pages* branch (GitHub pages).

.. note:: Remember to update the :ref:`about-build-versions` for *public* builds.

安装 Sphinx
-----------------

Notes for installing Sphinx are provided `here <http://sphinx-doc.org/install.html>`_.


Ubuntu
++++++

The version of Sphinx on Ubuntu package repository (apt-get) fails when building the site. This is an early version (1.1.3), which appears to be dependent on an old version of the Jinja templating library.

The workaround is to use the *Python package installer* (pip) to get version 1.7.8, and then run an upgrade (note, you may have to uninstall Sphinx first): ::

  pip install sphinx==1.7.9


.. _about-site-builds:

编译方法
-----------

The site can be built from source on Ubuntu and Windows by navigating to the */emscripten/site* directory and using the command: ::

  make clean
  make html


.. _about-sdk-builds:

SDK Builds
----------

SDK builds are virtually identical to :ref:`about-site-builds`. The main difference is that on SDK builds the :ref:`home page <home-page>` has a clear notification that it is an SDK build.

SDK builds are enabled by enabling the ``sdkbuild`` tag. This is done through the ``SPHINXOPTS`` environment variable: ::

  # Set the sdkbuild tag.
  set SPHINXOPTS=-t sdkbuild
  make html

  # Unset SPHINXOPTS
  set SPHINXOPTS=

.. _about-build-versions:

Build version
-------------

The documentation version should match the Emscripten version for the current build. For a general site build this will be the latest tagged release as defined in `Emscripten version <https://github.com/emscripten-core/emscripten/blob/incoming/emscripten-version.txt>`_. For an SDK build it will be the Emscripten version for the SDK.

The version and release information is used in a few places in the documentation, for example :ref:`emscripten-authors`.

The version information is defined in **conf.py** — see variables ``version`` and ``release``. These variables can be overridden by setting new values in the ``SPHINXOPTS`` environment variable. For example, to update the ``release`` variable through the command line on Windows: ::

  # Set SPHINXOPTS
  set SPHINXOPTS=-D release=6.40
  make html

  # Unset SPHINXOPTS
  set SPHINXOPTS=


.. _writing-and-updating-articles:

Writing and updating articles
=============================

.. note:: Sphinx is `well documented <http://sphinx-doc.org/latest/index.html>`_. This section only attempts to highlight specific styles and features used on this site.

  The :ref:`building-the-site` section explains how to find the sources for articles and build the site.


Site content is written using :term:`reStructured text`. We recommend you read the following articles to understand the syntax:

* `reStructured text primer <http://sphinx-doc.org/rest.html>`_.
* `Sphinx Domains <http://sphinx-doc.org/domains.html>`_ (define and link to code items).
* `Inline markup <http://sphinx-doc.org/markup/inline.html>`_.



界面风格指导
-----------

This section has a few very brief recommendations to help authors use common style.

.. tip:: In terms of contributions, we value your coding and content writing far more than perfect prose! Just do your best, and then :ref:`ask for editorial review <contact>`.

**Spelling:** Where possible use US-English spelling.

**Avoid idiomatic expressions**: These can be particularly confusing to non-native speakers (for example "putting your foot in your mouth" actually means "saying something embarrassing").

**Emphasis:**

  - **Bold** : use for file names, and UI/menu instructions (for example: "Press **OK** to do something").
  - *Italic* : use for tool names - e.g. *Clang*, *emcc*, *Closure Compiler*.
  - ``monotype`` : use for inline code (where you can't link to the API reference) and for demonstrating tool command line options.

  .. note:: Other than the above rules, emphasis should be used sparingly.


**Lists**: Use a colon on the lead-in to the list where appropriate. Capitalize the first letter and use a full-stop for each item.


How to link to a document or heading
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
