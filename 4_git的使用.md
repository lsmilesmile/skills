### git的使用

###### git上传本地文件到github起步

1、个人信息配置

打开Git bash输入以下命令（用户和邮箱为你的github注册的账号和邮箱）

```
git config --global user.name "Felix"
git config --global user.email "112321qq.com"
```

2、设置SSH key

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

3、为github账号配置ssh key

切换到github，展开个人头像的小三角，点击settings，然后打开SSH and GPG keys菜单， 点击New SSH key，在Title中填上标题（最好跟本地仓库保持一致），在key栏中输入刚才记事本打开的文件内容，点击Add SSH key。

4、上传本地文件到github

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



###### 基本命令

1. 克隆github或者码云上代码到本地

   ```
   git clone  分支名仓库名地址
   ```

2. 创建自己的分支

   ```
   git checkout -b lsmilesmile
   ```

3. 更新文件到github

   ```
   git add 文件名称或者 git add.  # git add .是提交当前文件夹下的所有文件
   git commit -m "这是注释内容"
   git pull origin master  # 从本地仓库或本地分支获取并集成(整合)
   git push -u origin master
   ```

4. 在命令行删除远程仓库的文件（夹） - useless

   ```
   git rm --cached -r useless  # useless是要删除的文件的名字
   git commit -m "remove directory from remote repository"
   git push
   ```

   **注意，要使用-r参数**

5. 撤销add添加的文件

```git
git status  # 先看一下add中的文件
git reset HEAD  # 如果后面什么都不跟的话，就是上一次add里面的全部撤销
git reset HEAD filename  # 撤销某个文件
```



###### 代码分支合并，tag提交

1. 将自己分支代码合并到测试分支以便测试人员测试 先切换版本到dev分支 

   ```
   git checkout dev
   ```

2. 当前dev分支在合并lsmilesmile分支

   ```
   git merge lsmilesmile
   ```

3. 提交dev分支合并的代码到远程dev分支上 

   ```
   git push origin dev
   ```

4. 上线代码需要打tag，在master分支打tag 打版本v1.0.0.0 

   ```
   git tag -a 版本号 -m '注解'
   ```

   提交版本v1.0.0.0 

   ```
   git push origin v1.0.0.0
   ```



###### 缓存机制，在某一个分支修改了代码，但是不想提交该分支，又想切换到另外一个分支在修改相同的代码，就需要使用stash命令

1. 缓存本地修改的代码

   ```
   git stash
   ```

   缓存之后，在git status去查看修改代码记录会发现提示 nothing to commit，working tree clean。说明刚才修改的代码都缓存起来了

2. 查看缓存的片段

   ```
   git stash list
   ```

   发现有缓存列表，刚才缓存的记录为 stash@{0}: XXXXXXXXXX

3. 还原缓存的代码

   ```
   git stash apply stash@{0}
   ```

------



###### 查看某次提交的详情，退回代码到某一次提交

1. 查看提交的日志记录

   ```
   git log
   ```

   例如结果提交信息的日志如下：

   ```
   commit f9838aa51ca5ccd603e1e8cbd347a43c9cd2e0be
   Merge: f5847ec 52dc6fa
   Author: lsmilesmile <779598160@qq.com>
   Date:   Mon Jan 29 17:15:34 2018 +0800
   
       Merge branch 'whf_p0' into dev
   
   commit 52dc6fa34f36fae981d1c347825af93a150308fa
   Author: lsmilesmile <779598160@qq.com>
   Date:   Mon Jan 29 17:15:22 2018 +0800
   
       完成预约增加预约到店时间
   ```

2. 查看某次提交的内容

   ```
   git show commit-id
   ```

3. 退回代码 回退到当前版本用HEAD表示当前版本，上一个版本是HEAD^,或者使用HEAD~1，表示上一个版本。HEAD后面是数字可以一直往大了写，只要有那么多老版本

   ```
   git reset --hard
   ```

   