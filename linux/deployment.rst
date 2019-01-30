部署
========

virtualenvwrapper
-----------------------
a. pip install
b. 编辑 **~/.bashrc** 文件

- export WORKON_HOME=$HOME/.virtualenvs # 虚拟环境创建的地方
- export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3 # 指定虚拟使用的python解释器路径
- source /usr/local/bin/virtualenvwrapper.sh # 每次登陆用户自动执行下脚本

注：virtualenvwrapper管理的虚拟环境会放在 **/.virtualenvs** 里
