#### 网页 PPT

- 考察: JQuery （选择器，显示隐藏等常用 API）

- 答案：

```js
// 缓存 $("section") 的 jQuery 选择器，以提高性能
let $sections = $("section");

// 隐藏所有 section 元素，显示 activeIndex 对应的元素
$sections.hide();
$sections.eq(activeIndex).show();

// 记录 section 元素的个数
let len = $sections.length;

// 如果 activeIndex 是 0，给左侧按钮添加 disable 类，否则删除
$(".left").toggleClass("disable", activeIndex === 0);

// 如果 activeIndex 是 len-1，给右侧按钮添加 disable 类，否则删除
$(".right").toggleClass("disable", activeIndex === len - 1);

// 显示当前页数和总页数，使用字符串插值来构造 HTML 内容
$(".page").html(`${activeIndex + 1}/${len}`);
```

- 知识点解析：

.`toggleClass()` 是 jQuery 提供的一个方法，它用于在元素上切换一个或多个类名。这个方法有两个参数：

`className`：表示要切换的类名。可以是一个或多个类名，用空格分隔。当该类名存在时，它将被删除；否则它将被添加。

`state`：表示一个布尔值，用于决定是添加还是删除指定的类名。如果这个值为 true，类名将被添加；如果是 false，类名将被删除。如果这个参数被省略，那么类名将被添加或删除，取决于它是否存在。

在 `$(".left").toggleClass("disable", activeIndex === 0)` 这一行中，第一个参数是 `disable` 类名，它将被添加或删除。第二个参数是一个表达式 `activeIndex === 0`，当它的值为 `true` 时，类名将被添加，否则将被删除。因此，这行代码的作用是：

如果 `activeIndex` 等于 0，给 `.left` 元素添加 `disable` 类。
如果 `activeIndex` 不等于 0，删除 `.left` 元素上的 `disable` 类。
这个方法非常方便，可以用于快速地在元素上添加或删除类名。

```js
// $(".left").toggleClass("disable", activeIndex === 0)`等价于
if (activeIndex == 0) {
  $(".left").addClass("disable");
} else {
  $(".left").removeClass("disable");
}
```

#### 西游记之西天取经 

- 考察点 ：CSS3  常用属性


- 答案： 

```html
<style>
 .actor:nth-child(x) {
    /* ...省略代码  */
    /* TODO 填空 */
    animation: a2 0.8s steps(8) infinite;
}
<style>
```

-  知识点解析       这是一个 CSS3 动画属性 `animation` 的值，它包含以下几个部分：

  -  `a2`：表示要应用的动画名称，这个名称需要通过 @keyframes 规则来定义。

  - `0.8s`：表示动画持续的时间，即 0.8 秒。

  - `steps(8)`：表示动画执行的步数，这里使用 `steps` 函数来指定。`steps(8)` 表示动画会分为 8步进行，每一步持续相同的时间。

  - `infinite`：表示动画将无限循环，直到被停止
  
-  拓展学习：  step()、steps() 

#### 商品销量和销售额实时展示看板

- 考察 echarts （数据修改，正式比赛：常用 API -> 提供）


答案：

```js

let data = result.data;
// 销售额
if (data?.saleObj) {
  let [x, y] = [Object.keys(data.saleObj), Object.values(data.saleObj)];
  charData.xAxis.data = x;
  charData.series[0].data = y;
}
// 销量
if (data?.countObj) {
  let y = Object.values(data.countObj);
  charData.series[1].data = y;
}
```

-  知识点解析

`data?.saleObj` 是 ECMAScript 2020 引入的一种可选链语法。

它允许您访问对象的属性，而不会在对象为 nullish（`null` 或 `undefined`）时引发错误。如果对象为 `nullish`，则表达式将计算为 `undefined`。

因此，如果 `data` 是 `nullish`，则 `data?.saleObj` 将计算为 `undefined`。如果 `data` 不是 `nullish`，则将尝试访问 `saleObj` 属性。如果 `saleObj` 存在于 `data` 对象上，则返回它的值，否则返回 `undefined`。

以下是一个示例以说明这个语法：

```js 
const data = null;
console.log(data?.saleObj); // undefined

