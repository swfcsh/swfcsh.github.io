---
layout: mypost
title: Hello World
categories: [分享]
extMath: false
---

#### 写在前面

学期结束了，这一个阶段也算是告一段落了吧。

之前就一直有建个人博客的打算，倒也不是说正儿八经的博客，只不过是想有个地方能记录一下罢了。这件事情拖了又拖，找了一堆理由和借口，就是不肯开始。

今年是没法回家过年了，也是长这么大第一次不在家过年吧。正好闲来无事，想的也比较多，毕竟以后的事谁知道呢？二十多年的经历，可以成为故事的、需要成为秘密藏在字里行间的，又积累了不少，如果再拖下去，就觉得太过浪费了。

正是因为如此，我才需要找到一种记录的方式，文字、图片、声音，那些显得非常自我的东西，把自己的情绪都藏在文字之中，毕竟如果没办法留下记录的人生又得多么的无聊啊！

Google搜索一圈，发现使用`Jekyll + Github Pages`这一套框架来搭建个人博客比较成熟且容易上手。

好了，这就开始！

---

#### 开启 Github Pages

首先我们用自己的 Github 账号创建一个新的库（repository），这个库的名称有固定的格式： `username.github.io`，其中 `usernam`e 必须是 Github 账户的用户名，`.github.io` 是固定的，这个地址将会成为个人站点的网站地址。另外，我们可以勾选Initialize this repository with a README，让仓库自动创建一个 README.md 文件。

创建完成后，进入所创建的库，在`settings`页面找到`GitHub Pages`进行设置，如果你的库有按照上述方式进行命名，则它会自动进行设置，设置成功后会该页面出现绿色的提示。

#### Jekyll 特点

Jekyll 的核心是一个文本转换引擎。它的方便之处在于支持多种文本标记语言：Markdown，Textile，HTML，然后 Jekyll 就会帮你加入你选择主题的样式的布局中。最终生成你自己的静态博客网站。

#### Jekyll 架构

一个基本的 Jekyll 网站的目录结构一般是像这样的：

```
.
├── assets # 存放用于线上环境的静态资源，比如我们想放在博客上的图片之类
├── _config.yml # 配置文件，我们通过修改这里的参数改造博客
├── _data
|   └── members.yml
├── _drafts # 未发布的文章。这些文件的格式中都没有title.MARKUP数据。
|   ├── begin-with-the-crazy-ideas.md
|   └── on-simplicity-in-technology.md
└── index.html # 模板首页
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts # 用于存放博客文章的文件夹，文件格式必须符合: 年-月-日-文章标题.md
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
|   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
|   ├── _base.scss
|   └── _layout.scss
├── _site
├── .jekyll-metadata

```

#### Jekyll 运行环境的配置与安装

运行 Jekyll 所需的环境如下：

- Ruby
- Ruby Gems
- NodeJS或其他 JavaScript 运行环境
- Python2.7(或2.7以上版本）

由于网络上大部分教程都是在Linux/MacOS上配置并安装Jekyll ，看起来操作也比较简单，也比较推荐大家用Linux/MacOS作为配置环境。

ruby安装：
```shell
sudo apt-get install ruby-full
```
安装完成后可以用命令行执行`ruby -v`和`gem -v`检测是否安装成功。

jeyyll安装：
```shell
gem install jekyll bundler
```

详细信息可以参考 [官方文档](https://www.jekyll.com.cn/docs/installation/ubuntu/)

#### Jekyll 主题

我使用了[TMaize](https://github.com/TMaize/tmaize-blog)主题进行二次开发，直接到主题仓库将代码`git clone`到本地。

通过下面命令编译/启动项目

```shell
bundle exec jekyll build --destination=dist
bundle exec jekyll serve --host=127.0.0.1 --port=8080 --livereload
```
然后打开浏览器输入`127.0.0.1:8080`即可在本地打开博客进行调试

#### Jekyll 项目配置

1. 如果使用自己的域名，`CNAME`文件里的内容请换成你自己的域名，然后 CNAME 解析到`用户名.github.com`

2. 如果使用 GitHub 的的域名，请删除`CNAME`文件，然后把你的项目修改为`用户名.github.io`

3. 修改`pages/about.md`中关于我的内容

4. 修改`_config.yml`文件，具体作用请参考注释

5. 清空`posts`和`_posts`目录下所有文件，注意是清空，不是删除这两个目录

6. 网站的 logo 和 favicon 放在了`static/img/`下，替换即可，大小无所谓，图片比例最好是 1:1


#### 博客内容编写

文章放在`_posts`目录下，命名为`yyyy-MM-dd-xxxx-xxxx.md`，内容格式如下

```yaml
---
layout: mypost
title: 标题
categories: [分类1, 分类2]
---
文章内容，Markdown格式
```

文章资源放在`posts`目录，如文章文件名是`2018-01-01-theme-usage.md`，则该篇文章的资源需要放在`posts/2018/01/01`下，在文章使用时直接引用即可。当然了，写作的时候会提示资源不存在忽略即可

```md
![这是图片](xxx.png)

[xxx.zip 下载](xxx.zip)
```

一般提交到 github 过个几十秒就可以看到效果。


#### 使用cloudflare加速

由于Github Pages 服务器在国外，国内访问速度非常慢，而且近期`github.io`的域名经常被干扰解析成`127.0.0.1`，所以套一层 cloudflare CDN可以提升国内博客访问速度，虽然它在国内没有CDN节点，但是整体效果还是要比`github.io`好的。

使用cloudflare首先需要一个域名，可以在阿里云、腾讯云等官网买一个。配置好后在cloudflare页面设置一下就行。具体步骤很简单这边就不再赘述了，可以到[官网](https://dash.cloudflare.com/sign-up
)参考官方文档。

#### 参考

https://www.jekyll.com.cn/docs/

https://docs.github.com/zh/pages/quickstart

https://github.com/TMaize/tmaize-blog

https://developers.cloudflare.com/dns/zone-setups/full-setup/setup/

---

#### 写在最后

总的来说用这一套框架搭建一个简单的个人博客还是挺简单的，流程并不多而且网上相关文档已经很完善了。

但是难的本来就不是把博客建起来，而是能有持续的内容输出。

我希望这个小角落能记录下有趣的经历、人生的感悟、对过去或未来的吐槽，我想我需要这么一个记录生活和随想的地方，毕竟三年前写过的东西，三年后重新感悟，又是另一个完全不同的状态。

在一个不会倒退的时间平面上，去经历相同的仿佛只有一个纬度的空间，却能有好几种完全不同的人生感悟。

但是过去的就是过去了，就算有无数个关于「如果」的猜测，都再也回不去了。

最后的最后，Do have faith in what you're doing.



---


