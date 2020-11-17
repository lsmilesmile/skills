# Anaconda常用命令

> author:刘笑
>
> date    : 2020/03/03

- **查看当前存在的环境**

  ```
  conda env list
  ```

- **列出环境中已经安装的库**

  ```
  conda list
  ```

- **创建环境**

  ```
  conda install -n 环境名 python=Python版本
  如：conda install -n my_env python=3.6
  ```

- **安装库**

  ```
  conda install 库名
  pip install 库名
  ```

- **激活环境**

  ```
  activate 环境名
  ```

- **删除环境**

  ```
  conda remove -n 环境名 --all
  ```

- **退出环境**

  ```
  deactivate 环境名
  ```

- **删除库**

  ```
  conda remove 库名
  ```

- **新建环境时同时安装一个包**

  ```
  conda create -n 环境名 python=Python版本 库名
  如：conda create -n my_env python=3.6 tensorflow
  ```

  