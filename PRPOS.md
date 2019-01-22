# props进行的组件之间的双向数据绑定

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.js"></script>
</head>

<body>
    <div id='app'>
        <Coa :title="title" @on-change-value="getNewValue"></Coa>
        <p>{{title}}</p>
    </div>
</body>
<script>
    var Coa = {
        props: ['title'],
        // 父组件传过来的 title 属性
        data() {
            return {
                // 在组件内的 data 对象中创建一个 props 属性的副本
                // 因为title 是不可写的,需要在data 中创建一个副本 newTitle,初始值时 title,同时在组件中调用的props 的地方直接使用newTitle
                newTitle: this.title  // 新增字段
            }
        },
        // 2.创建正对props 属性的watch 来同步组件外对 props的修改
        // 此时在组件外（父组件）修改了组件props ,会同步到组件内对应的props 上，但是不会同步到你刚刚在 data 对象中创建的副本上，所以需要在创建一个针对props 属性 title 的watch, 当 props修改后对应的 副本 也要同步数据。
        watch: {
            title(value) {
                this.newTitle = value  // 新增title 的watch, 监听变更并同步到newTitle上
            },
            // 3.创建正对props 副本的watch, 通知到组件外
            // 此时组建内修改了 props 的副本newTitle, 组件外不知道组件内的props 状态，所以需要在创建一个针对 props 副本newTitle，据对应 data 属性的watch
            // 在徐建内向外层发送通知，通知组件内属性变更，然后又外层自己来更改它的数据
            newTitle(value) {
                this.$emit('on-change-value', value)
            }
        },
        template: `<input v-model='newTitle'/>`
    }

    var vm = new Vue({
        el: '#app',
        data: {
            title: '我现在是谁'
        },
        components: {
            Coa
        },
        methods: {
            getNewValue(value) {
                this.title = value
            }
        }
    })
</script>
</html>
```

# 改造v-model来实现双向绑定
__注意__ 实现v-model的几个要素：

* `子组件`通过 __`value`__ 属性(`prop`)接受输入
* `子组件`通过触发 __`input`__ 事件输出, 带数组参数
* `父组件`中用 `v-model` 绑定

```html
<html>

<body>

    <!-- 模板中 -->
    <li v-for="todo in todos">
        <!--  父组件中使用 v-model 来绑定 -->
        <todo :text="todo.text" v-model="todo.done"></todo>
        -- {{todo.done}}
    </li>
</body>
<script>
    Vue.component('todo',{
        props:{
            value: '',  //<---- 注意 这里使用value接收
            text: ''
        },
        data () {
            return {
                isDone: this.value
            }
        },
        methods: {
            toggle(){
                this.isDone = !this.isDone
                this.$emit('input', this.isDone) // <-- 事件名称改变使用input
            }
        },
        template:`<label>
                <input type="checkbox"
                v-on:change="toggle"
                v-bind:checked="isDone">
        
                <del v-if="isDone">
                {{ text }}
                </del>
                <span v-else>
                {{ text }}
                </span>
            </label>`
    })
</script>
</html>
```

# .sync 实现其他数据的绑定
`.sync` 修饰语用于修饰 `v-bind`(即`:` ),使之成为双向绑定.
这同样是语法糖，添加`.sync` 修饰的数据绑定会像v-model 一样自动注册事件处理函数来对绑定的数据进行赋值。
这样的方式同样要求子组件触发特定的事件。不过这个事件的名称好歹和绑定属性名有点关系模式下绑定属性名前添加`update: `前缀。

比如`<sub :some.sync="any" />`将子组件的some 属性和父组件的any 属性绑定起来，子组件中需要通过`$emit('update:some', value)`来出触发变更。

```html
<html>
    <body>
        <!-- 模板中 -->
    <li v-for="todo in todos">
        <!--  父组件中使用 v-model 来绑定 -->
        <todo :text="todo.text" :done.sync="todo.done"></todo>
        -- {{todo.done}}
    </li>
    </body>
    <script>
         Vue.component('todo',{
        props:{
            done: '', //注意这个值
            text: ''
        },
        data () {
            return {
                isDone: this.done
            }
        },
        methods: {
            toggle(){
                this.isDone = !this.isDone
                this.$emit('update:done', this.isDone) // <-- 事件名称改变使用input
            }
        },
        template:`<label>
                <input type="checkbox"
                v-on:change="toggle"
                v-bind:checked="isDone">
        
                <del v-if="isDone">
                {{ text }}
                </del>
                <span v-else>
                {{ text }}
                </span>
            </label>`
    })
    </script>
</html>
```