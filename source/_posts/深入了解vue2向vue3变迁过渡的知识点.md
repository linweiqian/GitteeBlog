---
title: 深入了解vue2向vue3变迁过渡的知识点
tags: 
- vue3
categories:
- vue3
---

## TypeScript 类型支持
vue2.x使用的是Flow来进行开发,但是flow对于一些复杂的场景flow支持的不是很好。

vue3.x中vue全面转向typescript，typescript提供了更好的类型检查，也支持复杂的类型推导。
<!--more-->
## vue3移除vue2的实例方法或修饰符

```
- $children已经被移除。如果要访问子组件，可以使用 $refs
- $on、 $off、 $once 实例方法被移除
- vue3对`filter`过滤器过滤器移除,建议议用方法调用或计算属性来替换它们
- vue3 移除了 $listeners，封装进了 $attrs中
- 移除了v-on.native 修饰符，触发可用emits对象暴露
```
## watch监听数组
vue3当中，如果想要监听数组内容的变化那么必须要写deep。

## v-if和v-for优先级已更改
vue2在同一元素`v-for`优先级高于`v-if`,vue3则相反，仍不建议在同一标签同时使用

## 性能优化

- 源码体积优化：移除冷门api、引入tree-shaking实行按需编译
- 数据劫持优化 proxy
- 编译优化：diff 算法优化
- 编译优化：PatchFlag(静态标记)、hoistStatic(静态提升)与渲染复用
- cacheHandler 事件监听缓存
- 编译优化：Fragment
- SSR 服务端渲染
- StaticNode(静态节点)
- slot 编译优化

## 生命周期的对比

`beforeCreate` -> setup()

`created` -> setup()

`beforeDestroy` -> `beforeUnmount`

`destroyed` -> `unmounted`

## 创建VUE实例的对比

###  vue2创建


```
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')
```

### vue3创建

```
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
createApp(App,{ userName: "sara" })
.use(store)
.use(router)
.mount('#app')  
// createApp 方法返回应用实例本身，因此可以在其后链式调用其它方法
```
## 指令的变化

### vue2.x


```
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
```
### vue3.x

```
const { createApp } from "vue"
const app = createApp({})
app.directive('focus', {
    mounted(el) {
        el.focus()
    }
})
```

## Hooks

vue2使用的`mixin`,
vue3提供了一种新的东西 ，叫做`vue-hooks`

## 响应式数据

在vue2中，实现数据监听使用的是`Object.defineProperty`。我们使用$set。
vue3使用的是`Proxy`

## v-model 升级


> -   变更：在自定义组件上使用`v-model`时， 属性以及事件的默认名称变了
> -   变更：`v-bind`的`.sync`修饰符在 Vue 3 中又被去掉了, 合并到了`v-model`里
> -   新增：同一组件可以同时设置多个 `v-model`
> -   新增：开发者可以自定义 `v-model`修饰符

## 在 prop 的默认函数中访问this

> 生成 prop 默认值的工厂函数不再能访问 this。  
>取而代之的是：
>-   组件接收到的原始 prop 将作为参数传递给默认函数；
>-   inject API 可以在默认函数中使用。

```
import { inject } from 'vue'
export default {
  props: {
    theme: {
      default (props) {
        // `props` 是传递给组件的、
        // 在任何类型/默认强制转换之前的原始值，
        // 也可以使用 `inject` 来访问注入的 property
        return inject('theme', 'default-theme')
      }
    }
  }
}
```
## 插槽统一

> 此更改统一了 3.x 中的普通插槽和作用域插槽。  
> 以下是变化的变更总结：
> -   this.$slots 现在将插槽作为函数公开
> -   非兼容：移除 this.$scopedSlots

### vue2.x


```
<!-- 当使用渲染函数，即 h 时，2.x 曾经在内容节点上定义 slot 数据 property。 -->
// 2.x 语法

h(LayoutComponent, [
  h('div', { slot: 'header' }, this.header),
  h('div', { slot: 'content' }, this.content)
])

<!-- 此外，可以使用以下语法引用作用域插槽： -->
// 2.x 语法

this.$scopedSlots.header
```
### vue3.x

