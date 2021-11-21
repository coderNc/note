# JSX核心语法

## 一. ES6的class

> 虽然目前React开发模式中更加流行hooks，但是依然有很多的项目依然是使用类组件（包括AntDesign库中）；

### 1.1. 类的定义

在ES6之前，我们通过function来定义类，但是这种模式一直被很多从其他编程语言（比如Java、C++、OC等等）转到JavaScript的人所不适应。

原因是，大多数面向对象的语言，都是使用class关键字来定义类的。

而JavaScript也从ES6开始引入了class关键字，用于定义一个类。

ES6之前定义一个Person类：

```jsx
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.running = function() {
  console.log(this.name + this.age + "running");
}

var p = new Person("why", 18);
p.running();
```

转换成ES6中的类如何定义呢？

- 类中有一个constructor构造方法，当我们通过new关键字调用时，就会默认执行这个构造方法

- - 构造方法中可以给当前对象添加属性

- 类中也可以定义其他方法，这些方法会被放到Person类的prototype上

```jsx
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  running() {
    console.log(this.name + this.age + "running");
  }
}

const p = new Person("why", 18);
p.running();
```

另外，属性也可以直接定义在类中：

- height和address是直接定义在类中

```jsx
class Person {
  height = 1.88;
  address = "北京市";

  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  studying() {
    console.log(this.name + this.age + "studying");
  }
}
```

### 1.2. 类的继承

继承是面向对象的一大特性，可以减少我们重复代码的编写，方便公共内容的抽取（也是很多面向对象语言中，多态的前提）。

ES6中增加了extends关键字来作为类的继承。

我们先写两个类没有继承的情况下，它们存在的重复代码：

- Person类和Student类

```jsx
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  running() {
    console.log(this.name, this.age, "running");
  }
}

class Student {
  constructor(name, age, sno, score) {
    this.name = name;
    this.age = age;
    this.sno = sno;
    this.score = score;
  }

  running() {
    console.log(this.name, this.age, "running");
  }

  studying() {
    console.log(this.name, this.age, this.sno, this.score, "studing");
  }
}
```

我们可以使用继承来简化代码：

- 注意：在constructor中，子类必须通过super来调用父类的构造方法，对父类进行初始化，否则会报错。

```jsx
class Student1 extends Person {
  constructor(name, age, sno, score) {
    super(name, age);
    this.sno = sno;
    this.score = score;
  }

  studying() {
    console.log(this.name, this.age, this.sno, this.score, "studing");
  }
}

const stu1 = new Student1("why", 18, 110, 100);
stu1.studying();
```

## 二. 案例练习

### 2.1. 列表展示

真实开发中，我们的数据通常会从服务器获取，比较常见的是获取一个列表数据，保存到一个数组中进行展示

- 比如现在有一个电影列表，我们如何通过React进行展示呢？

我们还是通过一个组件来完成：

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      movies: ["星际穿越", "大话西游", "盗梦空间", "少年派"]
    }
  }

  render() {
    // var movieLis = [];
    // for (var i in this.state.movies) {
    //   movieLis.push((<li>{this.state.movies[i]}</li>));
    // }

    return (
      <div>
        <h2>电影列表</h2>
        <ul>
          {
            this.state.movies.map((item, index) => {
              return (<li>{item}</li>)
            })
          }
        </ul>
      </div>
    )
  }
}

ReactDOM.render(<App/>, document.getElementById("app"));
```

### 2.2. 计数器案例

电影列表的案例中并没有交互，我们再来实现一个计数器的案例：

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      counter: 0
    }
  }

  render() {
    return (
      <div>
        <h2>当前计数:{this.state.counter}</h2>
        <button onClick={this.increment.bind(this)}>+1</button>
        <button onClick={this.decrement.bind(this)}>-1</button>
      </div>
    )
  }

  increment() {
    this.setState({
      counter: this.state.counter+1
    })
  }

  decrement() {
    this.setState({
      counter: this.state.counter-1
    })
  }
}

ReactDOM.render(<App/>, document.getElementById("app"));
```

## 三. JSX语法解析

### 3.1. 认识JSX的语法

我们先来看一段代码：

- 这段element变量的声明右侧赋值的标签语法是什么呢？

