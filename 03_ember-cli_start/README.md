# ember-cli 快速熟悉

安装好ember-cli和各种工具之后就可以愉快的开始了。在开始之前我们先来熟悉一下这个工具。

## 创建新项目

首先来让我们创建一个新项目。根据多年经验，我起了个很负责任的名字**aaa**，使用下面的命令可以快速创建：

```sh
ember new aaa
```

<img src="../images/ember-cli_create.png" title="create new project" />

这样会新创建一个aaa的文件夹。如果是在已有的文件夹创建项目，需要使用下面的命令：

```sh
ember init
```

可以看到ember-cli会自动创建一些文件，然后又自动通过npm和bower去安装依赖，创建过程可能需要10-20分钟。安装成功之后会在命令行看到绿色的`Successfully initialized git.`

让我们看一下这些文件或文件夹都是做什么的：

* **.ember-cli** ember-cli的配置文件，里面放一下配置信息，比如主机和端口号。
* **package.json**、**node_modules** package.json是npm用来安装依赖的配置文件，broccoli和ember-cli的插件都申明在这里。通过npm安装后的依赖会被放在nodo_module文件夹里。
* **bower.json**、**bower_components**、**.bowerrc** bower.json是bower用来安装依赖的配置文件，ember.js和jQuery的版本就在这里配置，打开后我们看到ember-cli 0.2.7默认使用的ember版本是**1.12**。通过bower安装的依赖被放在bower_components里。.bowerrc文件用来设置bower安装的依赖被放置在哪个文件夹下。
* **Brocflie.js** broccoli的配置文件，就像Grunt和Gruntfile.js，Gulp和gulpfile.js的关系一样，broccoli也有自己的配置文件。这个文件用来配置broccoli相关的设置。
* **config/environment.js** 项目的配置文件，可以说这是第二重要的文件。开发、测试、产品环境都在这里配置，我们自己的全局变量以及各种插件相关配置也都在这里。
* **app文件夹** 不用说了，这是第一重要的，ember代码就写在这个文件夹里面。
* **dist文件夹** 这个里面是broccoli编译好的文件。今后我们打包代码也会默认放在这个文件夹里。
* **tests文件夹** 这个文件夹放着测试代码，用于各种测试。
* **tmp文件夹** 这里用来放置broccoli合并各种树生成的临时文件。
* **public文件夹** 这个文件夹里的文件会被直接拷贝到dist文件夹下。所以这个文件夹适合放一些静态文件，比如图片和字体。
* **vendor文件夹** 这个文件夹可以放一些不是通过npm和bower来安装的包。

剩下的文件夹或文件是一些其他的配置，都很常见并且里面都有注释，不明白作用的话打开看看或是查查看就好了。

## 运行项目

项目创建好后我们通过下面的命令开启服务：

```sh
ember s
```

这时会看到broccoli开始编译：

<img src="../images/ember-cli_serve.png" title="start server." />


编译成功之后会提示`Build successful - xxxxms.`，并且会显示合并的树和所用的时间。打开浏览器访问网址`http://localhost:4200`，如果是下面的画面，恭喜你。

<img src="../images/ff_welcome.png" title="firefox welcome page." />

## app项目结构

打开app文件夹我们可以看到项目结构树。来看一下这些文件都是做什么用的吧。

<img src="../images/app_struct.png" title="app struct." />

* **app.js** 程序入口，Ember.Application.create在这里申明。
* **router.js** 路由，Ember.Router.map写在这里，我们要在这里配置url。
* **index.html** 主页面。单页App嘛，当然要有一个这样的页面，打开后发现有四个钩子：

```hbs
{{content-for 'head'}}
{{content-for 'head-footer'}}
{{content-for 'body'}}
{{content-for 'body-footer'}}
```

他们是ember-cli和他的插件用来把各种文件引入的钩子。

然后是各种文件夹，modals、views、controllers、templates、components等等等。他们的作用就和名字一样，只不过一开始除了templates外，其他都是空的。

然后我们的templates文件夹里面有一个模板文件application.hbs。打开后可以看到就是我们在浏览器里面看到的**Welcome to Ember.js**。

所以说我们的项目新建了四个主要文件外加styles里的样式表，一共五个。

## summary

可以看到ember-cli采用了ES6的模块来引入和导出模块。由于ember-cli使用了babel，所以ES6的好多东西都可以直接编译过来，也给我们提供了一个学习ES6的机会。

在熟悉之后，接下来我们通过一个简单的CRUD demo来说明ember-cli gemerate的用法。