const data2 = { saleObj: { price: 10 } };
console.log(data2?.saleObj?.price); // 10

const data3 = { };
console.log(data3?.saleObj?.price); // undefined
```

#### 心愿便利贴  

- 考察点： element-ui  (表单验证 ) 

- 答案：

  ```html
  <div class="card" :class="item.css" v-for="(item,index) in    wishList" :key="index">
  <div>
  <script>
  const app = new Vue({
        // ......
				rules: {
					// TODO 待补充验证的代码
					name:[
						{ required: true, message: '请输入姓名', trigger: 'blur' },
						{ min: 2, max: 4, message: '长度在 2 到 4 个字符', trigger: 'blur' }
					],
					content:[
						{ required: true, message: '请输入内容', trigger: 'blur' },
						{ min: 1, max: 30, message: '长度在 1 到 30 个字符', trigger: 'blur' }
					]
				}
			 // ......
		 })
  </script>
   
  ```

#### 消失的 Token

- 考察点：Vue(Vuex 的基本使用)

- 答案：

```js
 var app = new Vue({
            el: '#app',
            data() { },
            computed: {
                welcome() {
                    return store.getters.welcome
                },
                username() {
                    // 第一处修改 
                    return store.getters['user/username']
                },
                token() {
                    // 第二处修改 
                    return store.getters['user/token']
                }
            },
            methods: {
                // 回车/点击确认的回调事件
                login(username) {
                    // 第三处修改 
                    username && store.commit('user/login', { username, token: 'sxgWKnLADfS8hUxbiMWyb' })
                    username && store.commit('say', '登录成功，欢迎你回来！')
                }
            }
        })