- - 它不是一段字符串（因为没有使用引号包裹），它看起来是一段HTML原生，但是我们能在js中直接给一个变量赋值html吗？
  - 其实是不可以的，如果我们将 `type="text/babel"` 去除掉，那么就会出现语法错误；
  - 它到底是什么呢？其实它是一段jsx的语法；

```jsx
<script type="text/babel">
  const element = <h2>Hello World</h2>
 ReactDOM.render(element, document.getElementById("app"));
</script>
```

JSX是什么？

- JSX是一种JavaScript的语法扩展（eXtension），也在很多地方称之为JavaScript XML，因为看起就是一段XML语法；
- 它用于描述我们的UI界面，并且其完全可以和JavaScript融合在一起使用；
- 它不同于Vue中的模块语法，你不需要专门学习模块语法中的一些指令（比如v-for、v-if、v-else、v-bind）；

为什么React选择了JSX？

- React认为渲染逻辑本质上与其他UI逻辑存在内在耦合

- - 比如UI需要绑定事件（button、a原生等等）；
  - 比如UI中需要展示数据状态，在某些状态发生改变时，又需要改变UI；

- 他们之间是密不可分，所以React没有将标记分离到不同的文件中，而是将它们组合到了一起，这个地方就是组件（Component）；

- - 当然，后面我们还是会继续学习更多组件相关的东西；

- 在这里，我们只需要知道，JSX其实是嵌入到JavaScript中的一种结构语法；

JSX的书写规范：

- JSX的顶层**只能有一个根元素**，所以我们很多时候会在外层包裹一个div原生（或者使用后面我们学习的Fragment）；

- 为了方便阅读，我们通常在jsx的外层包裹一个小括号()，这样可以方便阅读，并且jsx可以进行换行书写；

- JSX中的标签可以是单标签，也可以是双标签；

- - 注意：如果是单标签，必须以/>结尾；

JSX的本质，我们后面再来讨论；

### 3.2. JSX嵌入表达式

如果我们jsx中的内容是动态的，我们可以通过表达式来获取：

- 书写规则：{表达式}
- 大括号内可以是变量、字符串、数组、函数调用等任意js表达式；

#### 3.2.1. jsx中的注释

jsx是嵌入到JavaScript中的一种语法，所以在编写注释时，需要通过JSX的语法来编写：

```jsx
<div>
  {/* 我是一段注释 */}
  <h2>Hello World</h2>
</div>
```

#### 3.2.2. JSX嵌入变量

- 情况一：当变量是Number、String、Array类型时，可以直接显示

- 情况二：当变量是null、undefined、Boolean类型时，内容为空；

- - 如果希望可以显示null、undefined、Boolean，那么需要转成字符串；
  - 转换的方式有很多，比如toString方法、和空字符串拼接，String(变量)等方式；

- 情况三：对象类型不能作为子元素（not valid as a React child）

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      name: "why",
      age: 18,
      hobbies: ["篮球", "唱跳", "rap"],
      
      test1: null,
      test2: undefined,
      flag: false,

      friend: {
        name: "kobe",
        age: 40
      }
    }
  }

  render() {
    return (
      <div>
        {/* 我是一段注释 */}
        <h2>Hello World</h2>
      </div>

      <div>
        {/* 1.可以直接显示 */}
        <h2>{this.state.name}</h2>
        <h2>{this.state.age}</h2>
        <h2>{this.state.hobbies}</h2>

        
        {/* 2.不显示 */}
        <h2>{this.state.test1}</h2>
        <h2>{this.state.test1 + ""}</h2>
        <h2>{this.state.test2}</h2>
        <h2>{this.state.test2 + ""}</h2>
        <h2>{this.state.flag}</h2>
        <h2>{this.state.flag + ""}</h2>
        
        {/* 3.不显示 */}
        <h2>123{this.state.friend}</h2>
      </div>
    )
  }
}

ReactDOM.render(<App/>, document.getElementById("app"));
```

**补充：为什么null、undefined、Boolean在JSX中要显示为空内容呢？**

原因是在开发中，我们会进行很多的判断；

- 在判断结果为false时，不显示一个内容；
- 在判断结果为true时，显示一个内容；

这个时候，我们可以编写如下代码：

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      flag: false
    }
  }

  render() {
    return (
      <div>
        {this.state.flag ? <h2>我是标题</h2>: null}
        {this.state.flag && <h2>我是标题</h2>}
      </div>
    )
  }
}
```

