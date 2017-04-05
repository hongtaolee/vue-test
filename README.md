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
cnpm install --save element-ui
cnpm run dev  # 类似于rails 里面的 rails s
```
## 修改App.vue
1. <script> 中增加
	
```shell
import Vue from 'vue'
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-default/index.css'
```
2. template 中参考element ui 文档编写代码

3. style 中参考element ui 文档编写代码

## 开发工具

- webstorm 
 
  下载： https://www.jetbrains.com/webstorm/  

	破解： http://www.cnblogs.com/tzdy/p/6472538.html