常用命令：

- 新建文章：hexo new "My New Post"
- 启动服务：hexo server
- 生成静态文件：hexo generate
- 发布远程站点：hexo deploy

环境准备

- Node.js (Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本)
- Git

安装

1. 安装hexo脚手架
       npm install -g hexo-cli
2. 创建一个文件夹，下载所需要的文件
       mkdir wjqixige
       hexo init blog
       mv blog wjqixige
3. 下载项目依赖包
       npm install

写文章 

创建草稿

在准备写一篇文章的时候，可以先创建一篇操作，建立的草稿会保存到source/_drafts文件夹下,默认是不会显示到页面中的。 在预览的时候可以加上 --draft参数来进行预览，比如： $ hexo s --draft

    $ hexo new draft <title>

发表草稿

当文章写好并检查无误的时候，可以从source/_drafts文件夹将要发布的文章移动到 source/_posts文件夹下。

    $ hexo publish [layout] <title>

Front-matter

主要用于指定文章的变量，hexo预先定义好的参数如下：

  参数        	描述        	默认值   
  layout    	布局        	      
  title     	标题        	      
  date      	建立日期      	文件建立日期
  updated   	更新日期      	文件更新日期
  comments  	开启文章的评论功能 	true  
  tags      	标签（不适用于分页）	      
  categories	分类（不适用于分页）	      
  permalink 	覆盖文章网址    	      
  keywords  	          	      

YAML方式编写

    ---
    title: Hello World
    date: 2019/08/13 18:29:25
    ---

JSON方式编写

    "title":"Hello World",
    "date":"2019/08/13 18:29:25"
    ;;;

标签插件

引用快

    {% blockquote [作者名[, 资源名]] [URL链接] [资源链接标题] %}
    content
    {% endblockquote %}

Image

    {% img [class names] /path/to/image [width] [height] [title test [alt text]] %}

链接

    {% link text url [external] [title] %}

资源管理

图片管理

    #_config.yml
    post_asset_folder: true

打开资源文件管理功能后，hexo将会在你每一次通过hexo new [layout] <title>命令创建新文章时自动创建一个和文件名称一样的文件夹。放在这个文件夹中的资源通过相对路径来引用：

    {% asset_img slug [title] %}

本地预览

1. 清除缓存文件(db.json) 和已生成的静态文件（publlic）
       $ hexo clean
2. 生成静态文件public
       $ hexo generate  // 简写：  hexo g
3. 启动服务器
       $ hexo server  // 简写： hexo s
4. 本地预览：http://localhost:4000

主题

next

    cd wjqixige
    npm install hexo-theme-next  //更新 npm install hexo-theme-next@latest
    ## 克隆至仓库： git clone https://github.com/next-theme/hexo-theme-next themes/next

启动

    hexo server

git生成秘钥

SSH 秘钥默认储存在账户的主目录下的 ~/.ssh 目录。

    ## 生成秘钥
    $ ssh-keygen -t rsa -C "wujiang569@126.com"
    ## 然后在~/.ssh目录下将id_rsa.pub内容添加到：github -> setting -> SSH and GPG keys中

备份到github

在本地根目录初始化仓库并做第一次提交：

    $ git init
    $ git add .
    $ git commit -a -m "first commit"

在 Github 上新建一个空项目，然后在本地添加远程仓库地址并追踪：

    $ git remote add origin git@github.com:Coodool/hexo-blog-yearito.git
    $ git push --set-upstream origin master
    $ git push

themes/next主题无法提交，需要删除子模块

    $ git rm --cached themes\next

部署至阿里云

环境：CentOS8

源码：/soft/hexo/node、/soft/hexo/npm

安装node

    $ wget https://nodejs.org/dist/v10.9.0/node-v12.2.0-linux-x64.tar.xz
    $ tar xf node-v12.2.0-linux-x64.tar.xz
    $ cd node-v12.2.0-linux-x64
    $ ./bin/node -v
    $ mv node-v12.2.0-linux-x64 node
    
    ## 设置软连接
    $ ln -s /soft/hexo/nodejs/bin/node /usr/local/bin/node
    $ ln -s /soft/hexo/nodejs/bin/npm /usr/local/bin/npm

Git安装

    ## 安装依赖包
    $ yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
    $ yum install gcc perl-ExtUtils-MakeMaker
    
    ## 检查是否已安装
    $ git --version
    
    ## 安装
    $ wget https://github.com/git/git/archive/v2.19.2.tar.gz
    $ tar -zxvf  v2.19.2.tar.gz   // 解压
    $ mv v2.19.2.tar.gz git   //重命名
    
    ## 编译安装
    $ cd git // 进入文件夹
    $ make prefix=/usr/local/git all // 编译源码
    $ make prefix=/usr/local/git install // 安装至 /usr/local/git 路径
    
    ## 配置环境变量
    $ vim /etc/profile
    ##PATH=$PATH:/usr/local/git/bin // git 的目录
    ##export PATH
    $ source /etc/profile
    
    ## 卸载
    yum remove git

nginx指令

    启动service nginx start
    停止service nginx stop
    重启service nginx reload

百度统计

注意： baidu_analytics 不是你的百度 id 或者 百度统计 id