#### 3.3.3. JSX嵌入表达式

JSX中，也可以是一个表达式。

这里我们演练三个，其他的大家在开发中灵活运用：

- 运算表达式
- 三元运算符
- 执行一个函数

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      firstName: "kobe",
      lastName: "bryant",
      age: 20
    }
  }

  render() {
    return (
      <div>
        {/* 运算表达式 */}
        <h2>{this.state.firstName + " " + this.state.lastName}</h2>
        {/* 三元运算符 */}
        <h2>{this.state.age >= 18 ? "成年人": "未成年人"}</h2>
        {/* 执行一个函数 */}
        <h2>{this.sayHello("kobe")}</h2>
      </div>
    )
  }

  sayHello(name) {
    return "Hello " + name;
  }
}
```

#### 3.3.4. jsx绑定属性

很多时候，描述的HTML原生会有一些属性，而我们希望这些属性也是动态的：

- 比如元素都会有title属性

- 比如img元素会有src属性

- 比如a元素会有href属性

- 比如元素可能需要绑定class

- - 注意：绑定class比较特殊，因为class在js中是一个关键字，所以jsx中不允许直接写class
  - 写法：使用className替代

- 比如原生使用内联样式style

- - style后面跟的是一个对象类型，对象中是样式的属性名和属性值；
  - 注意：这里会讲属性名转成驼峰标识，而不是连接符-；

我们来演示一下属性的绑定：

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      title: "你好啊",
      imgUrl: "https://upload.jianshu.io/users/upload_avatars/1102036/c3628b478f06.jpeg?imageMogr2/auto-orient/strip|imageView2/1/w/240/h/240",
      link: "https://www.baidu.com",
      active: false
    }
  }

  render() {
    return (
      <div>
        <h2 title={this.state.title}>Hello World</h2>
        <img src={this.state.imgUrl} alt=""/>
        <a href={this.state.link} target="_blank">百度一下</a>
        <div className={"message " + (this.state.active ? "active": "")}>你好啊</div>
        <div className={["message", (this.state.active ? "active": "")].join(" ")}>你好啊</div>
        <div style={{fontSize: "30px", color: "red", backgroundColor: "blue"}}>我是文本</div>
      </div>
    )
  }
}
```

### 3.3. jsx事件监听

#### 3.3.1. 和原生绑定区别

如果原生DOM原生有一个监听事件，我们可以如何操作呢？

- 方式一：获取DOM原生，添加监听事件；
- 方式二：在HTML原生中，直接绑定onclick；

我们这里演练一下方式二：

- `btnClick()`这样写的原因是onclick绑定的后面是跟上JavaScript代码；

```jsx
<button onclick="btnClick()">点我一下</button>
<script>
  function btnClick() {
  console.log("按钮发生了点击");
}
</script>
```

在React中是如何操作呢？

我们来实现一下React中的事件监听，这里主要有两点不同

- React 事件的命名采用小驼峰式（camelCase），而不是纯小写；
- 我们需要通过{}传入一个事件处理函数，这个函数会在事件发生时被执行；

```jsx
class App extends React.Component {
  render() {
    return (
      <div>
        <button onClick={this.btnClick}>点我一下(React)</button>
      </div>
    )
  }

  btnClick() {
    console.log("React按钮点击了一下")
  }
}
```

#### 3.3.2. this绑定问题

在事件执行后，我们可能需要获取当前类的对象中相关的属性：

- 比如我们这里打印：`this.state.message`

- - 但是这里会报错：`Cannot read property 'state' of undefined`
  - 原因是this在这里是undefined