```
-  知识点解析 

`namespaced: true` 是在 Vuex 模块中的配置选项之一，它表示将该模块开启命名空间模式。

在 Vuex 中，模块系统可以将 `store` 分割成小模块，每个模块都有自己的状态、`mutation`、`action` 和 `getter` 等。命名空间模式是一种使模块更加封装的方法，它可以确保模块内部的 `mutation` 和 `getter` 只能访问该模块内部的状态，而不是整个应用程序的状态。

使用 `namespaced: true` 配置选项，可以为该模块启用命名空间模式，这意味着在访问该模块的 `mutation` 和 `getter` 时，需要通过模块名来限定。例如，在一个名为 `user` 的 Vuex 模块中，如果启用了命名空间模式，那么在该模块内部的 `mutation` 中，要访问该模块的 `state`，就需要使用 `state` 参数的形式，即 `context.state`，而在调用该模块的 `mutation` 或 `getter` 时，需要指定该模块的名称，例如：`store.commit('user/login')`。

命名空间模式可以有效地避免模块之间的状态冲突，提高代码的可维护性和可读性。但是，在使用命名空间模式时，需要注意模块之间的依赖关系，以及在模块之间传递参数时的命名方式等问题。

#### 封装 Promisefy 函数 （大学组）

- 考察点：ES6    promise、fs基本理解 

- 答案：

```js
function promisify(fn) {
  return function (...args) {
    return new Promise((resolve, reject) => {
      fn(...args, (err, result) => {
        if (err) {
          reject(err);
        } else {
          resolve(result);
        }
      });
    });
  };
}
```
下面是函数的详细解释：

- `function promisify(fn)` - promisify 函数使用一个回调函数作为参数，它将被转换为返回 Promise 的函数。
- `return function (...args)` - promisify 返回一个新函数，这个新函数接受任意数量的参数并将它们传递给原始函数。
- `return new Promise((resolve, reject) => { ... }` - promisify 返回的函数创建一个新的 Promise，当原始函数完成时将被解析。
- `fn(...args, (err, result) => { ... })` - promisify 执行原始函数并传递最后一个参数作为回调函数。回调函数期望两个参数：`err` 和 `result`。
- `if (err) { reject(err); } else { resolve(result); }` - 当原始函数完成时，回调函数将被执行。如果存在错误，则 Promise 将被拒绝为该错误；否则，Promise 将被解析为返回结果。

#### 虚拟滚动

- 考察点 ：vue  
- 答案：

```html
<template>
  <div id="virtual-list" class="virtual-list" ref="list" @scroll="onScroll">
    <!--用于撑起滚动区域高度的空白元素-->
    <div id="scroll-container" :style="{ height: totalHeight + 'px' }"></div>
    <!--展示列表的ul元素-->
    <ul
      id="list"
      class="list"
      ref="list"
      :style="{ transform: dynamicTranslate }"
    >
      <!--用v-for循环展示列表数据-->
      <li
        v-for="item in showingList"
        :key="item"
        :style="{ height: itemHeight + 'px', lineHeight: itemHeight + 'px' }"
      >
        {{ item }}
      </li>
    </ul>
  </div>
</template>
<script>
module.exports = {
  data() {
    return {
      itemHeight: 60, // 每一项的高度
      length: 10, // 初始展示的项数
      buffer: 5, // 预加载的项数
      list: [], // 数据列表
      totalHeight: 0, // 数据列表总高度
      scrollTop: 0, // 滚动条的位置
      start: 0, // 开始展示的项的索引
    };
  },
  computed: {
    showingList() {
      return this.list.slice(
        Math.max(0, this.start - this.buffer), // 起始索引（加上缓存）
        Math.min(this.start + this.buffer + this.length, this.list.length) // 结束索引（加上缓存和可见范围）
      );
    },
    dynamicTranslate() {
      const belowOffset = this.buffer * this.itemHeight; // 预加载项的总高度
      if (this.scrollTop <= belowOffset) { // 如果滚动距离小于等于预加载项的总高度，不需要滚动
        return `translate3d(0,0,0)`;
      }

      const startOffset =
        this.scrollTop - (this.scrollTop % this.itemHeight) - belowOffset; // 计算开始滚动的位置
      return `translate3d(0,${startOffset}px,0)`;
    },
  },
  methods: {
    onScroll() { // 监听滚动事件
      this.scrollTop = this.$refs.list.scrollTop; // 获取滚动条位置
      this.start = Math.floor(this.scrollTop / this.itemHeight); // 计算开始展示的索引
    },
  },
  mounted() { // 在组件挂载后获取数据
    axios.get("./data.json").then(({ data }) => {
      this.list = data; // 将数据存入列表
      this.totalHeight = this.itemHeight * this.list.length; // 计算数据列表总高度
      this.start = 0; // 初始化开始展示的索引
      this.scrollTop = 0; // 初始化滚动条位置
    });
  },
};
</script>
```

- 知识点解析

  **`computed` 计算属性**

  `computed` 计算属性用于根据已有的数据计算出新的数据，并且只有在相关数据发生变化时才会重新计算。在这段代码中，`computed` 计算属性主要用于计算列表的展示内容和滚动的位置。
    showingList`：根据 `start`、`length` 和 `buffer` 计算出当前需要展示的数据列表。
  `

  dynamicTranslate`：根据滚动条的位置和预加载项的总高度计算出需要滚动的位置，以实现虚拟滚动

  **虚拟列表的实现原理：**

  虚拟列表通过只渲染可见范围内的数据项，而不是渲染整个列表来提高性能。在这段代码中，虚拟列表的实现原理如下：

    - 通过计算出开始展示的项的索引和需要展示的项数，计算出当前需要展示的数据列表。
    - 通过计算出滚动条的位置和预加载项的总高度，计算出需要滚动的位置。
    - 将滚动位置应用到列表容器上，从而实现虚拟滚动。

