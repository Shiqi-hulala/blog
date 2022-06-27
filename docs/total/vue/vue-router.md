# vue-router

分析：

1. 下载vue-router模块到当前项目
2. 在main.js中引入VueRouter函数
3. 在Vue.use()上，添加全局RouterLink和RouterView组件
4. 创建**路由规则**数组（路由结构） - 保证路径和组件名称一一对应
5. 利用规则生产路由对象
6. 把路由对象注入到new Vue实例中
7. 用router-view作为挂载点，切换不同的路由页面
8. [vue-router文档](https://v3.router.vuejs.org/zh/)

步骤：

#### 1.  安装

   ```bash
   // 1. 下载vue-router
   yarn add vue-router@3.5.1
   ```

#### 2. 在main.js 中导入路由

   ```js
   // 2. 引入
   import VueRouter from 'vue-router'
   ```

#### 3. 使用路由插件

   ```js
   // 在vue中，使用使用vue的插件，都需要调用Vue.use()
   // 3. 注册全局组件
   Vue.use(VueRouter)
   ```

#### 4. 创建路由规则数组

```js
import Find from './views/Find.vue' // @是src的绝对地址
import My from './views/My.vue'
import Part from './views/Part.vue'
// 4. 规则数组
const routes = [
  {
    path: "/find", // 路由
    component: Find // 组件名称
  },
  {
    path: "/my",
    component: My
  },
  {
    path: "/part",
    component: Part
  }
]
```

Find.vue

```vue
<template>
  <div>
    <p>推荐</p>
    <p>排行榜</p>
    <p>歌单</p>
  </div>
</template>
```

My.vue

```vue
<template>
  <div>
      <p>我的收藏</p>
      <p>我的历史记录</p>
  </div>
</template>
```

Part.vue

```vue
<template>
  <div>
      <p>关注明星</p>
      <p>发现精彩</p>
      <p>寻找伙伴</p>
      <p>加入我们</p>
  </div>
</template>
```

#### 5. 创建路由对象 - 传入规则

```js
   // 5. 生成路由对象（传入配置对象）
   const router = new VueRouter({
     routes,// routes是固定key(传入规则数组)
   })
```

#### 6. 关联到vue实例

```js
   new Vue({
     router
   })
```

#### 7. 设置App.vue引入挂载路由组件

```vue
   <template>
     <div>
       <div class="footer_wrap">
         <a href="#/find">发现音乐</a>
         <a href="#/my">我的音乐</a>
         <a href="#/part">朋友</a>
       </div>
       <div class="top">
         <!-- 7. 设置挂载点-当url的hash值路径切换, 显示规则里对应的组件到这 -->
         <router-view></router-view>
       </div>
     </div>
   </template>
   
   <script>
   export default {};
   </script>
   
   <style scoped>
   .footer_wrap {
     position: fixed;
     left: 0;
     top: 0;
     display: flex;
     width: 100%;
     text-align: center;
     background-color: #333;
     color: #ccc;
   }
   .footer_wrap a {
     flex: 1;
     text-decoration: none;
     padding: 20px 0;
     line-height: 20px;
     background-color: #333;
     color: #ccc;
     border: 1px solid black;
   }
   .footer_wrap a:hover {
     background-color: #555;
   }
   .top {
     padding-top: 62px;
   }
   </style>
```

> 总结:
>
> 1. 下载路由模块, 编写对应规则注入到vue实例上, 使用router-view挂载点显示切换的路由
> 2. 一切都围绕着hash值变化为准,切换url上的hash值，开始匹配规则，对应组件展示到router-view位置



## vue声明式导航

### 2.1 基础用法

> 可用全局组件router-link来替代a标签

1. vue-router提供了一个全局组件 router-link
2. router-link实质上最终会渲染成a链接 to属性等价于提供 href属性**(to无需#)**
3. router-link提供了声明式导航高亮的功能(自带类名)



> 总结:
>
> 1. router-link是全局组成的组件，本质就是a标签
> 2. 当使用router-link时，必须传入to属性，指定路由路径值
> 3. 自带类名
>
> router-link没啥大用


### 2 .2跳转传参

> 目标: 在跳转路由时, 可以给路由对应的组件内传值

在router-link上的to属性传值, 语法格式如下

- /path?参数名=值
- /path/值 – 需要路由对象提前配置 path: “/path/参数名”

对应页面组件接收传递过来的值

- `$route.query.参数名`
- `$route.params.参数名`

> 总结:
>
> 1. ?key=value 用$route.query.key 取值
> 2. /值 提前在路由规则/path/:key 用$route.params.key 取值 (可读性很差，建议不要使用)

## 路由重定向和模式修改

### 3.1 重定向

场景：首次进入页面时，没有任何路由的hash值，页面元素会显示空白，如何解决？

> 目标: 匹配path后, 强制切换到目标path上

- 网页打开url默认hash值是/路径
- redirect是设置要重定向到哪个路由路径

```js
const routes = [
  {
    path: "/", // 默认hash值路径
    redirect: "/find" // 重定向到/find
    // 浏览器url中#后的路径被改变成/find-重新匹配数组规则
  }
]
```

> 总结: 强制重定向后, 还会重新来数组里匹配一次规则

**实际作用：**

1. 当某个路由在使用过程中废弃掉之后，将原来路由地址重定向到其他地址
2. 当满足某个条件时（如：登录信息过期），可以重定向到某个指定位置



### 3.2 路由 - 404页面

> 目标: 如果路由hash值, 没有和数组里规则匹配

默认给一个404页面

![image-20220611145433145](https://extraordinary-palmier-f8e65a.netlify.app/06-vue%E5%9F%BA%E7%A1%80/vue07/vue07/images/image-20220611145433145.png)

语法: 路由最后, path匹配*(任意路径) – 前面不匹配就命中最后这个, 显示对应组件页面

**步骤：**

1. 创建`NutFound`页面

```vue
   <template>
     <img src="../assets/404.png" alt="">
   </template>
   
   <script>
   export default {
   
   }
   </script>
   
   <style scoped>
       img{
           width: 100%;
       }
   </style>
```

2. 在main.js - 修改路由配置

```js
   import NotFound from '@/views/NotFound'
   
   const routes = [
     // ...省略了其他配置
     // 404在最后(规则是从前往后逐个比较path)
     {
       path: "*",
       component: NotFound
     }
   ]
```

> 总结: 如果路由未命中任何规则, 给出一个兜底的404页面

### 3.3 路由模式修改

> 目标: 修改路由在地址栏的模式
>
> [模式文档](https://router.vuejs.org/zh/api/#mode)

hash路由例如: http://localhost:8080/#/home

history路由例如: http://localhost:8080/home (以后上线需要服务器端支持, 否则找的是文件夹)

```js
const router = new VueRouter({
  routes,
  mode: "history" // 打包上线后需要后台支持, 模式是hash
})
```

> 唯一区别，是路由后缀有无#号



## 编程式导航（★★★★★）

> 用JS代码跳转!

### 4.1 基础用法

语法：

**path和name二选一！**

```js
this.$router.push({
    path: "路由路径", // 都去 router/index.js定义
    name: "路由名"
})
```

1. main.js - 路由数组里, 给路由起名字

   **代码规范：**一般情况下，path除去`/`以外的部分和name需要保持一致

```js
   {
       path: "/find",
       name: "Find",
       component: Find
   },
   {
       path: "/my",
       name: "My",
       component: My
   },
   {
       path: "/part",
       name: "Part",
       component: Part
   },
```

2. App.vue - 换成span 配合js的编程式导航跳转

```vue
   <template>
     <div>
       <div class="footer_wrap">
         <span @click="btn('/find', 'Find')">发现音乐</span>
         <span @click="btn('/my', 'My')">我的音乐</span>
         <span @click="btn('/part', 'Part')">朋友</span>
       </div>
       <div class="top">
         <router-view></router-view>
       </div>
     </div>
   </template>
   
   <script>
   // 目标: 编程式导航 - js方式跳转路由
   // 语法:
   // this.$router.push({path: "路由路径"})
   // this.$router.push({name: "路由名"})
   // 注意:
   // 虽然用name跳转, 但是url的hash值还是切换path路径值
   // 场景:
   // 方便修改: name路由名(在页面上看不见随便定义)
   // path可以在url的hash值看到(尽量符合组内规范)
   export default {
     methods: {
       btn(targetPath, targetName){
         // 方式1: path跳转
         this.$router.push({
           // path: targetPath,
           name: targetName
         })
       }
     }
   };
   </script>
```

### 4.2 跳转传参

> 目标: JS跳转路由, 传参

语法 query / params 任选 一个

```js
this.$router.push({
    path: "路由路径"
    name: "路由名",
    query: {
        "参数名": 值
    }
    params: {
        "参数名": 值
    }
})

// 方式1:
// params => $route.params.参数名

// 方式2:
// query => $route.query.参数名Copy to clipboardErrorCopied
```

**格外注意:** 使用path的话，只能和query一起使用，不可以使用params(会自动忽略)

App.vue

```vue
<template>
  <div>
    <div class="footer_wrap">
      <span @click="btn('/find', 'Find')">发现音乐</span>
      <span @click="btn('/my', 'My')">我的音乐</span>
      <span @click="oneBtn">朋友-小传</span>
      <span @click="twoBtn">朋友-小智</span>
    </div>
    <div class="top">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
// 目标: 编程式导航 - 跳转路由传参
// 方式1:
// params => $route.params.参数名
// 方式2:
// query => $route.query.参数名
// 重要: path会自动忽略params
// 推荐: name+query方式传参
// 注意: 如果当前url上"hash值和?参数"与你要跳转到的"hash值和?参数"一致, 爆出冗余导航的问题, 不会跳转路由
export default {
  methods: {
    btn(targetPath, targetName){
      // 方式1: path跳转
      this.$router.push({
        // path: targetPath,
        name: targetName
      })
    },
    oneBtn(){
      this.$router.push({
        name: 'Part',
        params: {
          username: '小传'
        }
      })
    },
    twoBtn(){
      this.$router.push({
        name: 'Part',
        query: {
          name: '小智'
        }
      })
    }
  }
};
</script>

```



## 路由嵌套

router-view嵌套架构图

### 5.1 创建所有组件

   ![image-20220611155109473](https://extraordinary-palmier-f8e65a.netlify.app/06-vue%E5%9F%BA%E7%A1%80/vue07/vue07/images/image-20220611155109473.png)

### 5.2 main.js– 继续配置2级路由

   一级路由path从/开始定义

   二级路由往后path直接写名字, 无需/开头

   嵌套路由在上级路由的children数组里编写路由信息对象

```js
   // 动态路由配置
   import Find from './views/Find.vue' // @是src的绝对地址
   import My from './views/My.vue'
   import Part from './views/Part.vue'
   import NotFound from './views/NotFound.vue'
   import Recommend from './views/Second/Recommend.vue'
   import Ranking from './views/Second/Ranking.vue'
   import SongList from './views/Second/SongList.vue'
   const routes = [
     {
       path: "/", // 默认hash值路径
       redirect: "/find" // 重定向到/find
       // 浏览器url中#后的路径被改变成/find-重新匹配规则
     },
     {
       path: "/find",
       name: "Find",
       component: Find,
       children: [
         {
           path: "recommend",
           component: Recommend
         },
         {
           path: "ranking",
           component: Ranking
         },
         {
           path: "songlist",
           component: SongList
         }
       ]
     }
   ]
```



##  全局前置守卫（★★★★★）

### 6.1 beforeEach

> 目的: 路由跳转之前, 先执行一次前置守卫函数, 判断是否可以正常跳转

**场景：**在跳转路由前, 判断用户登陆了才能去<我的音乐>页面, 未登录弹窗提示回到发现音乐页面

1. 在路由对象上使用固定方法beforeEach

```js
   // 目标: 路由守卫
   // 场景: 当你要对路由权限判断时
   // 语法: router.beforeEach((to, from, next)=>{//路由跳转"之前"先执行这里, 决定是否跳转})
   // 参数1 to: 要跳转到的路由 (路由对象信息)    目标
   // 参数2 from: 从哪里跳转的路由 (路由对象信息)  来源
   // 参数3 next: 函数体 - next()才会让路由正常的跳转切换, next(false)在原地停留, next("强制修改到另一个路由路径上")
   // 注意: 如果不调用next, 页面留在原地
   
   // 例子: 判断用户是否登录, 是否决定去"我的音乐"/my
   const isLogin = true; // 登录状态(未登录)
   router.beforeEach((to, from, next) => {
     if (to.path === "/my" && isLogin === false) {
       alert("请登录")
       next(false) // 阻止路由跳转
       // next('/part') // 跳转别的地方
     } else {
       next() // 正常放行
     }
   })Copy to clipboardErrorCopied
```

> 总结:
>
> 1. next()放行
> 2. next(false)留在原地不跳转路由
> 3. next(path路径)强制换成对应path路径跳转

### 6.2 扩展：afterEach

> 添加一个导航钩子，在每次导航后执行。返回一个删除注册钩子的函数。

语法：

```js
router.afterEach((to,from)=>{}) Copy to clipboardErrorCopied
```

**注意：**该钩子一般用于跳转到某个页面后，调用某个身份验证接口获取权限

### 6.3 组件内的独享路由钩子

1. `beforeRouteEnter` - 在进入到该组件之前，触发
2. `beforeRouteUpdate` - 仅是当前组件内部的路由发生变化（主路由地址没有改变）时，触发
3. `beforeRouteLeave` - 离开该组件之前，触发

```vue
<script>
    export default {
        beforeRouteEnter(to, from, next) {
            // 在渲染该组件的对应路由被 confirm 前调用
            // 不！能！获取组件实例 `this`
            // 因为当守卫执行前，组件实例还没被创建
            console.log('进find')
            next()
        },
        beforeRouteUpdate(to, from, next) {
            // 在当前路由改变，但是该组件被复用时调用
            // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
            // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
            // 可以访问组件实例 `this`
            console.log('被复用')
            next()
        },
        beforeRouteLeave(to, from, next) {
            // 导航离开该组件的对应路由时调用
            // 可以访问组件实例 `this`
            console.log('离开')
            next()
        }
    };
</script>
```



## 模块化后的路由文件  router/index.js

```js
import Vue from 'vue'
import Router from 'vue-router'

Vue.use(Router)
// 动态路由配置
import One from '../view/One.vue'
import Two from '../view/Two.vue'

const routes = [
    {
        path: '/one',
        component: One,
    },
    {
        path: '/two',
        component: Two,
    }
]

const router = new Router({
    routes,
    mode: 'hash'
})

export default router
```



### 最后在main.js 引入  和  把路由注入到实例中

```js
import router from './router/index.js'

new Vue({
  router,
  render: h => h(App),
}).$mount('#app')
```