- 如果我们这里直接打印this，也会发现它是一个undefined

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      message: "你好啊,李银河"
    }
  }

  render() {
    return (
      <div>
        <button onClick={this.btnClick}>点我一下(React)</button>
      </div>
    )
  }

  btnClick() {
    console.log(this);
    console.log(this.state.message);
  }
}
```

为什么是undefined呢？

- 原因是`btnClick`函数并不是我们主动调用的，而且当button发生改变时，React内部调用了`btnClick`函数；
- 而它内部调用时，并不知道要如何绑定正确的this；

**如何解决this的问题呢？**

**方案一：bind给btnClick显示绑定this**

在传入函数时，我们可以主动绑定this：

- 这里我们主动将btnClick中的this通过bind来进行绑定（显示绑定）
- 那么之后React内部调用btnClick函数时，就会有一个this，并且是我们绑定的this；

```jsx
<button onClick={this.btnClick.bind(this)}>点我一下(React)</button>
```

但是呢，如果我有两个函数都需要用到btnClick的绑定：

- 我们发现 `bind(this)` 需要书写两遍；

```jsx
<button onClick={this.btnClick.bind(this)}>点我一下(React)</button>
<button onClick={this.btnClick.bind(this)}>也点我一下(React)</button>
```

这个我们可以通过在构造方法中直接给this.btnClick绑定this来解决：

- 注意查看 `constructor` 中我们的操作：`this.btnClick = this.btnClick.bind(this);`

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      message: "你好啊,李银河"
    }

    this.btnClick = this.btnClick.bind(this);
  }

  render() {
    return (
      <div>
        <button onClick={this.btnClick}>点我一下(React)</button>
        <button onClick={this.btnClick}>也点我一下(React)</button>
      </div>
    )
  }

  btnClick() {
    console.log(this);
    console.log(this.state.message);
  }
}
```

**方案二：使用 ES6 class fields 语法**

你会发现我这里将btnClick的定义变成了一种赋值语句：

- 这是ES6中给类定义属性的方法，称之为class fields语法；
- 因为这里我们赋值时，使用了箭头函数，所以在当前函数中的this会去上一个**作用域**中查找；
- 而上一个作用域中的this就是当前的对象；

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      message: "你好啊,李银河"
    }
  }

  render() {
    return (
      <div>
        <button onClick={this.btnClick}>点我一下(React)</button>
        <button onClick={this.btnClick}>也点我一下(React)</button>
      </div>
    )
  }

  btnClick = () => {
    console.log(this);
    console.log(this.state.message);
  }
}
```

**方案三：事件监听时传入箭头函数（推荐）**

因为 `onClick` 中要求我们传入一个函数，那么我们可以直接定义一个箭头函数传入：

- 传入的箭头函数的函数体是我们需要执行的代码，我们直接执行 `this.btnClick()`；
- `this.btnClick()`中通过this来指定会进行隐式绑定，最终this也是正确的；

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      message: "你好啊,李银河"
    }
  }

  render() {
    return (
      <div>
        <button onClick={() => this.btnClick()}>点我一下(React)</button>
        <button onClick={() => this.btnClick()}>也点我一下(React)</button>
      </div>
    )
  }

  btnClick() {
    console.log(this);
    console.log(this.state.message);
  }
}
```

#### 3.3.3. 事件参数传递

在执行事件函数时，有可能我们需要获取一些参数信息：比如event对象、其他参数

情况一：获取event对象

- 很多时候我们需要拿到event对象来做一些事情（比如阻止默认行为）
- 假如我们用不到this，那么直接传入函数就可以获取到event对象；

```jsx
class App extends React.Component {
  constructor(props) {

  render() {
    return (
      <div>
        <a href="http://www.baidu.com" onClick={this.btnClick}>点我一下</a>
      </div>
    )
  }

  btnClick(e) {
    e.preventDefault();
    console.log(e);
  }
}
```

情况二：获取更多参数

- 有更多参数时，我们最好的方式就是传入一个箭头函数，主动执行的事件函数，并且传入相关的其他参数；

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      names: ["衣服", "鞋子", "裤子"]
    }
  }

  render() {
    return (
      <div>
        <a href="http://www.baidu.com" onClick={this.aClick}>点我一下</a>

        {
          this.state.names.map((item, index) => {
            return (
              <a href="#" onClick={e => this.aClick(e, item, index)}>{item}</a>
            )
          })
        }
      </div>
    )
  }

  aClick(e, item, index) {
    e.preventDefault();
    console.log(item, index);
    console.log(e);
  }
}
```

## 四. 条件渲染

某些情况下，界面的内容会根据不同的情况显示不同的内容，或者决定是否渲染某部分内容：

- 在vue中，我们会通过指令来控制：比如v-if、v-show；
- 在React中，所有的条件判断都和普通的JavaScript代码一致；

常见的条件渲染的方式有哪些呢？

### 4.1. 条件判断语句

一种方式是当逻辑较多时，通过条件判断：

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      isLogin: true
    }
  }

  render() {
    let titleJsx = null;
    if (this.state.isLogin) {
      titleJsx = <h2>欢迎回来~</h2>
    } else {
      titleJsx = <h2>请先登录~</h2>
    }

    return (
      <div>
        {titleJsx}
      </div>
    )
  }
}
```

