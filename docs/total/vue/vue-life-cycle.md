## Vue Life Cycle (生命周期) (★★★★★)

### 1.1 生命周期

> 一个vue组件从 创建 到 销毁 的整个过程就是生命周期 

### 1.2  钩子函数

> 目标: **Vue** 框架内置函数，随着组件的生命周期阶段，自动执行

作用: 特定的时间点，执行特定的操作

场景: 组件创建完毕后，可以在created 生命周期函数中发起Ajax 请求，从而初始化 data 数据

分类: 4大阶段8个方法

- 初始化

- 挂载

- 更新

- 销毁

| **阶段** | **方法名**    | **方法名** |
| -------- | ------------- | ---------- |
| 初始化   | beforeCreate  | created    |
| 挂载     | beforeMount   | mounted    |
| 更新     | beforeUpdate  | updated    |
| 销毁     | beforeDestroy | destroyed  |



![Day03](https://extraordinary-palmier-f8e65a.netlify.app/06-vue%E5%9F%BA%E7%A1%80/vue05/vue05/images/Day03.png)


```js

Vue.component( 'Hello',{
    template: '#hello',
    data () { //除了根式
      return {
        num: 920
      }
    },
    //------------------------------------初始化------------------------
    beforeCreate () { 
      /* 
        这个阶段：组件创建前
          data  data选项中的数据获取不到
          RDOM  拿不到
          项目中： 没什么用
          但是这个阶段是一个对事件和生命周期的准备阶段，也是必不可少的
      */
    },
    created () { // 组件创建结束
       /* 
        这个阶段：
          data  data选项中的数据获到了
          RDOM  拿不到
          项目中： 
              数据的修改
              异步数据请求
      */
    },
    beforeMount () { //组件即将挂载
        /* 
        这个阶段：
          data  data选项中的数据获到了
          RDOM  拿不到
          项目中： 
              数据的修改
              异步数据请求
      */
    },
    mounted () { //组件挂载结束了
      /* 
        这个阶段：
          data: 可以获得数据
          RDOM: 拿到了
          项目中： 
              数据修改
              异步数据请求
              真实DOM操作可以了( Vue一般情况下不要直接操作真实DOM, 一般可以进行第三方库的实例化（静态数据渲染来的）  )

     */
    },
    // ------------------------------------运行中---------------------
    beforeUpdate () { //表示组件即将更新   vdom --diff--> vdom的不同（patch对象）
      /* 
        这个阶段： 
          data: 拿到了
          RDOM： 获得
          这个阶段进行的是vdom的生成和diff算法的对比，都是内部进行的，我们在项目中可以不使用
       */
    },
    updated () { // 组件更新结束 ， 通过render函数将vdom渲染成了真实dom,然后驱动vue进行视图更新
      /* 
        这个阶段：
           动态数据的渲染，进行dom操作（ 第三方库的实例化 ）
       */
    },
    // --------------------------------------销毁 -------------
    beforeDestroy () {
    },
    destroyed () {
    }
  })
```



![img](https://img-blog.csdnimg.cn/20200515103424403.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzIyMTMyMw==,size_16,color_FFFFFF,t_70)



### 1.3  初始化阶段

> 目标: 掌握初始化阶段2个钩子函数作用和执行时机


含义讲解:

1.new Vue() – Vue实例化(组件也是一个小的Vue实例)

2.Init Events & Lifecycle – 初始化事件和生命周期函数

3.beforeCreate – 生命周期钩子函数被执行

4.Init injections&reactivity – Vue内部添加data和methods等

5.created – 生命周期钩子函数被执行, 实例创建

6.接下来是编译模板阶段 –开始分析

> 问： 此时，页面上的html结构构建出来了吗？？？？换句话来说，create初始化阶段可以获取到真是DOM吗？
> 

> 总结 ：beforeCreate  无法获取到 data 中的数据 和 方法 等
>
> created 可以获取 data 中的数据 和 方法 等  **（常用钩子函数）**



### 1.4 挂载阶段

> 目标: 掌握挂载阶段2个钩子函数作用和执行时机

1.template选项检查

 有 - 编译template返回render渲染函数

 无 – 编译el选项对应标签作为template(要渲染的模板)（非脚手架）

2.虚拟DOM挂载成真实DOM之前

3.beforeMount – 生命周期钩子函数被执行

4.Create … – 把虚拟DOM和渲染的数据一并挂到真实DOM上

5.真实DOM挂载完毕

6.mounted – 生命周期钩子函数被执行

**注意：**

- 一般工作中主要会用到created和mounted这两个生命周期。

1. 可以在created中修改data中的数据，以及注册全局事件，**不可以去查询DOM元素**
2. 可以在mounted中做所有created中可以执行的事件，也可以在这个时期去查询DOM元素
3. 以上 - 可以直接只用mounted确保万无一失

> 总结 ：beforeMount  不能获取到 dom 元素 它能获取 数据和方法 但是这些 cerated 就可以做到
>
> mounted 可以获取到挂载后的 真实 dom 对 dom 元素进行一个操作 **（常用钩子函数）**



### 1.5 更新阶段 

> 目标: 掌握更新阶段2个钩子函数作用和执行时机

含义讲解:

1.当data里数据改变, 更新DOM之前

2.beforeUpdate – 生命周期钩子函数被执行

3.Virtual DOM…… – 虚拟DOM重新渲染, 打补丁到真实DOM

4.updated – 生命周期钩子函数被执行

5.当有data数据改变 – 重复这个循环

**问：**

1. 什么时候执行updated钩子函数?

   当数据发生变化并更新页面后

2. 在哪可以获取更新后的DOM?

   在updated钩子函数里

**注意：**

1. 更新阶段有这样一种情景：如果在update更新阶段时对数据做了新的处理，可能又会触发update更新阶段，以此往复会出现修改一次数据触发多次更新阶段逻辑的过程，这样会出现项目代码执行效率低下，**在开发过程中，尽量不要去使用update的两个生命周期，如果需要监听某个值的改变应该用到watch！**

> 总结：beforeUpdate  数据更新之前执行的
>
> updated 数据更新后执行 但是数据更新 会重复这个循环  
>
> 所以正常人 都不使用  beforeUpdate   updated ，而是使用 watch 去替代这个两个钩子函数



### 1.6  销毁阶段

> 目标: 掌握销毁阶段2个钩子函数作用和执行时机

含义讲解:

1.当$destroy()被调用 – 比如组件DOM被移除(例v-if)

2.beforeDestroy – 生命周期钩子函数被执行

3.拆卸数据监视器、子组件和事件侦听器

4.实例销毁后, 最后触发一个钩子函数

5.destroyed – 生命周期钩子函数被执行

**注意：**

1. 销毁阶段一般是拿来销毁一些全局事件, 移除当前组件, 计时器, 定时器，特别注意！如果子组件中涉及到定时器`setInterval`时，一定注意当组件销毁时这个定时器是否关闭`clearInterval`

> 总结：beforeDestroy  会执行一些 异步事件，定时器
>
> destroyed  组件销毁后 执行



## Axios  (★★★★★)

### 2.1 axios基本使用

> axios是基于原神ajax+Promise技术封装通用于前后端的请求库
>
> 其原理为： 浏览器window接口的XMLHttpRequest
>
> [axios文档](http://www.axios-js.com/)

**特点**

- 支持客户端发送Ajax请求
- 支持服务端Node.js发送请求
- 支持Promise相关用法
- 支持请求和响应的拦截器功能
- 自动转换JSON数据

**axios 底层还是原生js实现, 内部通过Promise封装的**

**axios的基本使用**

```js
axios({
  method: '请求方式', // get post delete put
  url: '请求地址',
  data: {    // 拼接到请求体的参数,  post请求的参数
    xxx: xxx,
  },
  params: {  // 拼接到请求行的参数, get请求的参数
       xxx: xxx 
  }
}).then(res => {
  console.log(res.data) // 后台返回的结果
}).catch(err => {
  console.log(err) // 后台报错返回
})
```

 

### 2.2 获取数据 - get请求

1. 创建一个组件 设置基本结构

2. 在App.vue 里面 引入该组件 （引入组件三步曲 ）
- import 引入
- components 注册组件
- template 里面挂载 组件

3. 下载`axios `
```
npm i axios
```

4. 引入`axios`
```js
import axios from "axios";
```

> 思考：如果只在这个地方引入 `axios` 在其他组件里面使用 还需要引入，有什么更好的办法解决这个问题啊？


5. 发送`axios`请求
```vue
<template>
  <div>
    <p>1. 获取所有图书信息</p>
    <button @click="getAllFn">点击-查看控制台</button>
  </div>
</template>

<script>
    import axios from "axios";
    // 4. 全局配置
    axios.defaults.baseURL = "http://123.57.109.30:3006"
    export default {
        methods: {
            getAllFn() {
                axios({
                    method: "GET", // 默认就是GET方式请求, 但不准省略
                    url: "/api/getbooks"
                }).then((res) => { // axios()-原地得到Promise对象
                    console.log(res)
                }). catch((err) => {
                    console.log(err)
                })
            }
        }
    };
</script>
```


### 2.3 `axios` 的 POST请求

发起axios请求

```js
<script>
    import axios from "axios";
    axios.defaults.baseURL = "http://123.57.109.30:3006"
    export default {
        methods: {
            sendFn(){
                axios({
                    url: "/api/addbook",
                    method: "POST",
                    data: {
                        appkey: "7250d3eb-18e1-41bc-8bb2-11483665535a",
                        ...this.bookObj
                        //等同于下面
                        //    bookname: this.bookObj.bookname,
                        //    author: this.bookObj.author,
                        //    publisher: this.bookObj.publisher
                    }
                }).then((res) => {
                    alert('添加图书成功')
                })
            }
        }
    };
</script>
```

代码规范优化：

GET 请求代码优化：

```js
export default {
  data() {
    return {
      list: [],
    };
  },
  created() {
    this.getList();
  },
  methods: {
    getList() {
      //获取购物车列表数据接口
      this.$axios({
        methods: "GET",
        url: "/api/cart",
      })
        .then((res) => {
          console.log(res);
          // 将res.data.list 赋值给 list 变量
          this.list = res.data.list;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
```

POST 请求代码优化：

```js
<script>
// 1. 引入axios 依赖
axios.defaults.baseURL = "http://123.57.109.30:3006";
import axios from "axios";
export default {
    // 新增图书
    senFn() {
      // 1. 创建 入参 对象
      let params = {
        bookname: this.bookObj.bookname,
        author: this.bookObj.author,
        publisher: this.bookObj.publisher,
      };
      //   2. 调用接口
      axios({
        method: "POST",
        url: "/api/addbook",
        data: params,
      })
        .then((res) => {
          console.log(res.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
```

规范一：GET请求传参使用` params`  POST请求传参使用` data`

规范二：虽然在我们的结构 `params` 和 `data `是键值对的形式存在 就是可以直接把赋值给到` params` 和 `data `里面

```js
// data 或者 params 传的值写在里面，但是这是目前传值很少，但是如果传值很多 这样写会容易出错	
			axios({
                    url: "/api/addbook",
                    method: "POST",
                    data: {                 
                       bookname: this.bookObj.bookname,
                       author: this.bookObj.author,
                       publisher: this.bookObj.publisher
                    }
                }).then(callback).catch(callback)
//所以推荐使用第二种  把需要传的参数 创建一个对象 保存 后面赋值给对应的 data 或者 params
// 1. 创建 入参 对象
 let params = {
        bookname: this.bookObj.bookname,
        author: this.bookObj.author,
        publisher: this.bookObj.publisher,
      };
      //   2. 调用接口
      axios({
        method: "POST",
        url: "/api/addbook",
        data: params,
      }).then(callback).catch(callback)
```

规范三：我们 在 当前组件 引入的 `axios` 依赖  只能让 `axios` 作用于当前组件，如果其他组件也需要发送请求 还需要再次引入

所以我们可以 把 引入这一步放到 入口文件 `mian.js` 里面，另外我们使用 axios 想像 	`this.$emit `   `this.$refs` 一样使用，和一个`baseURL`的一个全局使用 我们一般在	`mian.js` 里面这样书写

```js
// 全局配置 axios 
import axios from 'axios'
// 配置全局 url 地址
axios.defaults.baseURL = 'https://www.escook.cn'
// 3. axios方法添加到Vue的原型上 
// 可以在每个组件中使用 this.$axios 来进行使用
Vue.prototype.$axios = axios
```



## vue 实例方法 - $refs  (★★★★★)

### 3.1 `$refs` - 获取DOM元素

> 目标: 利用 ref 和 $refs 可以用于获取 dom 元素

3.1.1 使用 `ref`和`$refs`获取 dom 元素

```vue
<template>
  <div>
    <h2>获取DOM元素</h2>
    <div id="myDiv">我是div</div>
    <h2>通过ref获取DOM元素</h2>
    <!-- 1. 在需要获取元素上 添加ref属性 为这个标签添加标记 -->
  </div>
</template>
<script>
export default {
  /**
   * 功能 1
   * $refs 可以代替 document.querySelector 获取
   */
  mounted() {
    console.log(document.querySelector("#myDiv"));
    // 2. 通过$refs 来有该标记的元素进行查找
    console.log(this.$refs.myRefDiv); 
  },
};
</script>
```

> 总结 ：获取dom元素 去操作dom元素 ，在vue 里面是很少做的事情，只是说可以使用，但是一般不用
>
> ref 最常使用的是 **获取组件中的 对象 方法** 就是下面提到的 功能 2

### 3.2 获取组件中的 对象 方法 (*****)

3.2.1 创建一个 子组件  里面有数据 和 一个方法

```vue
<template>
  <div>
    我是refs的child
  </div>
</template>

<script>
export default {
  data() {
    return {
      obj: {
        name: "shiqi",
        age: 20,
      },
    };
  },
  methods: {
    fn(){
        console.log('fn方法是refs的子组件')
    }
  },
};
</script>
```

3.2.1 获取组件中的 对象 方法

```vue
<template>
  <div>
    <!-- 1. 在需要获取元素上 添加ref属性 为这个标签添加标记 -->
    <refs-child ref="refsChild"></refs-child>
  </div>
</template>
<script>
import refsChild from "./04-refsChild.vue";
export default {
  /**
   * 功能 2
   * $refs 获取组件中的 对象 方法
   */
  mounted() {
    // 2.  获取组件
    let template = this.$refs.refsChild;
    console.log(template.obj);
    console.log(template.fn());
  },
  components: {
    refsChild,
  },
};
</script>

```





## vue - nextTick使用(★★★★★)

> Vue更新DOM-异步的!（数据与页面有延时）

> 案例：点击count++, 马上通过"原生DOM"拿标签内容, 无法拿到新值

步骤：

1. 在 `components/Move.vue` 中添加以下代码

   ```vue
   <template>
     <div>
         <p>3. vue更新DOM是异步的</p>
         <p ref="myP">{{ count }}</p>
         <button @click="btn">点击count+1, 马上提取p标签内容</button>
     </div>
   </template>
   
   <script>
   import Demo from './Child/Demo'
   export default {
       methods: {
           btn(){
               this.count++; // vue监测数据更新, 开启一个DOM更新队列(异步任务)
               console.log(this.$refs.myP.innerHTML); // 0
           }
       }
   }
   </script>Copy to clipboardErrorCopied
   ```

   发现： 页面数据更改了，但从页面上拿到的dom元素中的值还是更改前的数据

2. 使用`$nextTick()`

   等DOM更新后，触发`$nextTick()`的函数体执行

   ```vue
   <template>
     <div>
         <p>3. vue更新DOM是异步的</p>
         <p ref="myP">{{ count }}</p>
         <button @click="btn">点击count+1, 马上提取p标签内容</button>
     </div>
   </template>
   
   <script>
   import Demo from './Child/Demo'
   export default {
       methods: {
           btn(){
               this.count++; // vue监测数据更新, 开启一个DOM更新队列(异步任务)
               // console.log(this.$refs.myP.innerHTML); // 0
   
               // 原因: Vue更新DOM异步
               // 解决: this.$nextTick()
               // 过程: DOM更新完会挨个触发$nextTick里的函数体
               this.$nextTick(() => {
                   console.log(this.$refs.myP.innerHTML); // 1
               })
           }
       }
   }
   </script>Copy to clipboardErrorCopied
   ```

### 面试背点01 - nextTick实现原理

1. `nextTick`是`Vue`提供的一个全局`API`，是下次`DOM`更新循环结束之后执行延时回调，在修改之后使用`$nextTick`，则可以再回调中获取更新后的`DOM`
2. vue在更新DOM时是异步执行的。只要侦听到数据变化，`vue`将开启1个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个`watcher`被多次触发，只会推入到队列中1次。这种在缓冲时去除重复数据对于避免不必要的计算和`DOM`操作非常重要的。`nextTick`方法会在队列中加入一个回调函数，确保该函数在前面的`DOM`操作完成后才调用。

[源代码查看](https://extraordinary-palmier-f8e65a.netlify.app/#/)

