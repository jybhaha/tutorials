#windows git安装教程

[toc]

----------


##git for windows的安装
按官方提示安装即可
安装完成后设置：
```
$ git init
$ git config --global user.name "名字"
$ git config --global user.email "邮箱"
```

----------


##配置SSH
git for windows安装完毕后，首先要配置SSH密钥。
Git是分布式的代码管理工具，远程的代码管理是基于SSH的，所以要使用远程的Git则需要SSH的配置。
###查看是否存在SSH密钥
>windows的SSH密钥一般在C:\user\jiao\.ssh目录下面。
但是也有特殊情况。
我用的不是git bash客户端，而是**[babun][1]**客户端。默认吧在babun的安装目录下创建了home\用户名\.SSH。
这里可以用神奇everything搜索一下。

若是存在.ssh目录说明已经生成过了。否则下一步
###生成密钥
输入命令：**ssh-keygen -t rsa -C "jybhaha@gmail.com"**
jybhaha@gmail.com是自己邮箱。
第一次是生成密钥路径。回车保持默认即可。
第二次输入密码。
第三次保持和第二次输入的密码一致。
```shell
{ jiao }  » ssh-keygen -t rsa -C "jybhaha@gmail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/jiao/.ssh/id_rsa):
Created directory '/home/jiao/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/jiao/.ssh/id_rsa.
Your public key has been saved in /home/jiao/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:DKXTToUEgeXL5wi5KLAJ9XHNhvyrnKKuOK5rvnPKAuU jybhaha@gmail.com
The key's randomart image is:
+---[RSA 2048]----+
|     o++o..      |
|    .o B..       |
|  . . O *        |
| ... = X         |
|oo  + o S        |
|+oE. o + .       |
|= . . . o        |
|=+ ... o         |
|@@B. .+          |
+----[SHA256]-----+

```
会在.ssh目录下生成两个文件：
>id_rsa
id_ras.pub

分别对应私钥和公钥
###添加密钥
添加私钥id_rsa
预期结果：
```
{ .ssh }  » ssh-add id_rsa
Identity added: id_rsa (id_rsa)

```
但是可能会出现这样的结果：
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0670 for 'id_rsa' are too open.
It is recommended that your private key files are NOT accessible by others.
This private key will be ignored.
```
这是因为私钥文件本身的读写权限的问题。
只需要更改id_rsa的文件权限即可：
```
chmod 700 id_rsa  
```
>虽然是在windows上，但是我安装的[babun][1]允许在win平台使用部分Linux的命令。

###在github网站上提交公钥

 1. 登陆github账号
 2. 点击右上角头像，找到setting
 3. 点击SSH and GPG keys
 4. new SSH keys
 
###验证是否登陆成功
预期结果：
```
{ .ssh }  » ssh git@github.com
PTY allocation request failed on channel 0
Hi jybhaha! You've successfully authenticated, but GitHub does not provide shell a Connection to github.com closed.

```


----------


##开始使用git
>在使用了git init 命令的目录下使用以下命令

下面是一些常用的git命令：
###想重新添加一个目录

 - 登陆github，点击 create a new reop，输入Bingwallpapers。这是的目录还是空的，我们可以直接在网页上编辑，也可以将一个本地仓库与之关联。
```
$ git remote add origin git@github.com:用户名/bingwallpapers.git
```
 - 刷新一下本地仓库
```
 $ git pull origin master // 每次使用之前最好刷新一下
```
 - 添加文件及提交
```
$git add .
$git commit -m "first init"
```
 - 将本地仓库推送（push）到远程repo
```
 $ git push -u origin master //由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令
  $ git push  origin master  // 后期，当然在分支的情况，另论
```


  [1]: http://babun.github.io/