当然，我们也可以将其封装到一个独立的函数中：

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      isLogin: true
    }
  }

  render() {
    return (
      <div>
        {this.getTitleJsx()}
      </div>
    )
  }

  getTitleJsx() {
    let titleJsx = null;
    if (this.state.isLogin) {
      titleJsx = <h2>欢迎回来~</h2>
    } else {
      titleJsx = <h2>请先登录~</h2>
    }
    return titleJsx;
  }
}
```

### 4.2. 三元运算符

另外一种实现条件渲染的方法就是三元运算符：`condition ? true : false;`

三元运算符适用于没有太多逻辑的代码：只是根据不同的条件直接返回不同的结果

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      isLogin: true
    }
  }

  render() {
    return (
      <div>
        <h2>{this.state.isLogin ? "欢迎回来~": "请先登录~"}</h2>
        <button onClick={e => this.loginBtnClick()}>{this.state.isLogin ? "退出": "登录"}</button>
      </div>
    )
  }

  loginBtnClick() {
    this.setState({
      isLogin: !this.state.isLogin
    })
  }
}
```

### 4.3. 与运算符&&

在某些情况下，我们会遇到这样的场景：

- 如果条件成立，渲染某一个组件；
- 如果条件不成立，什么内容也不渲染；

如果我们使用三元运算符，是如何做呢？

```jsx
{this.state.isLogin ? <h2>{this.state.username}</h2>: null}
```

其实我们可以通过`逻辑与&&`来简化操作：

```jsx
{this.state.isLogin && <h2>{this.state.username}</h2>}
```

### 4.4. v-show效果

针对一个HTML原生，渲染和不渲染之间，如果切换的非常频繁，那么会相对比较损耗性能：

- 在开发中，其实我们可以通过display的属性来控制它的显示和隐藏；
- 在控制方式在vue中有一个专门的指令：v-show；
- React没有指令，但是React会更加灵活（灵活带来的代价就是需要自己去实现）；

我来看一下如何实现：

```jsx
  render() {
    const { isLogin, username } = this.state;
    const nameDisplay = isLogin ? "block": "none";

    return (
      <div>
        <h2 style={{display: nameDisplay}}>{username}</h2>
        <button onClick={e => this.loginBtnClick()}>{isLogin ? "退出": "登录"}</button>
      </div>
    )
  }
```

## 五. jsx列表渲染

### 5.1. 列表渲染

真实开发中我们会从服务器请求到大量的数据，数据会以列表的形式存储：

- 比如歌曲、歌手、排行榜列表的数据；
- 比如商品、购物车、评论列表的数据；
- 比如好友消息、动态、联系人列表的数据；

在React中并没有像Vue模块语法中的v-for指令，而且需要我们通过JavaScript代码的方式组织数据，转成JSX：

- 很多从Vue转型到React的同学非常不习惯，认为Vue的方式更加的简洁明了；
- 但是React中的JSX正是因为和JavaScript无缝的衔接，让它可以更加的灵活；
- 另外我经常会提到React是真正可以提高我们编写代码能力的一种方式；

如何展示列表呢？

- 在React中，展示列表最多的方式就是使用数组的map高阶函数；

数组的map函数语法如下：

- callback：生成新数组元素的函数，使用三个参数：

- - `currentValue`

    `callback` 数组中正在处理的当前元素。

  - `index`可选

    `callback` 数组中正在处理的当前元素的索引。

  - `array`可选

    `map` 方法调用的数组。

- `thisArg`可选：执行 `callback` 函数时值被用作`this`。

```jsx
var new_array = arr.map(function callback(currentValue[, index[, array]]) {
 // Return element for new_array 
}[, thisArg])
```

我们来演练一下之前的案例：

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      movies: ["盗梦空间", "大话西游", "流浪地球", "少年派", "食神", "美人鱼", "海王"]
    }
  }

  render() {
    return (
      <div>
        <h2>电影列表</h2>
        <ul>
          {
            this.state.movies.map(item => {
              return <li>{item}</li>
            })
          }
        </ul>
      </div>
    )
  }
}

