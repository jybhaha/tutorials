#github pages教程

本文参考[文章](http://pwnny.cn/original/2016/06/26/MakeBlog.html#NativeBuild02)

##Github Pages
Github是一个开源代码库及版本控制系统，它可以托管各种git库，号称程序员的Facebook，影响力非常大。而Github里的Pages功能，就是用来为项目建立网站，使项目的展示能够简明易懂。我们就可以通过它来建立托管在Github上的静态网页。
##Jekyll
Jekyll是一个简单免费的静态站点生成器，它根据网页源码生成静态文件，并且为我们提供了模板、插件。最关键的是可以免费部署在Github上。
###开始搭建
>**Jekyll官网上是不支持在window下搭建Jekyll的**

平台：Window10

1. Ruby
- Window 系统下，我们可以使用 RailsInstaller 来安装 Ruby 环境，[下载地址](http://railsinstaller.org/en)
- 下载 RailsInstaller 之后，双击 railsinstaller-3.2.0 文件，启动 Ruby 安装向导
- 点击 Next，继续向导，记得勾选 Add Ruby executables to your PATH，直到 Ruby 安装程序完成 Ruby 安装为止
安装后，通过在命令行中输入 $ ruby -v 命令来确保一切-工作正常
- 如果一切工作正常，将会输出所安装的 Ruby 解释器的版本。如果您安装了其他版本，则会显示其他不同的版本
>$ ruby -v
ruby 2.2.4p230 (2015-12-16 revision 53155) [i386-mingw32]

2. Jecky
安装位gem后会自动安装上Gems，下面使用gem安装Jekyll。
打开cmd命令行（我更推荐**Cmder**作为替代）
> $gem install jekyll

等待安装完毕即可。

3. Jekyll创建博客站点

cd到博客文件夹，执行命令
>jekyll new blog
New jekyll site installed in 目录

说明创建成功

4. 打开Jeckyll服务器
>$cd blog  #一定记得进入新创建的blog文件夹内
>$jekyll serve #启动一个地址为http://localhost:4000的服务器。在浏览器打开网址即可

**注意：**
若是提示
>Permission denied - bind(2) for 127.0.0.1:4000 (Errno::EACCES)

说明端口号4000被占用了，在_config.yml 末尾添加
>port: 4001

用端口4001创建即可。


用浏览器代开http://localhost:4001 出现Jekyll界面说明创建成功。



