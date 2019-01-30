Sphinx
==========

.. contents:: 目录


名词
-----------
文档编写工具：GitBook、MkDocs、Sphinx（三者均支持markdown标记语言；Sphinx默认支持rst标记语言）

 - rst：纯文本标记语言。其是Python Doc-SIG的Docutils项目的一部分

   - Docutils：一个开源的文本处理系统，包括rst
   - 纯文本标记语言：markdown、rst …

 - Read the Docs：一个托管Sphinx项目的网站

用法
------------
a. 使用sphinx-quickstart命令创建源目录（source directory）
b. 在源目录中的index.rst文件中定义目录树（toctree）
c. 根据目录树添加文档（rst、markdown等纯文本标记语言）

 - rst语法

   - 标题
   - 段落
   - 序号： **.. numbered::** 可以对指定层级内的标题自动添加序号
   - 图片： **.. image::**

d. 使用make命令生成一定格式的文档（html、epub、…）

使文档可被网络访问
-------------------------
a. 将文档项目托管在GitHub上
b. 在项目的Settings选项中的GitHub Pages里进行设置

.. image:: /.img/gitpage.JPG

高级用法
----------------
- Autodoc：自动抽取doc string
- Intersphinx：链接网络上的Sphinx文件（如Python官方文档……）

总结
------------
- 每个rst文件都会生成一个html网页
- rst文件中的toctree会根据路径生成目录（路径所指向的文件的标题会被解释为超链接）
- 在正文里插入目录：使用 **.. contents::** 指令
- 侧边栏里只显示标题：使用 **:titlesonly:** 指令

下一步
-----------
1. rst语法：基本文档格式、指令
2. toctree：深入了解
