# ember-cli 熟悉

安装好nodejs和ember-cli之后就可以愉快的开始了。在开始之前我们先来熟悉一下这个工具。

## 创建新项目

首先来让我们创建一个新项目。根据多年经验，我起了个很负责任的名字*aaa*，使用下面的命令可以快速创建：

```sh
ember new aaa
```

可以看到ember-cli会自动创建一些文件，然后又自动通过npm和bower去安装依赖，创建过程可能需要10-20分钟。

让我们看一下这些文件或文件夹都是做什么的：

.ember-cli ember-cli的配置文件，里面放一下配置信息，比如主机和端口号。
package.json npm用来安装依赖的配置文件，broccoli和ember-cli的插件名称申明在这里。通过npm安装的依赖会被放在nodo_module文件夹里。
bower.json bower用来安装依赖的配置文件，ember.js或是jQuery的版本就在这里配置，打开后我们看到ember-cli 0.2.7默认使用的ember版本是1.12。通过bower安装的依赖被放在bower_components里。
Brocflie.js broccoli的配置文件，就像Grunt和Gruntfile.js，Gulp和Gulpfile.js的关系一样，broccoli也有自己的配置文件。这个文件可能需要我们去配置。
evenment/config.js 项目的配置文件，这是第二重要的文件。开发、测试、产品环境都是在这里配置，我们自己的全局配置以及各种插件也都是在这里配置。
app文件夹 这是第一重要的，我们的ember代码就写在这个文件夹里面。
dist文件夹 这个里面是broccoli编译好的文件。今后我们打包代码也会默认放在这个文件夹里。
tmp文件夹 这是broccoli合并各种树生成的临时文件。

剩下的文件夹或文件是一些其他的配置，都很常见并且里面都有注释，不明白作用的话打开看看或是查查看就好了。

项目创建好后我们通过下面的命令开启服务：

ember s


打开浏览器访问http://localhost:4200，如果是下面的画面，恭喜你。

打开app文件夹我们可以看到ember的项目树。

app.js 整个程序入口，Ember.Application.create在这里申明。
router.js 全局路由，Ember.Router.map写在这里，我们要在这里配置所有的访问地址。
index.html 主页面。单页App嘛，当然要有一个这样的页面，打开后发现有两个钩子，他们是ember-cli和他的插件用来把各种文件引入所做的标记。

然后是各种文件夹，modal、view、controller、template、component他们的作用就和名字一样，只不过一开始除了template外都是空的。

然后我们的template文件夹里面有一个application.hbs，打开可以看到就是我们在浏览器里面看到的Welcome to Ember.js

所以说我们的项目新建了四个主要文件外加styles里的样式表，一共五个。

接下来我们通过一个简单的CRUD demo来说明ember-cli gemerate的用法。
