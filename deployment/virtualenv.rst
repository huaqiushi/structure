虚拟环境
============

virtualenv
--------------

1. 安装virtualenv：pip install virtualenv
2. 在当前目录下创建虚拟环境：

- virtualenv env
- virtualenv -p /usr/bin/python3.5 venv  创建时选择python3.5作为解释器
- virtualenv --no-site-packages venv  创建时不依赖系统环境中的site packages（默认依赖）

3. 启动虚拟环境

- cd venv
- source ./bin/activate

4. 退出虚拟环境：deactivate


virtualenvwrapper
----------------------

将所有虚拟环境都存放在WORKON_HOME指向的路径下统一管理

1. 进入一个虚拟环境：workon venv
2. 新建一个虚拟环境：mkvirtualenv venv
