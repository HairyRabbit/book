# ember-cli 快速开发

ember-cli中有一个叫做**generate**的东东，用好她能大大提高打怪效率。这节我们主要来介绍她。

## 准备工作

要开场还有30秒，碾碎他们。不过在这之前让我们稍微设计一下。

我想做一个简单的关于用户的增删改查，他包括一个列表用来显示用户的头像和姓名，一个页面用来显示用户的详细信息并且有修改和删除功能，一个表单用来添加和修改用户。

按照ember-data的规则，一群用户应该使用user的复数，也就是users。如果是person要注意复数是people而不是persons，挑战英文水平的时刻到了。我们的路由根据上面的说明简单设计为：

| 动作             | 路径            | 名称  | 作用               |
| :----------------|:---------------:|:-----:|:-------------------|
| 初始加载         | /users/index    | index | 所有用户           |
| 点击新增用户按钮 | /users/new      | new   | 新增用户           |
| 点击列表中的某只 | /users/:id      | user  | 显示用户的详细内容 |
| 点击详细修改按钮 | /users/:id/edit | edit  | 修改用户           |

这就是我们的路径规则，先不着急修改router.js。

接下来设计一下用户模型，很简单，这里只需要姓名name、性别sex和年龄age和头像avatar四个字段。

我们用ember generate来创建模板，在命令行输入下面命令：

```sh
ember g model user
```

完成后我们看到ember-cli为我们生成了两个文件，一个就是user.js，他放在app/models里，一个是他的测试文件，放在tests/unit/models下面。打开app/models/user.js定义模型：

```javascript
// app/models/user.js

import DS from 'ember-data';

let attr = DS.attr;

export default DS.Model.extend({

  avatar: attr('string'), // 头像
  name: attr('string'), // 姓名
  age: attr('number'), // 年龄
  sex: attr('boolean') // 性别 true: male, false: female
  
});
```

接下来我们先来实现列表的逻辑，为此我们首先准备一组假数据：

```javascript
[{
  avatar: '01.jpg',
  name: 'yufi',
  age: 999,
  sex: false
},{
  avatar: '02.jpg',
  name: 'huangdandan',
  age: 997,
  sex: false
}]
```

还是使用generate来生成路由：

ember g router users/index

这次看到生成了三个文件，除了路由，还生成了模板，这就是ember-cli贴心的地方，他知道你一定会去修改模板，所以提前为你生成。当然贴心的还不止这些，是时候解释刚才不着急修改router.js的原因了。打开router.js我们可以看到使用generate后ember-cli会自动修改路由。然而这里要注意，因为我们刚才使用的是users/index，所以不会自动为你创建index路由，原因是ember**约定**index的路径就是**/**。但是其他文件夹会创建index文件。

如果这里已经提前建好了模板，ember-cli会询问你是否需要重写，根据需要输入y或者n就可以了。

将我们的假数据写在app/routes/users/index.js的model钩子里：

```javascript
// app/routes/user/index.js

import Ember from 'ember';

export default Ember.Route.extend({

  model() {
    return [{
      avatar: '01.jpg',
      name: 'yufi',
      age: 999,
	  sex: false
	},{
	  avatar: '02.jpg',
	  name: 'huangdandan',
	  age: 997,
	  sex: false
	}];
  }
});

```

接下来我们来给列表模板app/templates/users/index.hbs添加内容：

```handlebar
<ul>
  {{#each model as |user|}}
  <li>
    <div>
	  <span><img src={{user.avatar}} /></span>
	  <span>{{user.name}}</span>
    </div>
  </li>
  {{/each}}
</ul>
```

完成之后看下浏览器里的变化：

很好，接下来我们来实现新增逻辑。修改我们的列表模板来增加一个新增用户按钮：
