# Vue 简单环境搭建

## node

```shell
node -v  # 检查node版本，如果版本过低，可以采用下面命令升级到最新版本
npm install -g n
n stable
```
## npm
```shell
npm -v          # 显示版本，检查npm 是否正确安装。 
npm install -g cnpm --registry=https://registry.npm.taobao.org      # 使用cnpm
cnpm install -g vue-cli   # 全局安装vue-cli
vue init webpack  my-project-name   # 初始化项目名，初始化建议使用ESLint，可以不安装test相关组件

? Project name vue-test
? Project description A Vue.js project
? Author Kevin <lihongtao@tumao.com>
? Vue build standalone
? Install vue-router? Yes
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard
? Setup unit tests with Karma + Mocha? No
? Setup e2e tests with Nightwatch? No

cd my-project-name
cnpm install  # 类似于rails 里面的 bundle install
cnpm run dev  # 类似于rails 里面的 rails s
```
## element-ui
1. 通过cnpm安装element-ui，如果package.json 中已经安装了，则跳过此步骤

```shell
cnpm install --save element-ui
```

2. App.vue 中\<script\>中增加

```shell
import Vue from 'vue'
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-default/index.css'
```

3. template 中参考element ui 文档编写代码

4. style 中参考element ui 文档编写代码

## 开发工具

- webstorm
  - 下载： https://www.jetbrains.com/webstorm/  
  - 破解： http://www.cnblogs.com/tzdy/p/6472538.html

## 组件

<img src = "https://cn.vuejs.org/images/components.png" />

```
	// 定义名为 todo-item 的新组件
	Vue.component("todo-item", {
		props: ['todo'],
		template: '<li>{{ todo.text }}</li>'
	})

	var app7 = new Vue({
		el: '#app-7',
		data: {
			todolist: [
				{ text: '蔬菜' },
				{ text: '奶酪' },
				{ text: '随便什么东西' }
			]
		}
	})
```
```
	<!--  创建一个 todo-item 组件的实例-->
	<ol>
		<todo-item v-for="item in todolist" v-bind:todo="item"></todo-item>
	</ol>
```

### 模板语法

#### 插值
	{{}}
	v-html
#### 指令： 当其表达式的值改变时相应地将某些行为应用到DOM上
#### 过滤器： 常见的文本格式化，只能在 mustache / v-bind 表达式中使用
#### 计算属性： 指令中实现更复杂的数据变化
#### 观察： watcher ，当想要在数据变化响应时，执行异步操作或开销较大的操作

### 指令

#### 列表渲染
名称 |  备注 | 使用方法
-----|--------|------
 v-if |  | ``` ```
 v-show |  | ``` ```
 v-else |  | ``` ```
 v-else-if |  | ``` ```
 v-for |  | ``` ```


#### 事件处理器
名称 |  备注 | 使用方法
-----|--------|------
 v-on | 监听DOM事件触发js代码 | ``` <button v-on:click="counter += 1">增加 1</button>```

#### 修饰符
修饰符 | 备注 | 案例
---|---|----
.stop | 阻止单击事件冒泡| ```<a v-on:click.stop="doThis"></a>```
.prevent | 提交事件不再重载页面 | ```<a v-on:click.stop.prevent="doThat"></a>```
.capture | 添加事件侦听器时使用事件捕获模式|```<div v-on:click.capture="doThis">...</div>```
.self | 只当事件在该元素本身（而不是子元素）触发时触发回调|```<div v-on:click.self="doThat">...</div>```
.once | 事件只会触发一次| ```<a v-on:click.once="doThis"></a>```
.enter/.tab | 按键，可通过 config.keyCodes 自定义别名 | ```<input @keyup.enter="submit">```

#### 表单控件绑定
名称 |  备注 使用方法
-----|--------|------
 v-model | 在表单空间元素上创建双向数据把固定；不关心表单空间初始化值，会根据Vue实例数据作为具体值。如果对于IME构成中更新，使用<mark>input</mark>| ``` <input v-model="message">```
v-bind/@ | 绑定value到Vue实例的一个动态属性上。|``` <input type="radio" v-model="pick" v-bind:value="a">```

#### 修饰符
修饰符 | 备注 | 案例
---|---|----
.lazy |v-model默认在input时间中同步，lazy为在<mark>change</mark>事件中同步| ```<input v-model.lazy="msg">```
.number | 自动将用户输入值转为Number 类型| ```<input v-model.number="age" type="number">```
.trim | 自动过滤用户输入的首尾空格|```<input v-model.trim="msg">```



### 组件间通信

<img src="https://cn.vuejs.org/images/props-events.png" />

- prop
	- prop 单向绑定：父组件属性变化 -> 子组件
	- 通过 计算属性 处理prop值
	- 验证：type / []

- 自定义事件
	- $on(eventName) ： 监听事件
	- $emit(eventName) ： 触发事件

```
<div id="counter-event-example">
  <p>{{ total }}</p>
  <button-counter v-on:incrementEvent="incrementTotal"></button-counter>
  <button-counter v-on:incrementEvent="incrementTotal"></button-counter>
</div>
```
```
Vue.component('button-counter', {
  template: '<button v-on:click="increment">{{ counter }}</button>',
  data: function () {
    return {
      counter: 0
    }
  },
  methods: {
    increment: function () {
      this.counter += 1
      this.$emit('incrementEvent')
    }
  },
})
new Vue({
  el: '#counter-event-example',
  data: {
    total: 0
  },
  methods: {
    incrementTotal: function () {
      this.total += 1
    }
  }
})

```

.native ： 修饰符，给某个组件的根元素上监听一个原生事件

```
<my-component v-on:click.native="doTheThing"></my-component>
```

- 非父子通信

```
var bus = new Vue()

// 触发组件 A 中的事件
bus.$emit('id-selected',1)

// 组件B 创建的钩子中监听事件
bus.$on('id-selected', function(id){
	//....
})
```
- slot: 分发内容，类似于 rails 的yield

```
	<app>
		<app-header></app-header>

		<app-footer></app-footer>
	</app>
```

	- 父组件决定挂载的内容
	- 组件很可能有自己的模板

- is： 动态组件  keep-alive  

- ref ： 子组件索引ID，避免在模板或计算属性中使用 $refs
- inline-template
- X-Templates
- v-once

### 响应式原理

<img src="http://v1-cn.vuejs.org/images/mvvm.png" >

<img src="https://cn.vuejs.org/images/data.png">

状态管理

<img src="https://cn.vuejs.org/images/state.png">

单向数据流

<img src="https://vuex.vuejs.org/zh-cn/images/flow.png">

Vuex

<img src="https://vuex.vuejs.org/zh-cn/images/vuex.png">
