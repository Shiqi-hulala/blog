# Vue

day 02 

#### 1.for 更新检测

```html
  <div>
    <ul>
      <li v-for="(val, index) in arr" :key="index">
        {{ val }}
      </li>
    </ul>
    <button @click="revBtn">数组翻转</button>
    <button @click="sliceBtn">截取前4个</button>
    <button @click="updateBtn">点击改掉第一个元素的值</button>
  </div>
```

```javascript
data() {
    return {
      arr: [1, 2, 3, 4, 5, 6, 7],
    };
  },
  methods: {
    revBtn() {
      // 1.数组翻转 可以让 v-for更新
      this.arr.reverse();
    },
    sliceBtn() {
      // 2.数组slice方法 不会造成 v-for更新
      // slice不会改变原始 数组
      let re = this.arr.slice(0, 4);
      console.log(re);
    },
    updateBtn() {
      // 3.更新某个值的时候 v-for 是检测不到的
      this.arr[0] = 1717;
    },
    // vue将被侦听的数组变更方法进行包裹 所以它们也将会触发视图更新
    // 这些被包裹的方法包括：
    // push（）
    // pop（）
    // shift（）
    // unshift（）
    // splice（）
    // sort（）
    // reverse（）
  },
```

1.1 更新检测

```html
  <div>
    <ul>
      <li v-for="(val, ind) in arr" :key="ind">{{ val }}</li>
      <!-- v-for= "(值，索引) in xxx" -->
    </ul>
    <button @click="btn">下标1位置插入新来的</button>
  </div>
```

```javascript
 data() {
    return {
      arr: ["老大", "老二", "老三"],
    };
  },
  methods: {
    btn() {
      this.arr.splice(1, 0, "new");
    },
  },
```

1.2 key 的作用

```html
<div>
    <ul>
      <!-- <li v-for="val in arr"> -->
      <li v-for="obj in arr" :key="obj.id">
        {{ obj.name }}
        <input type="text" />
      </li>
    </ul>
    <button @click="btn">添加新元素</button>
 </div>
```

```javascript
data() {
    return {
      // arr: ["老大", "老二", "老三"],
      arr: [
        {
          name: "老大",
          id: 50,
        },
        {
          name: "老二",
          id: 30,
        },
        {
          name: "老三",
          id: 10,
        },
      ],
    };
  },
  methods: {
    btn() {
      // this.arr.splice(1, 0, "new");
      this.arr.splice(1, 0, {
        name: "new",
        id: 17,
      });
    },
  },
```

有key 和没有key 在效果上面的不同，第一种在输入框里面分别输入 123，新增加的元素输入框里面

2会存在里面，但是有key 后 新增元素里面会是空，2会跟随自己本身的那个输入框下移 （表面现象）

#### 2.动态class

语法：

:class="{类名 ：布尔值}" 

使用场景 ： vue变量 控制标签 是否应该有类名

```html
<p :class="{ red_str: bool }">动态class</p>
```

```javascript+css
 data() {
    return {
      bool: true,
    };
  },
    
<style scoped>
.red_str {
  color: red;
}
</style> 
```



#### 3.动态style

语法：

:style="{ css 属性名: 值}"

```html
  <p :style="{ backgroundColor: 'skyblue' }">动态改变style</p>
  <p :style="{ backgroundColor: colorStr }">动态改变style</p>
```

```javascript
  data() {
    return {
      colorStr: "pink",
    };
  },
```



#### 9.过滤器

过滤器使用    语法：{{值 | 过滤器名字}}   | 管道符

```html
 <div>
    <p>原来的样子 : {{ msg }}</p>
    <p>使用翻转过滤器：{{ msg | reverse }}</p>
    <p :title="pig | toUp">鼠标长时间停留</p>

    <!-- 过滤器 要在vue2 的版本才可以使用 
    vue2 项目的创建 
    1.npm install -g @vue/cli-init
    2.ue init webpack my-project
    3.会有一些选择 安装的插件
    4.cd 项目名
    5. npm run dev
    -->
  </div>

vue 里的data部分
data() {
    return {
      msg: "你最牛逼，陈十七",
      pig: "are you pig",
    };
  },
```

main.js 里面添加 全局过滤器

```js
// 方式1 全局 - 过滤器   /* global Vue */
// 任意的 .vue 文件内 "直接"使用 
// 语法 ： Vue.filter('过滤器名'，值 => 处理结果)
Vue.filter("reverse", val => val.split('').reverse().join(''))

// 多个过滤器 传参数
 Vue.filter("reverse", (val, s) => {
    return val.split('').reverse().join(s)
 })
```

局部 -- 过滤器

只能在当前 vue文件内使用

