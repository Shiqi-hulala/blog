- ## 获取ID 元素

  - document.getElementById

    ```
    <div id="time">2019-9-9</div>
    ```

    ```javascript
    var timer = document.getElementById('time');
    ```

  

- ## 使用标签获取元素

  - document.getElementsByTagName

    ```html
    <ol id="ol">
        <li>生僻字</li>
        <li>生僻字</li>
        <li>生僻字</li>
        <li>生僻字</li>
    </ol>
    ```

    ```javascript
    var lis = document.getElementsByTagName('li');
    console.log(lis);
    ```

    

- ## H 5  新增获取元素的方式

  - ##### Class （*通过类名*）

    - document .getElementsByClassName

      ```html
      <div class="box">盒子1</div>
      ```

      ```javascript
      var box = document.getElementsByClassName('box')
      console.log(box)  // 返回值也是 伪数组
      ```

      

  - ##### *通过选择器  获取的是第一个*

    - document.querySelector

      ```html
          <div class="box">盒子1</div>
          <div class="box">盒子2</div>
          <div id="nav">
              <ul>
                  <li>首页</li>
                  <li>产品</li>
              </ul>
          </div>
          <p class="item">item</p>
          <p>item</p>
          <p>item</p>
      ```

      ```javascript
      var box = document.querySelector('.box')
      
      var nav = document.querySelector('#nav')
      
      var nav = document.querySelector('p')
      
      ```

      

    - ##### document.querySelectorAll

      ```javascript
      var allBox = document.querySelectorAll('.box')
      ```

      

- ## 事件三要素

  - #### 获取事件源  

    - ```java
      var btn = document.querySelector('button')
      ```

      

  - #### 事件类型   *绑定事件*

    - ```javascript
      //绑定的事件有很多 onclick 是鼠标点击事件
      btn.onclick = function () {
          // 3.事件处理程序
          input.value = '修改'
          console.log(this)
      
          // 禁用按钮
          this.disabled = true
      }
      ```

      

  - #### 处理程序

    - ```javascript
      //就是绑定的事件需要做的事情 需要如何操作
      // 3.事件处理程序
      input.value = '修改'
      console.log(this)
      ```

      

- ## 事件执行流程

  - [ ] 获取事件源
  - [ ] 注册事件 绑定事件
  - [ ] 添加事件处理程序 

- ## 鼠标事件

  - onclick  鼠标点击左键触发
  - onmouseover  鼠标经过
  - onmouseout  鼠标离开
  - onfocus  获得鼠标焦点
  - onblur  失去鼠标焦点
  - onmousemove  鼠标移动
  - onmouseup  鼠标弹起
  - onmousedown  鼠标按下

- ## 改变元素内容
  
  - innerHTML （推荐）
  - innerText
  
- innerHTML 和 innerText 区别

  - 获取内容时的区别：

  ​	innerText会去除空格和换行，而innerHTML会保留空格和换行	

  - 设置内容时的区别：

  ​	innerText不会识别html，而innerHTML会识别

- ## 获取特殊元素

  - *获取body 元素*

    - ```javascript
      var bodyEle = document.body;
      console.log(bodyEle);
      ```

      

  - *获取html 元素*

    - ```javascript
      var htmlEle = document.documentElement;
      console.log(htmlEle);
      ```

- ## 常用元素的属性操作

  - 1. innerHTML  innerText  改变元素内容
    2. src   href
    3. id  alt  title

  - **获取属性的值**

    > 元素对象.属性名

    **设置属性的值**

    > 元素对象.属性名 = 值





- ## 表单元素的属性操作

  - type, value , checked, selected, disabled

  - **获取属性的值**

    > 元素对象.属性名

    **设置属性的值**

    > 元素对象.属性名 = 值
    >
    > 表单元素中有一些属性如：disabled、checked、selected，元素对象的这些属性的值是布尔型。



- ## 样式属性操作

  - 常用方式

    - element.style    很内样式造作
    - element.className  类名样式操作

    方式1：通过操作style属性

    > 元素对象的style属性也是一个对象！
    >
    > 元素对象.style.样式属性 = 值;

    方式2：通过操作className属性

    > 元素对象.className = 值;
    >
    > 因为class是关键字，所有使用className。





- api ：application p...  接口  一种工具    函数
- web api ： 浏览器提供给我们的操作浏览器 功能 和操作页面元素（DOM）的 api 
- DOM :  document ...
- DOMs  tree : 它是一个层级结构