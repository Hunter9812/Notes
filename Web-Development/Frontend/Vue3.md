# 入门

1. 安装 [node.js](https://www.bilibili.com/video/BV1kN41197vw/?p=2&spm_id_from=pageDriver&vd_source=8a5edf01724270cb0d1c66670345dd0e)

   笔记：[Node.js.md](Node.js.md)

2. 安装工具链

   官方推荐使用Vite。
   ~~任意一个，建议先从vuecli开始学，因为教程一般用这个教（但现在属于维护状态）。~~

   - [Vite](https://cn.vitejs.dev/)
   - [Vue CLI](https://cli.vuejs.org/zh/) ：目前处于维护状态

## 基础语法

- `{{}}`

  是 Vue 中的一个特殊的模版语法，它能在模版内打印类中定义的 JavaScript 表达式的结果，包括值和方法。重要的是，`{{}}` 里的内容是作为文本显示，而非 HTML。

- [`props`](https://cn.vuejs.org/guide/components/props.html#props-declaration)

  我们需要的是一些组件状态。这可以通过在组件中添加 props 来实现。您可以认为 props 与函数中的输入类似。prop 的值给予了组件影响其显示的初始状态。

- [`data`](https://cn.vuejs.org/api/options-state.html#data)

  用于声明组件初始响应式状态的函数，你可以用来在组件中管理本地状态。

- [`v-bind`](https://cn.vuejs.org/api/built-in-directives.html#v-bind)`:`

  你可以在要绑定到的任何 attribute/prop 前面加上 `v-bind:`

- [`v-for`](https://cn.vuejs.org/api/built-in-directives.html#v-for)

  类似 JavaScript 中的 [`for...in`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in) 循环——`v-for="item in items"`——`items` 是你要迭代的列表，`item` 是数组中当前元素的引用。

- `v-on` `@`

  用于事件处理的特殊指令，通过 `v-on:event="method"` 语法工作。

  - [`$emit()`](https://cn.vuejs.org/api/component-instance.html#emit) 自定义事件

- [`v-model`](https://cn.vuejs.org/api/built-in-directives.html#v-model)

  在表单输入元素或组件上创建双向绑定。

  **备注：** 你还可以通过事件和 `v-bind` 属性的组合将数据与 `<input>` 值同步。事实上，这就是 `v-model` 在幕后所做的。但是，确切的事件和属性组合因输入类型而异，并且比仅使用 `v-model` 快捷方式需要更多代码。

  - [修饰符](https://cn.vuejs.org/guide/components/v-model.html#handling-v-model-modifiers)

    `.trim`：删除输入之前或之后的空格
    `.number`
    `.lazy`：`v-model` 同步通过使用事件更新变量来工作。对于文本输入，此同步使用 [`input` 事件](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/input_event)进行。通常，这意味着 Vue 在每次击键后都会同步数据。`.lazy` 修饰符导致 `v-model` 使用 [`change` 事件](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/change_event)代替。这意味着 Vue 只会在输入失去焦点或提交表单时同步数据。

- `v-if` 与 `v-else` 与 `v-else-if`

# 选择式

```vue
<script>
export default {
  // data() 返回的属性将会成为响应式的状态
  // 并且暴露在 `this` 上
  data() {
    return {
      count: 0
    }
  },

  // methods 是一些用来更改状态与触发更新的函数
  // 它们可以在模板中作为事件处理器绑定
  methods: {
    increment() {
      this.count++
    }
  },

  // 生命周期钩子会在组件生命周期的各个不同阶段被调用
  // 例如这个函数就会在组件挂载完成后被调用
  mounted() {
    console.log(`The initial count is ${this.count}.`)
  }
}
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>
```

+ Hello World

    ```vue
    <template>
      <h1>Hello World!</h1>
    </template>
    ```

+ 声明式渲染

    ```vue
    <script>
    export default {
    	data() {
    		return {
    			message: 'Make me dynamic!'
    		}
    	}
    }

    </script>

    <template>
      <h1>{{message.split('').reverse().join('')}}</h1>
    </template>
    ```

+ Attribute 绑定

    ```vue
    <script>
    	export default {
            data(){

            }
        }
    </script>
    ```

​

