# vue

##### day01

如何去使用vue/cli 搭建一个项目

1.yarn global add @vue/cli --- 得到vue 命令

2.vue create 脚手架项目名字 --- 得到一套文件夹 + 文件的标准工程代码

3.yarn serve



开始的时候 可以把不重要的文件删除掉  ： assets 里面的logo图片

components 里面的HelloWord.vue  文件   和  App.vue 里面的内容可以清除掉



然后在App.vue 里面   输入  '<'  会有模板 直接tab

注意：  在template 标签 里面的所有内容  只能放在一个父盒子里面 

通常我们会先  用一个div 包裹所有的内容

```vue
<template>
  <div>
    内容部分
  </div>
</template>
```



#### 1.插值表达式

​	第一步： 变量在data函数 return 的对象上 

```javascript
<script>
export default {
  // 1.变量在data函数 return 的对象上
  data() {
    return {
      msg: "hi,十七",
      obj: {
        name: "胡啦啦",
        age: 17,    
        sayHi: function () {
          console.log("hi~");
        },
      },
    };
  },
};
</script>
```

​	

第二步 ：把值赋给标签

```vue
<template>
  <div>
    <!-- 2.把值赋给标签 -->
    <h1>{{ msg }}</h1>
    <h2>{{ obj.name }}</h2>
    <h3>{{ obj.sayHi() }}</h3>
    <h4>{{ obj.age >= 18 ? "成年" : "未成年" }}</h4>
  </div>
</template>
```



#### 2.动态属性  v-bind 

第一步： 准备变量

```javascript
data() {
    return {
      url: "https://www.superbed.cn/timeline",
      imgUrl: "https://pic.imgdb.cn/item/62538be0239250f7c5045e8f.jpg",
    };
  },
```



第二步：变量引入          使用

```vue
<template>
  <div>
    <a v-bind:href="url"></a>
    <a :href="url">图床</a>
    <img :src="imgUrl" alt="" width="200px"/>
  </div>
</template>
```



#### 3.事件绑定  v-bind 

第一步: 绑定事件

语法： v-on： 事件名=” 少量代码“

```html
<button v-on:click="count += 1">+1</button>
```

语法： v-on：事件名=“methods里面的函数名”

```html
<button v-on:click="addFn">+1</button>
```

```vue
 methods: {
    addFn() {
      // this指向的是export default 的{}
      // data函数会把对象挂载到当前组件对象上
      this.count++;
    },
   },
```

语法： v-on:  事件名=“methods里面的函数名（值）”

```html
<button @click="addCountFn(5)">+5</button>
```

```vue
 addCountFn(num) {
      this.count += num;
    },
```



#### 4.事件对象

```js
methods: {
    one(e) {
    //  1. 事件触发 无传值 可以直接获取事件对象
      e.preventDefault();
    },
    // 2.事件触发 传值 需要手动传入$event
    two(num, e){
      e.preventDefault()
    }
  },
```

```html
 <div>
    <a
      @click="one"
      href="https://docsify.js.org/#/quickstart?id=writing-content"
    >docsify</a>
    <hr />
    <a 
      @click="two(10 , $event)" 													  href="https://www.webpackjs.com/concepts/#%E5%85%A5%E5%8F%A3-entry-		     ">webpack</a>
 </div>
```



#### 4.1.事件修饰符

.stop 阻止事件冒泡

```javascript
<p @click.stop="oneFn">.stop 阻止事件冒泡</p>
```

.prevent  阻止默认行为

由于点击后没有其他意思 所以后面可省略  (.prevent.stop 都阻止) 

```javascript
<a @click.prevent.stop href="https://cli.vuejs.org/zh/guide/creating-a-project.html#vue-create">去死</a> 
```

.once   程序执行期间 只触发一次事件处理函数

```javascript
 <p @click.once="twoFn">点击观察事件处理函数执行几次</p>
```



#### 4.2.键盘修饰符

绑定键盘事件  enter - - - 回车

```javascript
  <input type="text" @keydown.enter="enterFn" />
        
  methods: {
    enterFn() {
      console.log("按下回车键！");
    },
  },
```

.esc 修饰符  --- 取消键 esc

```javascript
 <input type="text" @keydown.esc="escFn" />
 methods: {
    escFn() {
      console.log("按下esc键~!");
    },
  },
```



#### 5.v-model 基本使用

v-model  双向数据绑定

 一个是：表单的value属性  另一个：vue 变量 

```javascript
<div>
    <span>用户名：</span>
    <input type="text" v-model="username" />
    <span>密码：</span>
    <input type="=password" v-model="password" />
</div>
```

```vue
 data() {
    return {
      username: "",
      password: "",
    };
  },
```



#### 5.1 v-model 表单双向数据绑定

下拉菜单：**下拉菜单要绑定在select上**

```html
    <div>
      <span>来自于:</span>
      <select v-model="from">
        <option value="长沙市">长沙</option>
        <option value="成都市">成都</option>
        <option value="重庆市">重庆</option>
      </select>
    </div>
```



复选框   遇到复选框 v-model 变量值

**非数组 -- 关联的是复选框的checked属性**

**数组 -- 关联的是复选框的value属性** 

```html
<div>
      <span>爱好:</span>
      <input type="checkbox" value="抽烟" v-model="hobby" />抽烟
      <input type="checkbox" value="喝酒" v-model="hobby" />喝酒
      <input type="checkbox" value="烫头" v-model="hobby" />烫头
</div>
```

单选框   设置name相同的单选钮为同一组 **单选按钮**

```javascript
<div>
      <span>性别：</span>
      <input type="radio" value="男" name="sex" v-model="gender" />男
      <input type="radio" value="女" name="sex" v-model="gender" />女
</div>
```

文本域

```javascript
 <div>
      <span>自我介绍</span>
      <textarea v-model="intro"></textarea>
</div>
```

vue代码

```vue
data() {
    return {
      from: "成都",
      // hoppy: "",  error!
      hobby: [],
      gender: "男",
      intro: "Please introduce yourself",
    };
  },
```



#### 5.2表单修饰符

**.number** 修饰符 把值parseFloat 转数值   再赋值给 v-model 对应的变量

```html
<div>
    <span>年龄</span>
    <input type="number" v-model.number="age" />
</div>
```

**.trim** 修饰  去除 收尾两边空格

```html
<div>
      <span>人生格言</span>
      <input type="text" v-model.trim="motto" />
</div>
```

**.lazy**    修饰符 失去焦点 内容改变时（onchange事件）把内容同步给 v-model的变量

```html
   <div>
      <span>个人简历</span>
      <textarea v-model.lazy="intro"></textarea>
    </div>
```



#### **6.vue指令  v-text 和 v-html 区别**

```html
  <p v-text="str"></p>
  <p v-html="str">{{ 10 + 20 }}</p>
  
  str: "<span>我是一个span</span>",
```

注意：v-text 或者 v-html 会覆盖插值表达式



#### **7.vue指令 v-if 和 v-show 的使用**

```html
    <h1 v-show="isShow">我是h1</h1>
    <h2 v-if="isOk">我是h2</h2>

	isShow: true
      isOk: true
```

原理：

  v-show 用的是 diaplay：none 隐藏 // （频繁切换使用）

  v-if 直接从DOM树上移除  // 移除

##### 7.1 v-if 和 v-else 使用

```html
<p v-if="age > 21">我成年了</p>
<p v-else>你还多吃点</p>

 变量 age: 20
```

