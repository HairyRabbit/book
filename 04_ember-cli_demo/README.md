# ember-cli 快速开发

ember-cli中有一个叫做**generate**的东东，用好她能大大提高打怪效率。这节我们主要来介绍她。

## 准备工作

要开场还有30秒，碾碎他们。不过在这之前让我们稍微设计一下。

我想做一个简单的关于用户的增删改查，他包括一个列表用来显示用户的头像和姓名，一个页面用来显示用户的详细信息并且有修改和删除功能，一个表单用来添加和修改用户。

按照ember-data的规则，一群用户应该使用user的复数，也就是users。如果是person要注意复数是people而不是persons，挑战英文水平的时刻到了。我们的路由根据上面的说明简单设计为：

| 动作             | 路径            | 名称  | 作用               |
| :----------------| ---------------:| :----:| :------------------|
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
      age: 18,
	  sex: false
	},{
	  avatar: '02.jpg',
	  name: 'huangdandan',
	  age: 18,
	  sex: false
	}];
  }
});

```

接下来我们来给列表模板app/templates/users/index.hbs添加内容：

```handlebars
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

完成之后看下浏览器里的变化，好像什么都没有，哪里错了么？

我们知道访问根目录`/`实际访问的路由是index，而然我们的还没有index模板。访问`/users`会看到刚才的列表：

<img src="images/demo_list.png" title="users list." />

解决办法想到了三个：

1. 在index路由里添加逻辑，在beforeModel钩子里跳转到`/user`;
2. 在index模板里放一个链接按钮;
3. 在router.js里面修改users的path路径成`/`

我们选择第一种，新建index路由：

```sh
ember g route index
```

将跳转逻辑写在beforeModel钩子里：

```javascript
// app/routes/index.js

import Ember from 'ember';

export default Ember.Route.extend({

  beforeModel() {
    this.transitionTo('users.index');
  }
});

```

页面自动刷新后看到自动跳到了`/users`，重新输入`http://localhost:4200`也会跳转。

很好，接下来我们来实现新增逻辑。修改我们的列表模板来增加一个新增用户按钮。因为这个按钮只有跳转到`users/new`这一个功能，所以用`link-to`就可以了：



创建一个新增用户的路由：

```sh
ember g route users/new
```

修改新增用户模板`app/templates/users/new.hbs`：

```handlebars
<form {{action 'doSave' on='submit'}}>
  <div>
    {{input name="avatar" id="avatar" type="file" value=avatar}}
  </div>
  <div>
    <label for="name">姓名</label>
	{{input name="name" id="name" type="text" value=name}}
  </div>
  <div>
    <label for="age">年龄</label>
	{{input name="age" id="age" type="number" value=age}}
  </div>
  <div>
    <label for="sexM">性别</label>
	<label for="sexM">男</label>
	{{input name="sex" id="sexM" type="checkbox" checked=sex}}
	<label for="sexF">女</label>
	{{input name="sex" id="sexF" type="checkbox" checked=sexInverseValue}}
  </div>
  <div>
    <button type="submit">保存</button>
  </div>
</form>
```

创建好后会自动刷新页面，点击新增用户。浏览器跳转到了`/users/new`，并且看到刚刚创建的表单。

接下来实现`doSave`逻辑，这时我们需要一个控制器了：

```sh
ember g controller users/new
```

打开app/controllers/users/new.js，提取数据并且保存：

```javascript
import Ember from 'ember';

export default Ember.Controller.extend({
  age: "18",
  sex: true,
  sexDidChange: Ember.observer('sex', function() {
    let sex = this.get('sex');
	return this.set('sexInverseValue', !sex);
  }),
  sexInverseValueDidChange: Ember.observer('sexInverseValue', function() {
    let sexInverseValue = this.get('sexInverseValue');
	return this.set('sex', !sexInverseValue);
  }),
  actions: {
    doSave() {
	  let _this = this;

      let user = this.getProperties('avatar', 'name', 'age', 'sex');

      console.log(user);
	}
  }
});
```

这个`user`要保存到哪里呢？然而列表的实体是假的，并没有什么卵用。现在要做的是从服务器端提取数据：

```sh
ember g http-mock users
```

这次生成的内容有点多。多了一个`server`文件夹，里面生成了一个`index.js`，还有一个mocks文件夹，里面有需要的`users.js`。之后通过npm添加了个依赖，分别的**morgan**、**golb**、**express**。使用过nodejs的同学一定知道express。express是一个web框架，用来处理请求和响应。打开`users.js`可以看到增删改查都齐了，只需要处理数据就可以了。这里就链接数据库了，还是使用刚才的两个假数据。

修改server/mocks/users.js部分代码：

```javascript
var users = [{
    id: 1,
	avatar: '01.jpg',
	name: 'yufi',
	age: 18,
	sex: false
  },{
    id: 2,
	avatar: '02.jpg',
	name: 'huangdandan',
	age: 18,
	sex: false
}];

usersRouter.get('/', function(req, res) {
  res.send({
    'users': users
  });
});
```

然后修改`app/users/index`路由的model钩子换成从服务器端请求：

```javascript
model() { return this.store.find('user'); }
```

把页面返回到`/users`看到页面报错了，请求`/users`报了404，可是刚才明明写了返回。没办法只能重启一下服务，按C-c两下关掉服务，然后再次重启。

发现还是什么都没，怎么回事呢？我们再来看一下`server/mocks/users.js`的最后一行：

```javascript
app.use('/api/users', usersRouter);
```

原来请求发错了地方，要发往`/api/users`，而不是`/users`。好像适配器可以解决这个问题。新建一个适配器：

```sh
ember g adapter application
```

在适配器/app/adapters/application.js里声明`namespace`：

```javascript
// app/adapters/application.js

import DS from 'ember-data';

export default DS.RESTAdapter.extend({
  namespace: 'api'
});
```

页面自动刷新后数据出来了：

<img src="images/demo_http.png" title="data form server" />