```
<!-- 在 3.x 中，插槽以对象的形式定义为当前节点的子节点： -->
// 3.x Syntax

h(LayoutComponent, {}, {
  header: () => h('div', this.header),
  content: () => h('div', this.content)
})

<!-- 当你需要以编程方式引用作用域插槽时，它们现在被统一到 $slots 选项中了。 -->
// 2.x 语法

this.$scopedSlots.header

// 3.x 语法

this.$slots.header()
```


## 过渡的class名更改

>过渡类名 v-enter 修改为 v-enter-from、过渡类名 v-leave 修改为 v-leave-from。

### vue2.x

```
<!-- 在 v2.1.8 版本之前，每个过渡方向都有两个过渡类：初始状态与激活状态。 -->
<!-- 在 v2.1.8 版本中，引入了 v-enter-to 来定义 enter 或 leave 变换之间的过渡动画插帧。然而，为了向下兼容，并没有变动 v-enter 类名： -->

.v-enter,
.v-leave-to {
  opacity: 0;
}

.v-leave,
.v-enter-to {
  opacity: 1;
}

<!-- 这样做会带来很多困惑，类似 enter 和 leave 含义过于宽泛，并且没有遵循类名钩子的命名约定。 -->
```
### vue3.x

```
<!-- 为了更加明确易读，我们现在将这些初始状态重命名为： -->

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.v-leave-from,
.v-enter-to {
  opacity: 1;
}

<!-- 现在，这些状态之间的区别就清晰多了。 -->
```

## Transition 作为根节点



```
    当使用 <transition> 作为根结点的组件从外部被切换时将不再触发过渡效果
```
### vue2.x
```
<!-- 在 Vue 2 中，通过使用 <transition> 作为一个组件的根节点，过渡效果存在从组件外部触发的可能性： -->
<!-- 模态组件 -->
<template>
  <transition>
    <div class="modal"><slot/></div>
  </transition>
</template>
<!-- 用法 -->
<modal v-if="showModal">hello</modal>
<!-- 切换 showModal 的值将会在模态组件内部触发一个过渡效果。
这是无意为之的，并不是设计效果。一个 <transition> 原本是希望被其子元素触发的，而不是 <transition> 自身。
这个怪异的现象现在被移除了。 -->
```
### vue3.x
    
```
<!-- 换做向组件传递一个 prop 就可以达到类似的效果： -->

<template>
  <transition>
    <div v-if="show" class="modal"><slot/></div>
  </transition>
</template>
<script>
export default {
  props: ['show']
}
</script>
<!-- 用法 -->
<modal :show="showModal">hello</modal>
```
    
## Transition Group 根元素
    

```
<transition-group> 不再默认渲染根元素，但仍然可以用 tag attribute 创建根元素
```
### vue2.x
```
<!-- 默认情况下，传递给带有 v-on 的组件的事件监听器只能通过 this.$emit 触发。要将原生 DOM 监听器添加到子组件的根元素中，可以使用 .native 修饰符： -->

<my-component
  v-on:close="handleComponentEvent"
  v-on:click.native="handleNativeClickEvent"
/>
```
### vue3.x

```
<!-- v-on 的 .native 修饰符已被移除。同时，新增的 emits 选项允许子组件定义真正会被触发的事件。 -->

<!-- 因此，对于子组件中未被定义为组件触发的所有事件监听器，Vue 现在将把它们作为原生事件监听器添加到子组件的根元素中 (除非在子组件的选项中设置了 inheritAttrs: false)。 -->

<my-component
  v-on:close="handleComponentEvent"
  v-on:click="handleNativeClickEvent"
/>

// MyComponent.vue

<script>
  export default {
    emits: ['close']
  }
</script>
```
    
