# vue组件

## 一：vue组件通信

### 1.1  父传子 - props(★★★★★)

> 目的: 从外面给组件内传值, 先学会语法

第一步 : 子组件里面设置 props 

```js
export default {
// 设置 props 
  props: ['title','info']
};
```

第二步 : 子组件 的 template 里面

```html
<template>
  <div>
    <!-- 2. 使用 props 中的变量  -->
    <h3>标题: {{ title }}</h3>
    <p>描述: {{ info }}</p>
  </div>
</template>
```

第三步 ： 父组件 中先引入 子组件

```js
import 自定义子组件名 from "相对路径"; 
```

第四步 ：父组件 里面注册 子组件 

```js
  components: {
   自定义子组件名
  },
```

第五步 :  挂载子组件 

```html
<自定义子组件 title="山城" info="山城啤酒，知心朋友" />
```

> 总结: props的值不能重新赋值, 对象引用关系属性值改变, 互相影响

> 思考? 那子组件中如何去修改父组件传递过来的值呢？
>
> 有没有一种可能，通过告诉父组件让父组件自己去修改传过来的值呢？
> 

![image-20220620203113869](.\img\image-20220620203113869.png)

### 1.2 子传父 - $emit (★★★★★)

> 目标： 从子组件把值传出来给外面使用

需求: 实现砍价功能, 子组件点击实现随机砍价-1功能

![image-20220620202341043](.\img\image-20220620202341043.png)

### 1.3 跨组件传参 - EventBus

略略略

### 1.4  props 进阶用法 

**说明：**props也可以作为一个对象，并且可以指定数据类型，必要性，默认值

```js
props: {
    str: {
      type: String, // 传参类型
      require: true, // 是否必传（一般也不写，了解）
      default: "默认值", // 默认值
    },
    num: {
      type: Number,
      default: 0,
    },
    arr: {
      type: Array,
      default: () => [],
    },
    obj: {
      type: Object,
      //   如果箭头函数返回的是一个对象 就用小括号包裹这个对象 以免让js代码认为大括号是方法的边界
      default: () => ({}),
    },
  },
```