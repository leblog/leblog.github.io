---
title: Vue面试题汇总
top: false
cover: false
toc: true
mathjax: true
date: 2021-08-12 12:28:30
password:
summary:
tags: [web,vue]
categories: vue
---


# Vue面试题

## 谈谈对Vue的理解

~~~js
1. 渐进式 JavaScript 框架，轻量级框架，只关心视图层
2. 双向数据绑定，数据操作方面更为简单
3. 组件化开发，在构建单页面应用方面有着独特的优势
4. 虚拟DOM，减少DOM操作，性能更好
5. 运行速度更快
~~~



## 对MVVM的理解

~~~js
MVVM是双向数据绑定

1. M 是 Model 数据层
2. V 是 View 视图层
3. VM 是 ViewModel 数据和视图的监听层，当数据或视图发生改变时，VM层能监听到，同时把对应的另外一层改变或者重新渲染（Vue就是VM监听层）
	数据层改变，vm会帮助我们重新渲染视图
	视图层改变，vm会帮我们把数据重新更改
~~~



## Vue的双向数据绑定原理

~~~js
vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter、getter，在数据变动时发布消息给订阅者，触发相应的监听回调
~~~



## Vue生命周期

总共分为8个阶段创建前/后，载入前/后，更新前/后，销毁前/后

~~~js
1. beforeCreate(): 创建前，data、methods、computed以及watch上的数据和方法都不能被访问

2. created(): 创建后，实例创建完成，可以操作 data、method 里的数据，可以进行一些数据、资源的请求

3. beforeMount(): 挂载前，当前阶段虚拟 Dom 已经创建完成，即将开始渲染

4. mounted(): 挂载后，真实的 Dom 挂载完毕，数据完成双向绑定，可以访问到Dom节点，使用$refs属性对Dom进行操作

5. beforeUpdate(): 更新前，也就是响应式数据发生更新，虚拟dom重新渲染之前被触发，你可以在当前阶段进行更改据，不会造成重渲染

6. updated(): 更新后，可以执行依赖于 DOM 的操作，但是要避免更改状态，可能会导致更新无线循环

7. beforeDestory(): 销毁前，在当前阶段实例完全可以被使用

8. destoryed(): 销毁后，这个时候只剩下了dom空壳，可以执行一些优化操作，清空计时器，解除绑定事件
~~~