ReactDOM.render(<App/>, document.getElementById("app"));
```

### 5.2. 数组处理

很多时候我们在展示一个数组中的数据之前，需要先对它进行一些处理：

- 比如过滤掉一些内容：filter函数
- 比如截取数组中的一部分内容：slice函数

比如我当前有一个数组中存放了一系列的数字：[10, 30, 120, 453, 55, 78, 111, 222]

案例需求：获取所有大于50的数字，并且展示前3个数组

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      numbers: [10, 30, 120, 453, 55, 78, 111, 222]
    }
  }

  render() {
    return (
      <div>
        <h2>数字列表</h2>
        <ul>
          {
            this.state.numbers.filter(item => item >= 50).slice(0, 3).map(item => {
              return <li>{item}</li>
            })
          }
        </ul>
      </div>
    )
  }
}

ReactDOM.render(<App/>, document.getElementById("app"));
```

### 5.3. 列表的key

我们会发现在前面的代码中只要展示列表都会报一个警告：

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)列表展示警告

这个警告是告诉我们需要在列表展示的jsx中添加一个key。

至于如何添加一个key，为什么要添加一个key，这个我们放到后面讲解setState时再来讨论；

## 六. JSX原理解析

### 6.1. JSX转换本质

实际上，jsx 仅仅只是 `React.createElement(component, props, ...children)` 函数的语法糖。

- 所有的jsx最终都会被转换成`React.createElement`的函数调用。

React.createElement在源码的什么位置呢？

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)React.createElement源码

createElement需要传递三个参数：

- 参数一：type

- - 当前ReactElement的类型；
  - 如果是标签元素，那么就使用字符串表示 “div”；
  - 如果是组件元素，那么就直接使用组件的名称；

- 参数二：config

- - 所有jsx中的属性都在config中以对象的属性和值的形式存储

- 参数三：children

- - 存放在标签中的内容，以children数组的方式进行存储；
  - 当然，如果是多个元素呢？React内部有对它们进行处理，处理的源码在下方

对children进行的处理：

- 从第二个参数开始，将其他所有的参数，放到props对象的children中

```jsx
const childrenLength = arguments.length - 2;
if (childrenLength === 1) {
  props.children = children;
} else if (childrenLength > 1) {
  const childArray = Array(childrenLength);
  for (let i = 0; i < childrenLength; i++) {
    childArray[i] = arguments[i + 2];
  }
  if (__DEV__) {
    if (Object.freeze) {
      Object.freeze(childArray);
    }
  }
  props.children = childArray;
}
```

真实的转换过程到底长什么样子呢？我们可以从多个角度来查看。

#### 6.1.1. Babel官网查看

我们知道默认jsx是通过babel帮我们进行语法转换的，所以我们之前写的jsx代码都需要依赖babel。

- 可以在babel的官网中快速查看转换的过程：https://babeljs.io/repl/#?presets=react

在这里我们编写一些jsx代码，来查看运行后的结果：