```javascript
/*
    语法：
    filters：{
      过滤器的名字 （val）{
        return 处理后的值
      }
    }
*/
  filters: {
    toUp(val) {
      return val.toUpperCase();
    },
  },
```

9.1 过滤器传参

```html
  <div>
    <p>原来的样子 : {{ msg }}</p>
    <!-- 给过滤器传参
    语法： vue变量  |  过滤器名（值）
     -->
    <p>使用翻转过滤器：{{ msg | reverse("---") }}</p>
    <!-- 多个过滤器使用
    语法： vue 变量 | 过滤器1 | 过滤器2
     -->
    <p :title="pig | toUp | reverse('--')">鼠标长时间停留</p>
  </div>
```

```javascript
data() {
    return {
      msg: "你最牛逼，陈十七",
      pig: "are you pig",
    };
  },

  filters: {
    toUp(val) {
      return val.toUpperCase();
    },
  },
```



#### 10.计算属性

  computed: {}

```html
 <div>
    <p>和为: {{ num }}</p>
 </div>
```

```javascript
data() {
    return {
      // num:17, error
      a: 10,
      b: 20,
    };
  },
 // 函数内使用 的变量 改变重新计算结果返回
 // 计算属性
 // 场景： 一个变量的值，需要用另外变量计算而得来
 /*
  语法：
  computed：{
    计算属性的名 (){
      return 值
    }
  }
 */
 // 注意：计算属性和data属性都是变量 - 不能重名
 computed: {
    num() {
      return this.a + this.b;
    },
  },
```

10.1 计算属性_缓存

```html
  <div>
    <p>{{ reverseMessage }}</p>
    <p>{{ reverseMessage }}</p>
    <p>{{ reverseMessage }}</p>
    <p>{{ getMessage() }}</p>
    <p>{{ getMessage() }}</p>
    <p>{{ getMessage() }}</p>
  </div>
```

```javascript
 data() {
    return {
      msg: "i can use vue",
    };
  },
  computed: {
    reverseMessage() {
      console.log('计算属性执行了')
      return this.msg.split("").reverse().join("");
    },
  },
  methods: {
    getMessage() {
      console.log('函数执行了')
      return this.msg.split("").reverse().join("");
    },
  },
```

  // 计算属性的优势
  // 带缓存
  // 计算属性对应函数执行后，会把return值缓存起来
  // 依赖项不变  多次调用都是从缓存取值
  // 依赖性值 - 变化  函数会 "自动" 重新执行 - 并缓存新的值

10.2 计算属性完整写法

```html
  <div>
    <span>姓名：</span>
    <input type="text" v-model="full" />
  </div>
```

```js
// 给计算属性赋值 -- 需要 setter
  computed: {
    // full(){
    //   return '陈十七'
    // }

    // 解决：
    /*
    完整语法：
    computed: {
    "计算属性名" (){}
    "计算属性名":{
        set(){

        },
        get(){
          return "值"
        }
    }
    */
// 完整写法
    full: {
      // 给full赋值触发set方法
      set(val) {
        console.log(val);
      },
      // 使用full的值 触发get方法
      get() {
        return "陈十七";
      },
    },
  },
```

11.侦听器

 watch:{}

```html
<template>
  <div>
    <input type="text" v-model="user.name" />
    <input type="text" v-model="user.age" />
  </div>
</template>
```

```javascript
export default {
  data() {
    return {
      name:""
    }
  },
  // 目标：侦听到name值的改变
  /**
   * 语法
   * watch：{
   *  变量名（newVal, oldVal）
   *  变量名对应值改变这里自动触发
   * }
   */
  watch:{
    // newVal ： 当前最新值
    // oldVal ：上一时刻的值
    name(newVal, oldVal){
      console.log(newVal, oldVal)
    }
  }
```

11.1深度侦听

```html
<template>
  <div>
    <input type="text" v-model="user.name" />
    <input type="text" v-model="user.age" />
  </div>
</template>
```

```js
export default {
  data() {
    return {
      user: {
        name: "",
        age: 0,
      },
    };
  },
  // 目标侦听一个对象
  /**
   * watch ：{
   *  变量名（newVal, oldVal{
   *  变量名对应值改变这里自动触发
   *  },
   *
   * 变量名：{
   * handler（newVal, oldVal）{
   *  },
   *  deep:true
   *  深度侦听（对象里面层的值改变）
   *  immediate: true 立即侦听
   *  网页打开handler 执行一下
   * }
   * }
   */
  watch: {
    user: {
      handler(newVal, oldVal) {
        // user里的对象
        console.log(newVal, oldVal);
        // console.log(newVal.name, oldVal.name);
      },
      deep: true,
      immediate: true,
    },
  },
};
```