![img](https://vmhandsel.oss-cn-shenzhen.aliyuncs.com/1597714975344.png)



## vue组件中data必须是一个函数

~~~js
1. vue组件是可以被用来创建多个实例的，如果data是一个对象的话，那么所有实例就将共享同一个data对象，这种情况下修改其中一个实例的data属性，会带来其他的组件也被修改

2. 组件之间的数据是相对独立，互不影响才符合组件的思想

3. data设置为函数的形式后，每次创建组件实例，data都是一个全新的对象副本，这样达到了相互独立的目标
~~~



## Vue的DOM操作是同步还是异步？

~~~js
vue中对DOM的操作都是异步的
当 this.name = 'hello' 修改data后，视图view不会立即发生
而是vue会把此次DOM操作放到事件队列里，待一定时机后，在更新队列里的操作
~~~



## computed和watch的区别

**计算属性：computed**

~~~js
1. 支持缓存，只有依赖数据发生改变，才会重新进行计算

2. 不支持异步，当computed内有异步操作时无效，无法监听数据的变化

3. computed 属性值会默认走缓存，计算属性是基于它们的响应式依赖进行缓存的，也就是基于data中声明过或者父组件传递的props中的数据通过计算得到的值

4. 如果一个属性是由其他属性计算而来的，这个属性依赖其他属性，是一个多对一或者一对一，一般用computed

5. 如果computed属性属性值是函数，那么默认会走get方法；函数的返回值就是属性的属性值；在computed中的，属性都有一个get和一个set方法，当数据变化时，调用set方法
~~~



**监听属性：watch**

~~~js
1. 不支持缓存，数据表，直接会触发相应的操作

2. watch支持异步

3. 监听的函数接收两个参数，第一个参数是最新的值；第二个参数是输入之前的旧值

4. 当一个属性发生变化时，需要执行对应的操作；一对多

5. 监听数据必须是data中声明过或者父组件传递过来的props中的数据，当数据变化时，触发其他操作，函数有两个参数
~~~



> immediate：组件加载立即触发回调函数执行

~~~js
watch: {
  firstName: {
    handler(newName, oldName) {
      this.fullName = newName + ' ' + this.lastName;
    },
    // 代表在wacth里声明了firstName这个方法之后立即执行handler方法
    immediate: true
  }
}
~~~

> deep: deep的意思就是深入观察，监听器会一层层的往下遍历，给对象的所有属性都加上这个监听器，但是这样性能开销就会非常大了，任何修改obj里面任何一个属性都会触发这个监听器里的 handler

~~~js
watch: {
  obj: {
    handler(newName, oldName) {
      console.log('obj.a changed');
    },
    immediate: true,
    deep: true
  }
}
~~~

优化：我们可以使用字符串的形式监听

~~~js
watch: {
  'obj.a': {
    handler(newName, oldName) {
      console.log('obj.a changed');
    },
    immediate: true,
    // deep: true
  }
}
~~~

这样Vue.js才会一层一层解析下去，直到遇到属性a，然后才给a设置监听函数



## v-if 和 v-show 区别

~~~js
// 相同点
都能动态的控制元素的显示和隐藏

// 不同点
v-if： 是动态的添加或删除dom元素（通过销毁和重建DOM元素）
v-show： 通过CSS的display属性：none和block控制显示隐藏

// 总结：
如果需要频繁切换某节点，使用 v-show（初始渲染开销较大，切换开销比较小）
如果不需要频繁切换某节点，使用 v-if（初始渲染开销较小，切换开销比较大）
~~~





## vue中$nextTick有什么作用

~~~js
处理数据动态变化后，dom还未及时更新的问题。$nextTick就可以获取到数据更新后最新的dom变化
~~~



## 对keep-alive的了解

~~~js
keep-alive是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染
~~~



## vue-loader是什么

~~~js
vue文件的一个加载器，跟template/js/style转换成js模块
~~~



## v-modal的使用

~~~js
v-model 用于表单数据的双向绑定，其实它就是一个语法糖，这个背后就做了两个操作：
v-bind 绑定一个value属性；
v-on 指令给当前元素绑定input事件
~~~



## v-for key的作用

~~~js
1. 在对节点进行diff的过程中，判断是否为相同节点的一个很重要的条件是key是否相等，如果是相同节点，则会尽可能的复用原有的DOM节点
2. 需要使用key来给每个节点做一个唯一标识，Diff算法就可以正确的识别此节点。
3. 作用主要是为了高效的更新虚拟DOM
~~~



## v-for 和 v-if 为什么不能连用

~~~js
v-for 会比 v-if 的优先级更高，连用的话会把 v-if 的每个元素都添加一下，造成性能问题
~~~



## v-on可以监听多个方法吗

~~~vue
可以
<input type="text" v-on="{ input: onInput, focus: onFocus, blur: onBlur, }" />
~~~



## 组件传值

**父传子**

通过props传递

~~~js
父组件： <child value = '传递的数据' />

子组件: props['value'],接收数据,接受之后使用和data中定义数据使用方式一样
~~~



**子传父**

在父组件中给子组件绑定一个自定义的事件，子组件通过$emit()触发该事件并传值

~~~js
父组件： <child @click = 'onClick' />

子组件: this.$emit('click','传递的数据')
~~~



**兄弟组件传值**

1、通过中央通信 let bus = new Vue()

~~~js
A：methods :{ 函数{bus.$emit('自定义事件名'，数据) } 发送

B：created （）{ bus.$on('A发送过来的自定义事件名'，函数) } 进行数据接收
~~~

2、通过vuex



## vue如何获取dom

先给标签设置一个ref值，再通过this.$refs.domName获取，例如：

~~~vue
<div ref="test"></div>

const dom = this.$refs.test
~~~



## vue常用的修饰符

~~~
.stop：等同于JavaScript中的event.stopPropagation()，防止事件冒泡

.prevent：等同于JavaScript中的event.preventDefault()，防止执行预设的行为（如果事件可取消，则取消该事件，而不停止事件的进一步传播

.capture：与事件冒泡的方向相反，事件捕获由外到内

.self：只会触发自己范围内的事件，不包含子元素

.once：只会触发一次
~~~



## vue如何监听对象或数组某个属性的变化

当在项目中直接设置数组的某一项的值，或者直接设置对象的某个属性值，这个时候，你会发现页面并没有更新。这是因为Object.defineprototype()限制，监听不到变化

**解决方式**

> this.$set(你要改变的数组/对象，你要改变的位置/key，你要改成什么value)

~~~js
this.$set(this.arr, 0, "李四"); // 改变数组

this.$set(this.obj, "name", "张三"); // 改变对象
~~~



**vue更新数组时触发视图更新的方法**

~~~js
push()、pop()、shift()、unshift()、splice()、sort()、reverse()
~~~

意思是使用这些方法不用我们再进行额外的操作，视图自动进行更新。推荐使用splice方法会比较好自定义,因为splice可以在数组的任何位置进行删除/添加操作



## assets和static的区别

~~~js
// 相同点
1. assets 和 static 两个都是用来存放静态资源文件
2. 项目中所需要的资源文件图片、字体图标、CSS样式文件等都可以放在这两个目录下

// 不同点
1. assets 中存放的静态资源文件在项目打包时，即：在运行 npm run build 时，会将 assets 中放置的静态资源文件进行打包上传（所谓打包，简单点可以理解为压缩体积、代码格式化），而压缩后的静态资源文件最终也都会放置在 static 目录中跟着 index.html 一同上传至服务器

2. static 中存放的静态资源文件不会要走打包压缩格式化等流程，而是直接进入打包好的目录，直接上传至服务器。因为避免了压缩直接进行上传，在打包时会提高一定的效率，但是 static 中的资源文件由于没有进行压缩等操作，所以文件的体积也就相对于 assets 中打包后的文件提交大一点儿，在服务器中就会占据更大的空间
~~~

​	注：将项目中 template 需要的样式文件、 js 文件等都可以放置在 assets 中，走打包这一流程，减少体积；而项目中引入的第三方的资源文件，如：iconfont.css 等文件可以放置在 static 中，因为这些引入的第三方文件已经经过处理，我们不再需要处理，直接上传





## Vuex是什么

~~~js
Vuex 是一个专为 Vue.js应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化

一共有5个核心属性：

state 唯一数据源,Vue 实例中的 data 遵循相同的规则

getters 可以认为是 store 的计算属性,就像计算属性一样，getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。Getter 会暴露为 store.getters 对象，你可以以属性的形式访问这些值

mutation 更改 Vuex 的 store 中的状态的唯一方法是提交 mutation,非常类似于事件,通过store.commit 方法触发

action类似于 mutation，不同在于Action 提交的是 mutation，而不是直接变更状态，Action 可以包含任意异步操作

module 由于使用单一状态树，应用的所有状态会集中到一个比较大的对象。当应用变得非常复杂时，store 对象就有可能变得相当臃肿。为了解决以上问题，Vuex 允许我们将 store 分割成模块（module）
~~~





## vuex中的数据在页面刷新后数据消失

用sessionstorage 或者 localstorage 存储数据

~~~js
存储：localStorage.setItem( '名', JSON.stringify(值) )

使用：localStorage.getItem('名') ---得到的值为字符串类型，用JSON.parse()去引号
~~~





## vue哪几种情况会视图不更新

**数组数据变动，使用某些方法操作数组，变动数据时，有些方法无法被vue监测**

~~~js
push()，pop()，shift()，unshift()，splice()，sort()，reverse() 可被vue检测到

filter(), concat(), slice() 这些不会改变原始数组，但总是返回一个新数组。当使用非变异方法时，可以用新数组替换旧数组

vue不能检测以下变动的数组：
1. 当你利用索引直接设置一个项时，vm.items[index] = newValue
2. 当你修改数组的长度时，例如： vm.items.length = newLength
~~~



**对象属性的添加或删除**

由于 Vue 会在初始化实例时对属性执行 getter/setter 转化过程，所以属性必须在 data 对象上存在才能让 Vue 转换它，这样才能让它是响应的

~~~js
// 解决办法：
使用 Vue.set(object, key, value) 方法将响应属性添加到嵌套的对象上

Vue.set(vm.someObject, 'b', 2) 或者 this.$set(this.someObject,'b',2) （这也是全局 Vue.set 方法的别名）
~~~



**vue多层循环，动态改变数据后渲染的很慢或者不渲染**

~~~js
// 可在动态改变数据的方法，第一行加上
this.$forceUpdate();
~~~



## 什么是vue-router

~~~js
Vue Router 是 Vue.js 官方的路由管理器。它和 Vue.js 的核心深度集成，让构建单页面应用变得易如反掌。包含的功能有：

- 嵌套的路由/视图表
- 模块化的、基于组件的路由配置
- 路由参数、查询、通配符
- 基于 Vue.js 过渡系统的视图过渡效果
- 细粒度的导航控制
- 带有自动激活的 CSS class 的链接
- HTML5 历史模式或 hash 模式，在 IE9 中自动降级
- 自定义的滚动条行为
~~~



## router和route的区别

~~~js
$router 是路由实例对象，包含了路由的跳转方法，钩子函数等

$route 是当前路由内的路由信息对象，包括path、params、hash、query、name等属性信息
~~~



## vue的query和params区别

~~~js
用法：query要用path来引入，params要用name来引入，接收参数都是类似的，分别是
this.$route.query.name 和 this.$route.params.name

url地址显示：query更加类似于get传参，params则类似于post，说的再简单一点，前者在浏览器地址栏中显示参数，后者则不显示
注意点：query刷新不会丢失query里面的数据
~~~



**传参和接收参数**

~~~js
// 传参: 
this.$router.push({
        path:'/xxx',
        query:{
          id:id
        }
      })
  
// 接收参数:
this.$route.query.id
~~~

~~~js
// 传参: 
this.$router.push({
        name:'xxx',
        params:{
          id:id
        }
      })
  
// 接收参数:
this.$route.params.id
~~~

params传参，push里面只能是 name:'xxxx'，不能是path:'/xxx'，因为params只能用name来引入路由，如果这里写成了path，接收参数页面会是undefined

**路由设置**

使用params方法传参的时候，要在路由后面加参数名，而query方法，就没有这种限制

~~~js
{
    path: '/index/:id', // 接收参数的路由，使用params传参要加参数名，这里的id就是参数名
    name: 'index',
    component: () => import('./view/index'),
}
~~~

使用params方法，如果路由上面不写参数，也是可以传过去的，但不会在url上面显示出你的参数，并且当你跳到别的页面或者刷新页面的时候**参数会丢失**



总结：使用query传参的话，会在浏览器的url栏看到传的参数类似于get请求，使用params传参的话则不会，类似于post请求





## vue路由 hash 和 history 区别

|          | hash                     | history          |
| -------- | ------------------------ | ---------------- |
| url显示  | 有#                      | 无#              |
| 回车刷新 | 可以加载到hash值对应页面 | 一般就是404掉了  |
| 支持版本 | 支持低版本和IE浏览器     | HTML5新推出的API |

~~~
1. hash(默认) —— hash 模式 url 里面永远带着 # 号,我们在开发中默认使用这个模式
比如这个 URL：http://www.abc.com/#/hello，hash 的值为 #/hello。它的特点在于：hash 虽然出现在 URL 中，但不会被包括在 HTTP 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面

2. history —— 利用了 HTML5 History Interface 中新增的 pushState() 和 replaceState() 方法
~~~

当然啦，history 也不是样样都好。SPA 虽然在浏览器里游刃有余，但真要通过 URL 向后端发起 HTTP 请求时，两者的差异就来了。尤其在用户手动输入 URL 后回车，或者刷新（重启）浏览器的时候。

hash 模式下，仅 hash 符号之前的内容会被包含在请求中，如 http://www.abc.com，因此对于后端来说，即使没有做到对路由的全覆盖，也不会返回 404 错误。

history 模式下，前端的 URL 必须和实际向后端发起请求的 URL 一致，如 http://www.abc.com/book/id。如果后端缺少对 /book/id 的路由处理，将返回 404 错误。Vue-Router 官网里如此描述：“不过这种模式要玩好，还需要后台配置支持……所以呢，你要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。

history模式怕啥
通过history api，我们丢掉了丑陋的#，但是它也有个毛病：
不怕前进，不怕后退，就怕刷新，f5，（如果后端没有准备的话）,因为刷新是实实在在地去请求服务器的,不玩虚的。

在hash模式下，前端路由修改的是#中的信息，而浏览器请求时是不带它玩的，所以没有问题.但是在history下，你可以自由的修改path，当刷新时，如果服务器中没有相应的响应或者资源，会分分钟刷出一个404来



## Vue性能优化

- 事件代理
- `keep-alive`
- 拆分组件
- `key` 保证唯一性
- 路由懒加载、异步组件
- 防抖节流

- 第三方模块按需导入（` babel-plugin-component` ）
- 图片懒加载



## vue初始化页面闪动问题

~~~css
使用vue开发时，在vue初始化之前，由于div是不归vue管的，所以我们写的代码在还没有解析的情况下会容易出现花屏现象，看到类似于
{{ message }} 的字样，虽然一般情况下这个时间很短暂，但是我们还是有必要让解决这个问题的。
首先：在css里加上
[v-cloak] {
	display: none;
}
~~~





## 提高首屏加载速度的优化方案

~~~js
1. 采用路由懒加载
2. 将一些静态js css放到其他地方（如OSS），减小服务器压力
3. 按需加载三方资源，如element,建议按需引入element中的组件
4. 使用nginx开启gzip减小网络传输的流量大小
5. webpack开启gzip压缩
6. 若首屏为登录页，可以做成多入口，登录页单独分离为一个入口
7. 图片懒加载方案
~~~



## 单页面应用和多页面应用区别及优缺点

~~~js
答：
单页面应用（SPA），通俗一点说就是指只有一个主页面的应用，浏览器一开始要加载所有必须的 html, js, css。所有的页面内容都包含在这个所谓的主页面中。但在写的时候，还是会分开写（页面片段），然后在交互的时候由路由程序动态载入，单页面的页面跳转，仅刷新局部资源。多应用于pc端。

多页面（MPA），就是指一个应用中有多个页面，页面跳转时是整页刷新
单页面的优点：
用户体验好，快，内容的改变不需要重新加载整个页面，基于这一点spa对服务器压力较小；前后端分离；页面效果会比较炫酷（比如切换页面内容时的专场动画）

单页面缺点：
不利于seo；导航不可用，如果一定要导航需要自行实现前进、后退。（由于是单页面不能用浏览器的前进后退功能，所以需要自己建立堆栈管理）；初次加载时耗时多；页面复杂度提高很多
~~~

