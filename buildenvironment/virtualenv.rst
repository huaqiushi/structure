虚拟环境
============

virtualenv
--------------

1. 安装：pip install virtualenv

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

1. 安装：pip install virtualenvwrapper

2. 初始化——在$HOME/.bashrc中添加：

- export WORKON_HOME=$HOME/.virtualenvs  # 指定虚拟环境存放路径
- export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
- source $HOME/.local/bin/virtualenvwrapper.sh

3. 新建一个虚拟环境：mkvirtualenv venv
4. 进入一个虚拟环境：workon venv
5. 退出虚拟环境：deactivate
