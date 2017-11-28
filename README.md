# lab

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

## Tips & 坑
### $options
Q：在methods中，一个方法需要调用另一个方法

A:
```javascript
a() {
  console.log("a");
},
b() {
  this.$options.methods.a();
  console.log("b");
}
```
总结：
vm.$options用于当前 Vue 实例的初始化选项。需要在选项中包含自定义属性时会有用处；
[官方文档vm.$options](https://cn.vuejs.org/v2/api/#vm-options)
### git
#### 在本地目录下关联远程repository ：
git remote add origin git@github.com:username/repository-name.git

#### 取消本地目录下关联的远程库：
git remote remove origin
### 防止组件style污染全局
使用`scoped`
```html
<style scoped>

</style>
```
### vue-router
#### 引入
```javascript
import Vue from 'vue';
import VueRouter from 'vue-router';

Vue.use(VueRouter);
```
#### 配置
```javascript
import login from './components/login/login';
import signUp from './components/signup/signup';

let routes = [
  { path: '/', component: login },
  { path: '/signUp', component: signUp }
]

let router = new VueRouter({
  linkActiveClass: 'active',
  routes
});
```
#### 挂载和初始化
```javascript
// 挂载
const vm = new Vue({
  router
}).$mount('#app');

// 初始化(默认显示'/')
router.push('/');
```
#### 使用
##### 路由插座
```html
<router-view></router-view>
```
`router-view`有`name`属性，在注册路由时可根据其`name`指定路由对应的`router-view`;
```
<router-view name="test"></router-view>

{ path: '/signUp', components: { test: signUp } }
```
##### keep-alive
```html
<keep-alive>
  <router-view></router-view>
</keep-alive>
```
使用`keep-alive`之后页面模板第一次初始化解析变成HTML片段后，再次进入就不在重新解析而是读取内存中的数据;
### 使用
##### 路由跳转
```html
<router-link to="/">登录</router-link>
<router-link to="/signUp">注册</router-link>
```
### 路由嵌套
使用`children: []`定义子路由
```
{
  path: '/admin',
  component: admin,
  redirect: '/admin/charts',
  children: [
    { path: 'charts', component: charts },
    { path: 'video', component: labVideo }
  ]
}
```

