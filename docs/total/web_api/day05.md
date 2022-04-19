1. this指向	

   **一定是在调用执行的时候才能确实指向  在定义时候不能确实**

   1. 全局作用域中  或  普通函数调用
   2. 方法调用中  谁调用this指向谁
   3. 事件注册的时候  this 指向的是被绑定的元素
   4. 构造函数 中的this   ---->  

   

2. offset  

   1. offset   ：动态获取盒子的位置

      ```
      <div class="shiqi">
              <div class="father">
                  <div class="son"></div>
              </div>
          </div>
      ```

      ```javascript
      var divFa = document.querySelector('.father')
      var divSon = document.querySelector('.son')
       1. offsetTop offsetLeft  获取元素距离  带有定位父元素的距离
       	console.log(divFa.offsetTop)  
      	console.log(divFa.offsetLeft)  
      	注意：如果没有定位的父元素  以body为参照 返回值不带单位
      	它以带有定位的元素为准  除了static   父元素有定位后就是距离父元素的位置
      	
      2. offsetWidth offsetHeight
      可以得到元素的大小  (高度宽度)  它包含 width padding border
      console.log(divFa.offsetHeight)
      console.log(divFa.offsetWidth)
      
      3. offsetParent 获取带有定位的父元素
      console.log(divFa.offsetParent)
      console.log(divSon.offsetParent)
      
      获取的是最近的一级的父元素 和定位无关
      console.log(divSon.parentNode)
      ```

      offset和style 区别

      style

      1.可以获取到任意样式的类型的值

      2.获取到的没有单位，number

      3.包含padding border width

      4.只能读属性 只能获取 不能赋

      offset

      1.只能获取到行内样式

      2.它获取到的是带单位的字符串

      3.只能获取 width 不包含 padding border

      4.本质区别: style 可以读写  不仅能获得还可以设置  本质区别

      

      **本质区别： 一个可以获取修改，一个只能获取，不能修改**

      

3. client

   1. client 宽度 和我们offsetWidth 最大的区别就是 不包含边框

   2. ```
      
      ```

      

4. 立即执行函数

   1. 

5. scroll

6. mouseenter 和 mouseover

   1. mouseover  和  mouseout       存在事件冒泡

   2. mouseenter      mouseleave    没有事件冒泡

      ```javascript
      <div class="father">
           <div class="son"></div>
      </div>
      var father = document.querySelector('.father');
      var son = document.querySelector('.son');
              father.addEventListener('mouseenter', function () {
                  console.log(1);
      
              })
              father.addEventListener('mouseover', function () {
                  console.log(2);
      
              })
      ```

      

7. 动画原理

8. 