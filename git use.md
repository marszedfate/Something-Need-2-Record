#### git initialization

* 配置git:

  ```shell
  git config --global user.name "yourname"    //不需要引号
  git config --global user.email "youremail@example.com"
  ```


* 生成 SSH key:

  ```shell
  ssh-keygen -t rsa -C "youremail@example.com"
  ```

* 将 "C:\Users\DELL\\.ssh\id_rsa.pub" 的内容添加到 GitHub SSH key 中

* 验证是否成功(出现如下内容即成功)：

  ```shell
  >>>ssh -T git@github.com
  Hi marszed1997! You've successfully authenticated, but GitHub does not provide shell access.
  ```

#### Git operation

* 初始化仓库：

  ```shell
  git init
  ```


* 查看配置：

  ```shell
  git config --list
  ```

* 查看仓库状态：

  ```shell
  git status
  ```

* 链接到远程仓库：

  ```shell
  git remote add origin <url>
  ```

  如果已经链接到别的远程仓库，取消原来的链接：

  ```shell
  git remote rm origin
  ```

#### 分区切换

* 将文件从暂存区退回到工作区：

  ```shell
  git reset HEAD 
  ```

#### push to GitHub

* 添加文件(到暂存区)：

  ```shell
  git add "filename"
  git add .    //全部修改的内容添加到暂存区
  ```
  将修改提交到本地仓库：

  ```shell
  git commit -m "add file"
  ```
  push 到远程仓库：

  ```shell
  git push -u origin master
  ```

* 删除文件：

  ```shell
  git rm "filename"
  ```
  同样将修改提交到本地仓库：

  PS: 添加或删除之后都是一样的提交

  ```shell
  git commit -m "remove file"
  ```

  push 到远程仓库：

  ```shell
  git push -u origin master
  ```


#### rollback

* 查看 git 日志：

  ```shell
  git log
  ```

* 回滚到某一版本：

  ```shell
  git reset --hard "commit ID"
  ```

* 强制同步 GitHub (如果之前 push 到 GitHub 上了)：

  ```shell
  git push -f origin master
  ```

#### problem solution

* 如果本地仓库和远程仓库不一致：

  ```shell
  git pull --rebase origin master
  git push -u origin master
  ```


#### warning fix

* Linux下，连接到远程仓库时：

  ```shell
  >>>git push -u origin master
  Warning: Permanently added 'github.com,13.229.188.59' (RSA) to the list of known hosts.
  ```

  * 打开 etc/hosts

    ```shell
    cd etc
    sudo vi hosts
    ```

  * 粘贴文本

    ```shell
    # set github
    "13.229.188.59"[IP address] github.com
    ```

* 