```jsx
<div className="app">
  <div className="header">
    <h1 title="标题">我是网站标题</h1>
  </div>
  <div className="content">
    <h2>我是h2元素</h2>
    <button onClick={e => console.log("+1")}>+1</button>
    <button onClick={e => console.log("+1")}>-1</button>
  </div>
  <div className="footer">
    <p>我是网站的尾部</p>
  </div>
</div>
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)babel转换

#### 6.1.2. 编写createElement

还有一种办法是我们自己来编写React.createElement代码：

```jsx
class App extends React.Component {
  constructor(props) {
  render() {
    /*#__PURE__*/
    const result = React.createElement("div", {
      className: "app"
    }, /*#__PURE__*/React.createElement("div", {
      className: "header"
    }, /*#__PURE__*/React.createElement("h1", {
      title: "\u6807\u9898"
    }, "\u6211\u662F\u7F51\u7AD9\u6807\u9898")), /*#__PURE__*/React.createElement("div", {
      className: "content"
    }, /*#__PURE__*/React.createElement("h2", null, "\u6211\u662Fh2\u5143\u7D20"), /*#__PURE__*/React.createElement("button", {
      onClick: e => console.log("+1")
    }, "+1"), /*#__PURE__*/React.createElement("button", {
      onClick: e => console.log("+1")
    }, "-1")), /*#__PURE__*/React.createElement("div", {
      className: "footer"
    }, /*#__PURE__*/React.createElement("p", null, "\u6211\u662F\u7F51\u7AD9\u7684\u5C3E\u90E8")));
    return result;
  }
}

ReactDOM.render(React.createElement(App, null) , document.getElementById("app"));
```

上面的整个代码，我们就没有通过jsx来书写了，界面依然是可以正常的渲染。

另外，在这样的情况下，你还需要babel相关的内容吗？不需要了

- 所以，`type="text/babel"`可以被我们删除掉了；
- 所以，`<script src="../react/babel.min.js"></script>`可以被我们删除掉了；

### 6.2. 虚拟DOM

#### 6.2.1. 虚拟DOM的创建过程

我们通过 `React.createElement` 最终创建出来一个 ReactElement对象：

```jsx
return ReactElement(
  type,
  key,
  ref,
  self,
  source,
  ReactCurrentOwner.current,
  props,
);
```

这个ReactElement对象是什么作用呢？React为什么要创建它呢？

- 原因是React利用ReactElement对象组成了一个JavaScript的对象树；
- JavaScript的对象树就是大名鼎鼎的虚拟DOM（Virtual DOM）；

如何查看ReactElement的树结构呢？

- 我们可以将之前的jsx返回结果进行打印；
- 注意下面代码中我打jsx的打印；

```jsx
render() {
  const jsx = (
    <div className="app">
      <div className="header">
        <h1 title="标题">我是网站标题</h1>
      </div>
      <div className="content">
        <h2>我是h2元素</h2>
        <button onClick={e => console.log("+1")}>+1</button>
        <button onClick={e => console.log("+1")}>-1</button>
      </div>
      <div className="footer">
        <p>我是网站的尾部</p>
      </div>
    </div>
  )
  console.log(jsx);
  return jsx;
}
```

打印结果，在浏览器中查看：

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)ReactElement对象结构

而ReactElement最终形成的树结构就是Virtual DOM；

整体的转换过程如下：

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)jsx转换流程

#### 6.2.2. 为什么采用虚拟DOM

为什么要采用虚拟DOM，而不是直接修改真实的DOM呢？

- 很难跟踪状态发生的改变：原有的开发模式，我们很难跟踪到状态发生的改变，不方便针对我们应用程序进行调试；
- 操作真实DOM性能较低：传统的开发模式会进行频繁的DOM操作，而这一的做法性能非常的低；

**DOM操作性能非常低：**

首先，document.createElement本身创建出来的就是一个非常复杂的对象；

- https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createElement

其次，DOM操作会引起浏览器的回流和重绘，所以在开发中应该避免频繁的DOM操作；

**这里我们举一个例子：**

比如我们有一组数组需要渲染：[0, 1, 2, 3, 4]，我们会怎么做呢？

```jsx
<ul>
  <li>0</li>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
</ul>
```

后来，我们又增加了5条数据：[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

```jsx
for (var i=5; i<10; i++) {
  var li = document.createElement("li");
  li.innerHTML = arr[i];
  ul.appendChild(li);
}
```

上面这段代码的性能怎么样呢？非常低效

- 因为我们通过 `document.createElement` 创建元素，再通过 `ul.appendChild(li)` 渲染到DOM上，进行了多次DOM操作；
- 对于批量操作的，最好的办法不是一次次修改DOM，而是对批量的操作进行合并；（比如可以通过DocumentFragment进行合并）；

**虚拟DOM帮助我们从命令式编程转到了声明式编程的模式**

React官方的说法：Virtual DOM 是一种编程理念。

在这个理念中，UI以一种理想化或者说虚拟化的方式保存在内存中，并且它是一个相对简单的JavaScript对象，我们可以通过ReactDOM.render让 `虚拟DOM` 和 `真实DOM`同步起来，这个过程中叫做协调（Reconciliation）；

这种编程的方式赋予了React声明式的API：你只需要告诉React希望让UI是什么状态，React来确保DOM和这些状态是匹配的。

你不需要直接进行DOM操作，只可以从手动更改DOM、属性操作、事件处理中解放出来；