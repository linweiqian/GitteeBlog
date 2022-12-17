---
title: vue3的7种路由守卫使用大全
tags: 
- vue
categories:
- vue
---
## 路由守卫有哪几种？
路由守卫(导航守卫)分为三种：全局守卫（3个）、路由独享守卫（1个）、组件的守卫（3个）


## 路由守卫的三个参数
<!--more-->
to：要跳转到的目标路由

from：从当前哪个路由进行跳转

next：不做任何阻拦，直接通行

注意： 必须要确保 next函数 在任何给定的导航守卫中都被调用过一次。它可以出现多次，但是只能在所有的逻辑路径都不重叠的情况下，否则会报错。
案例：

```bash
router.beforeEach((to, from, next) => {
  if (to.name !== 'Login' && !isAuthenticated) next({ name: 'Login' })
  else next()
})
```

## 一、全局路由守卫

> 全局路由守卫有三个：全局前置守卫，全局后置守卫,全局解析守卫

- 全局前置守卫

1.使用方式：main.js中配置,在路由跳转前触发，这个钩子作用主要是用于登录验证，也就是路由还没跳转提前告知，以免跳转了再通知就为时已晚
2.代码:

```bash
router.beforeEach((to,from,next)=>{})
```
3.例子:做登录判断

```bash
router.beforeEach((to,from,next)=>{

  if(to.path == '/login' || to.path == '/register'){

    next();

  }else{

    alert('您还没有登录，请先登录');

    next('/login');

  }

})
```
- 全局后置守卫

1.使用方式：main.js中配置,和beforeEach相反，它是在路由跳转完成后触发，它发生在beforeEach和beforeResolve之后，beforeRouteEnter（组件内守卫）之前。钩子不会接受next函数也不会改变导航本身
2.代码:

```bash
router.afterEach((to,from)=>{})
```
- 全局解析守卫
1.使用方式：main.js中配置,这个钩子和beforeEach类似，也是路由跳转前触发，区别是在导航被确认之前，同时在所有组件内守卫和异步路由组件被解析之后，即在 beforeEach 和 组件内beforeRouteEnter 之后，afterEach之前调用。
2.代码:

```bash
router.beforeResolve((to,from,next)=>{})
```

## 一、组件内守卫

> 组件内守卫有个三个：路由进入之前beforeRouteEnter，路由离开时beforeRouteLeave,页面更新时beforeRouteUpdate 

-  beforeRouteEnter(to, from, next)
1.使用方式：在组件模板中使用,跟methods: {}等同级别书写，组件路由守卫是写在每个单独的vue文件里面的路由守卫
2.代码:
```bash
beforeRouteEnter(to, from, next) {
    // 在组件生命周期beforeCreate阶段触发
    console.log('组件内路由前置守卫 beforeRouteEnter', this) // 访问不到this
    next((vm) => {
      console.log('组件内路由前置守卫 vm', vm) // vm 就是this
    })
  },
```
- beforeRouteUpdate(to, from, next)
1.使用方式：在组件模板中使用,跟methods: {}等同级别书写，组件路由守卫是写在每个单独的vue文件里面的路由守卫
2.代码:

```bash
beforeRouteUpdate (to, from, next) {
    // 同一页面，刷新不同数据时调用，
    // 可以访问组件实例 
}
```
- beforeRouteLeave(to, from, next)
1.使用方式：在组件模板中使用,跟methods: {}等同级别书写，组件路由守卫是写在每个单独的vue文件里面的路由守卫
2.代码:

```bash
beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例
}
```


## 路由独享守卫

>  路由独享守卫只有一个:进入路由时触发beforeEnter

- 路由独享守卫 beforeEnter(to, from, next)
1.使用方式：**在router.js中使用**,路由独享守卫是在路由配置页面单独给路由配置的一个守卫
2.代码

```bash

const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})

```

## 导航解析流程

> 
> 1.触发进入其它路由
2.调用要离开路由的组件守卫beforeRouteLeave
3.调用全局的前置守卫beforeEach
4.在重用的组件里调用 beforeRouteUpdate
5.在路由配置里的单条路由调用 beforeEnter
6.解析异步路由组件
7.在将要进入的路由组件中调用beforeRouteEnter
8.调用全局的解析守卫beforeResolve
9.导航被确认
10.调用全局的后置钩子afterEach
11.触发 DOM 更新mounted
12.执行beforeRouteEnter守卫中传给 next的回调函数

## 结尾:

vue2和vue3的写法基本一致没有改变
