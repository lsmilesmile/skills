# git的使用

## git上传本地文件到github起步

### 1、个人信息配置

打开Git bash输入以下命令（用户和邮箱为你的github注册的账号和邮箱）

```
git config --global user.name "Felix"
git config --global user.email "112321qq.com"
```

### 2、设置SSH key

首先检查是否已经生成密钥输入：

```
~/.ssh
```

如果有则输入ls后会有三个文件生成：

```
id_rsa
id_rsa.pub
known_hosts
```

如果没有则通过：

```
ssh-keygen -t rsa -C "112321qq.com"
```

生成，生成过程中一路按3次回车键就好了。（默认路径，默认没有密码登录） 

 生成成功后，去对应目录C:\Users\lsmil\.ssh里（lsmil为电脑用户名，每个人不同）用记事本打开id_rsa.pub，得到ssh key公钥。 

### 3、为github账号配置ssh key

切换到github，展开个人头像的小三角，点击settings，然后打开SSH and GPG keys菜单， 点击New SSH key，在Title中填上标题（最好跟本地仓库保持一致），在key栏中输入刚才记事本打开的文件内容，点击Add SSH key。

### 4、上传本地文件到github

- 创建本地仓库repository

- 把要上传的文件放在该仓库文件夹下

- 在Git Bash中进入本地仓库文件夹repository，执行命令

  ```
  git init
  ```

- 初始化成功后你会发现多了一个隐藏的文件夹.git（隐藏的文件夹）执行指令

  ```
  git add .  # 将所有文件提交到本地仓库
  git commit -m "备注"  # 添加备注
  ```

- 关联github仓库

  - 到github repository仓库复制地址

  - 执行指令

    ```
    git remote add origin https://github.com/lsmilesmile/repository.git
    ```

  - 可以通过如下命令进行代码合并

    ```
    git pull --rebase origin master
    ```

  - 执行上面代码后看到本地代码库中多了README.md文件

  - 上传本地代码

    ```
    git push -u origin master
    ```

**ok - 可以看到我们的文件已经上传到github上了**



## 更新文件到github

```
git add 文件名称或者 git add.  # git add .是提交当前文件夹下的所有文件
git commit -m "这是注释内容"
git pull origin master  # 从本地仓库或本地分支获取并集成(整合)
git push -u origin master
```



## 在命令行删除远程仓库的文件（夹） - useless

```
git rm --cached -r useless  # useless是要删除的文件的名字
git commit -m "remove directory from remote repository"
git push
```

**一定要注意，删除文件夹要使用-r 参数**



## 撤销add添加的文件

```git
git status  # 先看一下add中的文件
git reset HEAD  # 如果后面什么都不跟的话，就是上一次add里面的全部撤销
git reset HEAD filename  # 撤销某个文件
```



