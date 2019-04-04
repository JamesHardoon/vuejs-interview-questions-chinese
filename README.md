# VueJS 面试题

英文版：[vuejs-interview-questions](https://github.com/sudheerj/vuejs-interview-questions)

列出了 300 道 VueJS 面试题

> 如果你喜欢这个项目点击 :star:，Pull Requests 是非常赞赏的。

## 内容列表
-------------------------------------------------------------------
| 序号 | 问题                                                                                                             |
|------|------------------------------------------------------------------------------------------------------------------|
| 1    | [VueJS 是什么？](#1-vuejs-是什么)                                                                                |
| 2    | [VueJS 的主要功能是什么？](#2-vuejs-的主要功能是什么)                                                            |
| 3    | [VueJS 的生命周期方法是什么？](#3-vuejs-的生命周期方法是什么)                                                    |
| 4    | [条件指令是什么？](#4-条件指令是什么)                                                                            |
| 5    | [v-show 和 v-if 指令有什么不同？](#5-v-show-和-v-if-指令有什么不同)                                              |
| 6    | [v-for 指令的目的是什么？](#6-v-for-指令的目的是什么)                                                            |
| 7    | [vue 实例是什么？](#7-vue-实例是什么)                                                                            |
| 8    | [如何实现条件组元素？](#8-如何实现条件组元素)                                                                    |
| 9    | [如何复用有 key 属性的元素？](#9-如何复用有-key-属性的元素)                                                      |
| 10   | [为什么不能在同一个元素上同时使用 v-if 和 v-for 指令？](#10-为什么不能在同一个元素上同时使用-v-if-和-v-for-指令) |
| 11   | [为什么使用 for 指令时需要 key 属性？](#11-为什么使用-for-指令时需要-key-属性)                                   |
| 12   | [什么是数组检测突变的方法？](#12-什么是数组检测突变的方法)                                                       |
| 13   | [什么是数组检测非突变方法？](#13-什么是数组检测非突变方法)                                                       |
| 14   | [检测数组变化有什么注意事项？](#14-检测数组变化有什么注意事项)                                                   |
| 15   | [检测对象变化有什么注意事项？](#15-检测对象变化有什么注意事项)                                                   |
| 16   | [如何在一个范围内使用 v-for 指令？](#16-如何在一个范围内使用-v-for-指令)                                         |
| 17   | [如何在模板上使用 v-for 指令？](#17-如何在模板上使用-v-for-指令)                                                 |
| 18   | [如何使用事件处理程序？](#18-如何使用事件处理程序)                                                               |
| 19   | [Vue 提供的事件修饰符是什么？](#19-Vue-提供的事件修饰符是什么)                                                   |
| 20   | [什么是 key 修饰符？](#20-什么是-key-修饰符)                                                                     |

## 1. VueJS 是什么？

**Vue.js** 是一个开源，用于构建用户界面的渐进式 JavaScript 框架。VueJS 的核心库只关注于`视图层`，并且易于装载和集成其他的库或现有的项目。

## 2. VueJS 的主要功能是什么？

以下是一些 VueJS 可用的主要功能
1. **虚拟 DOM：** 它使用的虚拟 DOM 类似于其他现有的框架，例如 ReactJS，Ember etc。虚拟内存是一个轻量级的在内存中原生 HTML DOM 的表示形式并且不影响原生 DOM 的更新。
2. **组件：** 在 VueJS 应用中用于创建可复用的自定义元素。
3. **模板：** VueJS 提供基于 HTML 的模板并将 DOM 和 Vue 实例的 data 绑定。
4. **路由：** 通过 vue-router 实现页面之间的导航。
5. **轻量：** VueJS 相较于其他框架是一个轻量级的库。

## 3. VueJS 的生命周期方法是什么？

生命周期钩子是一个让你看到你正在使用的库是如何在后台工作的窗口。通过这些钩子，你可以知道你的组件何时被创建、添加进 DOM、更新、及销毁。在详细介绍每一个生命周期钩子之前，让我们一起先看一下生命周期的图表。

<img src="https://github.com/sudheerj/vuejs-interview-questions-chinese/blob/master/images/vuelifecycle.png" width="400" height="800">

1. **Creation(初始化):** Creation 钩子允许你在你的组件被添加进 DOM 之前执行行为。如果你需要在客户端和服务端渲染期间设置一些操作则需要使用这些钩子。不同于其他钩子，creation 在服务端渲染期间也会运行。

    1. beforeCreate: 这个钩子会在你的组件初始化时执行。组件中的钩子监听数据 data 并初始化事件。这时 data 还不是响应式的，并且发生在组件生命周期中的事件还未被设置。
        
    ```javascript
    new Vue({
        data: {
            count: 10
        },
        beforeCreate: function () {
            console.log('Nothing gets called at this moment')
            // `this` 指向视图模型的实例
            console.log('count is ' + this.count);
        }
    })
        // count is undefined
    ```
         
    2. created: 这个钩子会在 Vue 设置了事件并监听 data 之后被调用。这时事件是活跃状态并且能够使用响应式的 data 即使模板还未挂载或渲染。
        
    ```javascript
    new Vue({
        data: {
            count: 10
        },
        created: function () {
            console.log('count is: ' + this.count)
        }
    })
    // count is: 10
    ```
    
    **Note:** 记住这点, 你不能使用 DOM 或 挂载元素目标 (this.$el) 在 creation 钩子中。
        
2. **Mounting(DOM 插入):** Mounting 钩子是最常被用到的，它允许你在第一次渲染之后立即使用你的组件。
    
    1. beforeMount: beforeMount 允许你在组件第一次渲染后立即使用组件。
    
    ```javascript
    new Vue({
        beforeMount: function () {
            // `this` points to the view model instance
            console.log(`this.$el is yet to be created`);
        }
    })
    ```
        
    2. mounted:这个是一个最常被使用的钩子，你可以完全使用响应式的组件、模板、和渲染好的 DOM (via. this.$el)。最常用的模式就是获取组件的数据。
        
    ```javascript
    <div id="app">
        <p>I’m text inside the component.</p>
    </div>
    
    new Vue({
        el: ‘#app’,
        mounted: function() {
            console.log(this.$el.textContent); // I'm text inside the component.
        }
    })
    ```
        
3. **Updating (Diff 并 重新渲染):** Updating 钩子会在你的组件中使用的响应式属性改变或其他原因导致重新渲染时被调用
    
    1. beforeUpdate: beforeUpdate 钩子在你的组件 data 改变并且 update 周期开始后，DOM 的修改并重新渲染前运行。
    
    ```javascript
    <div id="app">
        <p>{{counter}}</p>
    </div>
    ...// rest of the code
    new Vue({
        el: '#app',
        data() {
            return {
            counter: 0
            }
        },
        created: function() {
            setInterval(() => {
                this.counter++
            }, 1000)
        },
        beforeUpdate: function() {
            console.log(this.counter) // Logs the counter value every second, before the DOM updates.
        }
    })
    ```
    
    2. updated: 这个钩子在组件 data 改变且 DOM 重新渲染后运行。
    
    ```javascript
    <div id="app">
        <p ref="dom">{{counter}}</p>
    </div>
    ...//
    new Vue({
        el: '#app',
        data() {
            return {
            counter: 0
            }
        },
        created: function() {
            setInterval(() => {
                this.counter++
            }, 1000)
        },
        updated: function() {
            console.log(+this.$refs['dom'].textContent === this.counter) // Logs true every second
        }
    })
    ```
    
4. **Destruction (拆卸):** Destruction 钩子允许你在你的组件被销毁后执行行为

    1. beforeDestroy: `beforeDestroy` 会在拆卸前被调用。如果你需要清理事件或响应订阅，就应使用 beforeDestroy 去做。
    
    ```javascript
    new Vue ({
        data() {
        return {
            message: 'Welcome VueJS developers'
        }
        },
        beforeDestroy: function() {
            this.message = null
            delete this.message
        }
    })
    ```
    
    2. destroyed: 这个钩子会在组件被销毁，指令解绑且事件监听器被移除后调用。
    
    ```javascript
    new Vue ({
        destroyed: function() {
            console.log(this) // Nothing to show here
        }
    })
    ```

## 4. 条件指令是什么？

VueJS 提供了通过指令基于条件来显示或隐藏元素。可用的指令有：**v-if, v-else, v-else-if and v-show**
    
**1. v-if:**  v-if 指令基于给定的表达式添加或移除 DOM 元素，下面的 button 在 isLoggedIn 被设置为 false 时不会显示。

```html
<button v-if="isLoggedIn">Logout</button>
```

将全部元素都包在一个 `<template>` 元素里这样也可以使用一个 v-if 指令基于条件控制多个元素。例如，你可以将条件同事应用于 label 和 button。

```html
<template v-if="isLoggedIn">
    <label> Logout </button>
    <button> Logout </button>
</template>
```

**2. v-else:**  这个指令只会在相邻的 v-if 条件为 false 时用来显示内容。这类似于任何编程语言中的 else 块用来显示可选的内容，并且在它前面是 v-if 或 v-else-if 块。你不需要传递任何值给它。
例如，v-else 在 isLoggedIn 被设置为 false （未登录）时显示 LogIn 按钮。

```html
<button v-if="isLoggedIn"> Logout </button>
<button v-else> Log In </button>
```

**3. v-else-if:** 当我们需要两个以上选项检查时，就会用到这个指令。
例如，当 ifLoginDisabled 属性被设置为 true 时我们想要显示一些文案替代 LogIn 按钮。这就可以通过 v-else 指令实现。

```html
<button v-if="isLoggedIn"> Logout </button>
<label v-else-if="isLoginDisabled"> User login disabled </label>
<button v-else> Log In </button>
```

**4. v-show:** 这个指令类似于 v-if，但是它会将所有元素渲染到 DOM 中并通过 CSS 的 display 属性来 显示 /隐藏 元素。这个指令被推荐用于需要频繁切换开关的元素。

```html
<span v-show="user.name">Welcome user,{{user.name}}</span>
```
## 5. v-show 和 v-if 指令有什么不同？

以下是一些关于 **v-show** 和 **v-if** 指令的不同点：

1. v-if 只在表达式通过的情况下将元素渲染到 DOM 中，而 v-show 渲染全部元素到 DOM 中并基于表达式使用 CSS display 属性来 显示/隐藏 元素。
2. v-if 支持 v-else 和 v-else-if 指令，而 v-show 不支持 else 指令。
3. v-if 有更高的切换开销，而 v-show 有更高的初始化渲染开销。换言之，如果元素会被频繁切换开关则 v-show 有优势，在初始渲染时间方面 v-if 有优势。
4. v-if 支持 `<template>` 选项卡，但 v-show 不支持。
        
## 6. v-for 指令的目的是什么？

内置的 v-for 指令允许我们循环遍历数组或对象中的每一项。你可以迭代数组或对象中的每一个元素。

1. 数组用法：

```javascript
<ul id="list">
    <li v-for="(item, index) in items">
        {{ index }} - {{ item.message }}
    </li>
</ul>

var vm = new Vue({
    el: '#list',
    data: {
        items: [
            { message: 'John' },
            { message: 'Locke' }
        ]
    }
})
```

你也可以使用 `of` 作为分隔符替代 `in`，类似于 javascript iterators。

2. 对象用法：

```javascript
<div id="object">
    <div v-for="(value, key, index) in user">
        {{ index }}. {{ key }}: {{ value }}
    </div>
</div>

var vm = new Vue({
    el: '#object',
    data: {
        user: {
            firstName: 'John',
            lastName: 'Locke',
            age: 30
        }
    }
})
```

## 7. vue 实例是什么？

每个 Vue 应用工作是通过 Vue function 创建一个新的 Vue 实例。一般只用变量 vm（ViewModel 简写）作为 Vue 实例的引用。你可以像下面这样创建一个 Vue 实例，

```javascript
var vm = new Vue({
    // options
})
```

如上面的代码片段所述，你需要传递选项对象。你可以在 API 参考里找到完整的选项列表。
    
## 8. 如何实现条件组元素？

你可以通过对元素组的不可见（不渲染）包装元素 `<template>` 应用 **v-if** 指令实现条件元素组（一次切换多个元素）。例如，你可以根据有效的用户条件对用户详情分组。

```html
<template v-if="condition">
    <h1>Name</h1>
    <p>Address</p>
    <p>Contact Details</p>
</template>
```
    
## 9. 如何复用有 key 属性的元素？
    
Vue 总是尝试尽可能高效地渲染元素。因此它会试图用重用元素替代从零开始构建。但这种行为会在有些情况下导致一些问题。例如，如果你尝试在 `v-if` 和 `v-else` 块中渲染同样的 input 元素，它将会像下面这样在切换后保留先前的值，

```html
<template v-if="loginType === 'Admin'">
    <label>Admin</label>
    <input placeholder="Enter your ID">
</template>
<template v-else>
    <label>Guest</label>
    <input placeholder="Enter your name">
</template>
```

这种情况下，它不应该重用。我们可以像下面这样在 input 元素上使用 **key** 属性分离，

```html
<template v-if="loginType === 'Admin'">
    <label>Admin</label>
    <input placeholder="Enter your ID" key="admin-id">
</template>
<template v-else>
    <label>Guest</label>
    <input placeholder="Enter your name" key="user-name">
</template>
```

上面的代码确保了两个输入框失独立的，且不会影响彼此。
    
## 10. 为什么不能在同一个元素上同时使用 v-if 和 v-for 指令？

建议不要使用 v-if 和 v-for 在同一个元素上。因为 v-for 指令比 v-if 优先级高。有两种情况下开发者会尝试这种组合，

1. 过滤列表的项。例如，如果你尝试使用 v-if 标记过滤列表，
    
```html
<ul>
    <li
        v-for="user in users"
        v-if="user.isActive"
        :key="user.id"
    >
        {{ user.name }}
    <li>
</ul>
```

这可以使用在初始列表上使用计算属性预过滤来避免。

```javascript
computed: {
    activeUsers: function () {
        return this.users.filter(function (user) {
            return user.isActive
        })
    }
}
...... //
...... //
<ul>
    <li
        v-for="user in activeUsers"
        :key="user.id"
    >
        {{ user.name }}
    <li>
</ul>

```
    
2. 避免渲染应该被隐藏的列表。例如，你想根据条件检查用户是否显示还是隐藏

```html
<ul>
    <li
        v-for="user in users"
        v-if="shouldShowUsers"
        :key="user.id"
    >
        {{ user.name }}
    <li>
</ul>
```

可以移动条件到父级避免对每一个用户检查

```html
<ul v-if="shouldShowUsers">
    <li
        v-for="user in users"
        :key="user.id"
    >
        {{ user.name }}
    <li>
</ul>
```

## 11. 为什么使用 for 指令时需要 key 属性？

为了跟踪每个节点的特征，从而重用和重排存在的元素，你需要为每一个 `v-for` 迭代的项提供一个 `key` 属性。一个理想的 key 值是条目的唯一 id，让我们举个例子，

```html
<div v-for="item in items" :key="item.id">
    {{item.name}}
</div>
```

因此，只要有可能，总是建议给 v-for 提供一个 key 值，除非迭代的 DOM 内容很简单。
**Note:** 不应该使用非基本类型的值，如对象和数组作为 v-for 的 key。使用 String 或 Number 类型替代。

## 12. 什么是数组检测突变的方法？

顾名思义，突变方法修改原生数组。以下列出了能触发视图更新的数组突变方法。

1. push()
2. pop()
3. shift()
4. unshift()
5. splice()
6. sort()
7. reverse()

如果执行以上任何一个突变方法都回触发试图更新。

```javascript
vm.todos.push({ message: 'Baz' })
```

## 13. 什么是数组检测非突变方法？

不改变原始数组但总是返回一个新的数组就叫非突变方法。以下列出了非突变方法，

1. filter()
2. concat()
3. slice()

以一个 todo list 为例，在列表中根据 status 过滤的新数组替换旧数组，

```javascript
vm.todos = vm.todos.filter(function (todo) {
    return todo.status.match(/Completed/)
})
```

由于 VueJS 的实现，这种方法不会重新渲染整个列表。

## 14. 检测数组变化有什么注意事项？

以下两种清空 Vue 不能检测数组的变化，

1. 直接根据索引设置项，例如

```javascript
vm.todos[indexOfTodo] = newTodo
```

2. 修改数组的长度，例如

```javascript
vm.todos.length = todosLength
```

可以通过使用 `set` 和 `splice` 方法克服这两种警告，让我们 看一下解决实例，

**第一个解决方案**

```javascript
// Vue.set
Vue.set(vm.todos, indexOfTodo, newTodoValue)
// (or)
// Array.prototype.splice
vm.todos.splice(indexOfTodo, 1, newTodoValue)
```

**第二个解决方案**

```javascript
vm.todos.splice(todosLength)
```

## 15. 检测对象变化有什么注意事项？

Vue 在对象属性增删时无法检测到更改。以 user 数据改变为例，

```javascript
var vm = new Vue({
    data: {
        user: {
            name: 'John'
        }
    }
})

// `vm.name` is now reactive

vm.email = 'john@email.com' // `vm.email` is NOT reactive
```

可以通过使用 Vue.set(object, key, value) 方法或 Object.assign() 克服这个情况。

```javascript
Vue.set(vm.user, 'email', john@email.com);
(or)
vm.user = Object.assign({}, vm.user, {
    email: john@email.com
})
```

## 16. 如何在一个范围内使用 v-for 指令？

可以使用一个整数作为 v-for 指令重复元素的次数。

```javascript
<div>
    <span v-for="n in 20">{{ n }} </span>
</div>
```

它会显示数字 1-20

## 17. 如何在模板上使用 v-for 指令？

就类似于 v-if 指令在木板上一样，也可以使用带有 v-for 指令的 `<template>` 标签来渲染多个元素块。以 todo 为例，

```javascript
<ul>
    <template v-for="todo in todos">
        <li>{{ todo.title }}</li>
        <li class="divider"></li>
    </template>
</ul>
```

## 18. 如何使用事件处理程序？

你可以在 Vue 中使用类似于纯 JavaScript 的事件处理程序。方法调用也支持特殊的 $event 变量。

```javascript
<button v-on:click="show('Welcome to VueJS world', $event)">
    Submit
</button>

methods: {
    show: function (message, event) {
        // now we have access to the native event
        if (event) event.preventDefault()
        console.log(message);
    }
}
```

## 19. Vue 提供的事件修饰符是什么？

通常，JavaScript 提供了 event.preventDefault() 或 event.stopPropagation() 在事件处理程序中。你可以使用 Vue 提供的方法，但这些方法用于数据逻辑而不是处理 DOM 事件。Vue 为 v-on 提供了以下事件修饰符，`.` 表示指令后缀。

1. .stop
2. .prevent
3. .capture
4. .self
5. .once
6. .passive

以 stop 修饰符为例，

```html
<!-- the click event's propagation will be stopped -->
<a v-on:click.stop="methodCall"></a>
```

也可以像下面这样链接修饰符，

```html
<!-- modifiers can be chained -->
<a v-on:click.stop.prevent="doThat"></a>
```

## 20. 什么是 key 修饰符？

Vue 支持 v-on 的 key 修饰符处理键盘事件。以输入 keycode 的 keyup 事件为例。

```html
<!-- only call `vm.show()` when the `keyCode` is 13 -->
<input v-on:keyup.13="show">
```

记住全部 keycode 真的很难。它支持完整 keycode 列表别名

1. .enter
2. .tab
3. .delete (捕获 “Delete” 和 “Backspace” 键)
4. .esc
5. .space
6. .up
7. .down
8. .left
9. .right

现在上面的代码使用别名重写如下，

```html
<input v-on:keyup.enter="submit">
<!-- (OR) -->
<!-- with shorthand notation -->
<input @keyup.enter="submit">
```

**不赞成使用 keycode 事件，新的浏览器可能会不支持。**