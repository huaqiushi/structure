目录结构
===========

.. contents:: 目录


安装依赖
--------------


搭建项目目录结构
--------------------

a. 创建包apps, extra-apps，将其标记为“Source Root”（被标记为“source root”的文件夹会被添加到“PYTHONPATH”中，因此其会被解析）
b. 将apps、extra-apps加入到根搜索路径之下

::

  import os
  import sys

  BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

  sys.path.insert(0, os.path.join(BASE_DIR, 'apps'))
  sys.path.insert(0, os.path.join(BASE_DIR, 'extra_apps'))

  - 注：可以任意组织项目的目录结构，这只会影响到包的导入；上述的sys.path变量里存储了导包时的搜索路径；项目即是各种包里的代码的堆砌
