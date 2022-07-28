### 1 SSH

#### 1.1 在 Ubuntu 上安装并使用 SSH

```shell
sudo apt install openssh-server
```

```shell
# Verify that ssh service running
sudo systemctl status ssh

# If not running, enable the ssh server and start it 
sudo systemctl enable ssh
sudo systemctl start ssh
```

#### 1.2 连接远程主机

```shell
# Known ip
ssh [user_name]@[ip]

#Known host name
ssh [user_name]@[host_name]
```

#### 1.3 配置防火墙

```shell
sudo ufw allow ssh
sudo ufw enable
sudo ufw status
```

[how open or allow port 22 when using ufw on Ubuntu:]: https://www.cyberciti.biz/faq/ufw-allow-incoming-ssh-connections-from-a-specific-ip-address-subnet-on-ubuntu-debian/

#### 1.4 注意

* SSH 报错：`WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED`

    目标主机的公钥发生了改变（比如重新安装了SSH程序），而本地保存的是原来的公钥

    ```shell
    # If local is ubuntu
    vi ~/.ssh/known_hosts
    # 找到目标主机的公钥信息并删除
    
    # If local is windows
    # 记事本打开 C:\Users\[User_name]\.ssh\known_hosts
    # 找到目标主机的公钥信息并删除
    ```

[Ubuntu Linux install OpenSSH server]: https://www.cyberciti.biz/faq/ubuntu-linux-install-openssh-server/



### 2 wget

#### 2.1 wget 命令使用

* 下载文件到当前文件夹

    ```shell
    wget [url](https://xxxx.tar.xz)
    ```

* 下载文件到指定文件夹

    ```shell
    # Download file to /tmp/ dir
    wget -P [dir](/tmp/) [url]
    ```



### 3 tar

#### 3.1 tar 命令使用

* 解压 后缀为 tar.gz 文件

    ```shell
    tar –xzvf [file_name].tar.gz
    ```



### 4 vnc 

#### 4.1 vnc 安装

* 安装 x11vnc 

    ```shell
    sudo apt-get install x11vnc net-tools
    ```

* 将 x11vnc 写入 

    ```shell
    $ cd /etc/systemd/system
    $ sudo vi x11vnc@.service
    
    # 写入内容
    [Unit]
    Description=VNC Server for X11
    Requires=display-manager.service
    After=display-manager.service
    
    [Service]
    Type=forking
    ExecStart=/usr/bin/x11vnc -rfbauth /home/[user](sethma12)/.vnc/passwd -forever -shared -bg -display :0
    Restart=on-failure
    RestartSec=10
    User=%I
    
    [Install]
    WantedBy=multi-user.target
    ```

* 创建密码

    ```shell
    x11vnc -storepasswd 
    ```

* 启动服务

    ```shell
    # 修改了 /etc/systemd/system之后需要重启服务
    systemctl daemon-reload
     
    systemctl enable x11vnc.service
    systemctl restart x11vnc@sethma12.service
    # 查询状态
    systemctl status x11vnc@sethma12.service
    ```

[🔗]: https://www.makeuseof.com/install-ubuntu-vnc-server-linux/
[🔗]: https://bbs.archlinux.org/viewtopic.php?id=168756



### 5 换源

[🔗]: https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/

