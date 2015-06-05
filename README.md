ember & cli :kiss:
========

## ember.js

首先是要简单的介绍一下，[EmberJS](emberjs.com) 是一个MVC框架，恩。

对于**Ember**，可以说是从一开始就开始关注他。那时的Ember名字叫做[Sproutcore](http://sproutcore.org)。Sproutcore是Apple的一个项目，他有两个版本，1.X 和 2.X 。1.X 版本现在还在，而 2.X 版本就是Ember的前身。Ember从Sproutcore分出去后先改名成了Amber，然后因为这个名字被占用了，就改名成了现在的Ember。

刚开始接触Ember真的是一头雾水，不明白这个框架的强大之处，因为那时候jQuery很流行，所以就不知不觉的把Ember和JQuery做比较，后来研究过一段时间的Rails才发现，这两根本就不是一个次元的东西。

之后也出了一些MVC框架，比如[Backbone](http://backbonejs.org), [Angular](http://angularjs.org)。然后就能看到大片大片的比较文章，《why i choose Ember》之类。这些框架我也稍微有所了解，怎么说呢，我不太喜欢Angular在标签里那样写，Backbone可能有些简单，不能满足需求，而Ember呢，他太大了，加载有些慢。但是我还是选择了站在Ember这边，很大一个原因是他是由**社区**驱动的，现在这个开源年代，这么做很靠谱，说不定那天google跪了Angular也就不在了。

真正喜欢Ember的原因其实是因为ES6。Ember是首先使用ES6模块的MVC框架，并且那时候源码也都改造成了ES6模块。RSVP是一个promiss库，也是由Ember核心团队的成员开发，这个也是我看中Ember的一个原因，因为是真真切切被jQuery的promiss摧残过。

**1.13**是Ember 1.X的最后一个版本，下一个版本号是从2.0开始。2.X具备了很多新的和好玩的特性，很令人期待。Canary版本现在已经是2.0，最近正在玩。

## ember-cli

要说到构建项目，那理由可是很充分，但是现在前端项目也需要构建，为什么？只有简单的css，js，html也需要去构建工具构建么？

没错，其实这都是被逼的。在日常coding中我们确实需要一些工具去辅助，比如版本上线之前的代码压缩，各类coffee、sass、less文件的编译，css、js文件和合并，并且需要监视文件改动自动刷新来保护我们的黄金F5。这些种种过分要求如果都要我们亲自一步步去实现那有点太坑，所以我们需要一个工具。

最早的构建工具可以说是[Grunt](http://gruntjs.com)。他有一些很常用的插件来完成上面说到的那些功能。第一个Ember项目kit - **Ember App Kit** 也是用Grunt作为构建工具来构建的。

Grunt之后出现了一些其他工具，如[Gulp](http://gulpjs.com)、[Broccoli](https://github.com/broccolijs/broccoli)。形象的说Gulp是水管，而Broccoli是树，但是不管是什么，他们都有一个共同点，都有各类插件来帮助完成项目的构建。而EAK之后也从Grunt改成了Broccoli。

[ember-cli](http://ember-cli.com) 从名字就可以理解，他是用命令行来快速构建项目的工具。ember-cli也是官方推荐的。那为什么要用ember-cli呢？

Ember的项目结构大家都知道，常用的有Route、controller、view、modal，根据命名规则和模块化开发，可能我们js文件有很多很多，那我们如何要快速创建呢？难道要鼠标点右键新建，或是emacs一个空文件么？使用ember-cli的话就会容易很多，比如我想创建login的controller，那只需要在终端输入:

```sh
ember g controller login
```

就会自动创建一个模板文件出来，可以说是很方便。

值得一提的是，ember-cli使用的是**Broccoli**，所以他支持Broccoli的所有插件。如果你是缩进狂魔，one line style，没有问题，coffee、sass 、emblem这些插件都可以安装使用。

但不光是Broccoli的插件，ember-cli本身有一套插件。像常用的simple-auth、locolstorage adapter等都可以通过命令行直接安装，而不需要**任何配置**。如果你玩的足够666666，你还可以自己做插件。当然，安装插件的方法我也会去介绍。

虽然emebr-cli的功能很强大，但是他还不是足够稳定，当前版本是0.2.7。

## 运行环境

ember-cli在**各种**平台都能够运行。

在例子中使用的各种环境，编辑器，包是:

* ubuntu 15.04
* nodejs 0.12.4
* npm 2.0.1
* emacs 24.0
* ember 2.0-cancay
* ember-cli 0.2.7

并且所有示例都在win下都测试过，能够正常运行。

## 感谢

* [Ember官方网站](http://emberjs.com)
* [Ember中文官网](http://emberjs.cn)
* [ember-cli官网网站](http://ember-cli.com)
* Ember QQ群 298026365
* [私人群Blisss](tencent://groupwpa/?subcmd=all&param=7B2267726F757055696E223A3132333632353231372C2274696D655374616D70223A313433333437373234367D0A)
<a href="tencent://groupwpa/?subcmd=all&param=7B2267726F757055696E223A3132333632353231372C2274696D655374616D70223A313433333437373234367D0A" title="Blisss">私人群Blisss</a>

感谢老大[@towerhe](https://github.com/towerhe)对中文社区的贡献和各位ember coder的支持。

特别感谢[@huangdandan](https://github.com/huangdandan)同学对本文的校验。

如果发现了文内错误或是不合适的地方，强烈欢迎提交PR，Issue，或者将错误告知[@yuffiy](https://github.com/yuffiy)。

