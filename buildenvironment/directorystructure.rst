目录结构
===========

.. contents:: 目录


安装依赖
--------------


搭建项目目录结构
--------------------

a. 创建包apps、extra-apps、创建文件夹db_tools、media，右键apps和extra_apps，选中“Mark Directory”下的“Source Root”（被标记为“source root”的文件夹会被添加到“PYTHONPATH”中，因此其会被解析）
b. 将apps、extra-apps加入到根搜索路径之下（如下）

::

  import os
  import sys

  # Build paths inside the project like this: os.path.join(BASE_DIR, ...)
  BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
  sys.path.insert(0, BASE_DIR)
  sys.path.insert(0, os.path.join(BASE_DIR, 'apps'))
  sys.path.insert(0, os.path.join(BASE_DIR, 'extra_apps'))

- b.注：可以任意组织项目结构，这只会影响到包的导入；上述的sys.path变量里存储了导包时的搜索路径；项目即是各种包里的代码的堆砌