1. 登录 百度统计， 定位到站点的代码获取页面
2. 复制 hm.js? 后面那串统计脚本 id，如： 
3. 编辑 主题配置文件， 修改字段 baidu_analytics 字段，值设置成你的百度统计脚本 id。

NexT主题添加文章阅读量统计功能

配置LeanCloud

在注册完成LeanCloud帐号并验证邮箱之后，我们就可以登录我们的LeanCloud帐号，进行一番配置之后拿到AppID以及AppKey这两个参数即可正常使用文章阅读量统计的功能了。

创建应用

- 我们新建一个应用来专门进行博客的访问统计的数据操作。首先，打开控制台，如下图所示：
- 在出现的界面点击创建应用：
- 在接下来的页面，新建的应用名称我们可以随意输入，即便是输入的不满意我们后续也是可以更改的:
- 这里为了演示的方便，我新创建一个取名为test的应用。创建完成之后我们点击新创建的应用的名字来进行该应用的参数配置：
- 在应用的数据配置界面，左侧下划线开头的都是系统预定义好的表，为了便于区分我们新建一张表来保存我们的数据。点击左侧右上角的齿轮图标，新建Class：
在弹出的选项中选择创建Class来新建Class用来专门保存我们博客的文章访问量等数据:
点击创建Class之后，理论上来说名字可以随意取名，只要你交互代码做相应的更改即可，但是为了保证我们前面对NexT主题的修改兼容，此处的新建Class名字必须为Counter:
- 由于LeanCloud升级了默认的ACL权限，如果你想避免后续因为权限的问题导致次数统计显示不正常，建议在此处选择无限制。

创建完成之后，左侧数据栏应该会多出一栏名为Counter的栏目，这个时候我们点击顶部的设置，切换到test应用的操作界面:
在弹出的界面中，选择左侧的应用Key选项，即可发现我们创建应用的AppID以及AppKey，有了它，我们就有权限能够通过主题中配置好的Javascript代码与这个应用的Counter表进行数据存取操作了:

复制AppID以及AppKey并在NexT主题的_config.yml文件中我们相应的位置填入即可，正确配置之后文件内容像这个样子:

    leancloud_visitors:
      enable: true
      app_id: joaeuuc4hsqudUUwx4gIvGF6-gzGzoHsz
      app_key: E9UJsJpw1omCHuS22PdSpKoh

这个时候重新生成部署Hexo博客，应该就可以正常使用文章阅读量统计的功能了。需要特别说明的是：记录文章访问量的唯一标识符是文章的发布日期以及文章的标题，因此请确保这两个数值组合的唯一性，如果你更改了这两个数值，会造成文章阅读数值的清零重计。

后台管理

当你配置部分完成之后，初始的文章统计量显示为0，但是这个时候我们LeanCloud对应的应用的Counter表中并没有相应的记录，只是单纯的显示为0而已，当博客文章在配置好阅读量统计服务之后第一次打开时，便会自动向服务器发送数据来创建一条数据，该数据会被记录在对应的应用的Counter表中。

我们可以修改其中的time字段的数值来达到修改某一篇文章的访问量的目的（博客文章访问量快递提升人气的装逼利器）。双击具体的数值，修改之后回车即可保存。

- url字段被当作唯一ID来使用，因此如果你不知道带来的后果的话请不要修改。
- title字段显示的是博客文章的标题，用于后台管理的时候区分文章之用，没有什么实际作用。
- 其他字段皆为自动生成，具体作用请查阅LeanCloud官方文档，如果你不知道有什么作用请不要随意修改。

Web安全

因为AppID以及AppKey是暴露在外的，因此如果一些别用用心之人知道了之后用于其它目的是得不偿失的，为了确保只用于我们自己的博客，建议开启Web安全选项，这样就只能通过我们自己的域名才有权访问后台的数据了，可以进一步提升安全性。

选择应用的设置的安全中心选项卡:

在Web 安全域名中填入我们自己的博客域名，来确保数据调用的安全:

如果你不知道怎么填写安全域名而或者填写完成之后发现博客文章访问量显示不正常，打开浏览器调试模式，发现如下图的输出:

这说明你的安全域名填写错误，导致服务器拒绝了数据交互的请求，你可以更改为正确的安全域名或者你不知道如何修改请在本博文中留言或者放弃设置Web安全域名。

常见问题与解决

问题1：TypeError: Cannot read property 'enable_sync' of undefined

解决：在站点配置文件_config.yml下添加以下代码。

    leancloud_counter_security:
      enable_sync: true
      app_id: <app_id>
      app_key: <app_key>
      username: # Will be asked while deploying if is left blank
      password: # Recommmended to be left blank. Will be asked while deploying if is left blank

问题2：页面阅读次数：Counter not initialized! More info at console err msg.

解决1：安装hexo-leancloud-counter-security plugin，具体配置待查；不适用这种方式

解决2：将主题_config.yml如下配置中，将security改为false即可。

    leancloud_visitors:
      enable: true
      app_id: 你自己的id
      app_key: 你自己的key
      # Dependencies: https://github.com/theme-next/hexo-leancloud-counter-security
      # If you don't care about security in leancloud counter and just want to use it directly
      # (without hexo-leancloud-counter-security plugin), set `security` to `false`.
      security: true
      betterPerformance: false

开发

参考文档：https://theme-next.js.org/docs/advanced-settings/custom-files.html

