####  1.删除节点

   1. node.removeChild() 方法从 node节点中删除一个子节点，返回删除的节点。

   2. ```java
      <button>删除</button>
          <ul>
              <li>熊大</li>
              <li>熊二</li>
              <li>光头强</li>
          </ul>
          <script>
              // 1.获取元素
              var ul = document.querySelector('ul');
              var btn = document.querySelector('button');
              // 2. 删除元素  node.removeChild(child)
              // ul.removeChild(ul.children[0]);
              // 3. 点击按钮依次删除里面的孩子
              btn.onclick = function() {
            	 // 不能一直点击删除  里面没有可删除的节点   
                  if (ul.children.length == 0) {
               // 当ul的子节点没有了 可以禁用按钮
                      this.disabled = true;
                  } else {
                      ul.removeChild(ul.children[0]);
                  }
              }
          </script>
      ```

      

#### 2.节点克隆

   1. cloneNode(false) 或者 cloneNode() 表示浅拷贝

      只复制标签 不复制内容

      

       cloneNode(true)  表示深拷贝

       复制标签和里面的内容

   2.  

      ```html
      <ul>
      
      ​    <li>1111</li>
      
      ​    <li>2</li>
      
      ​    <li>3</li>
      
      </ul>
      ```

      

   3. ```javascript
          var ul = document.querySelector('ul')
      ​    li1 = ul.children[0]
      
      ​    *// 克隆节点*
      ​    var cloneLi = ul.children[0].cloneNode(true)
      ​    console.log(cloneLi)
      
      ​    *// 在 ul.children[0] ==> 第一个li 的前面添加 cloneLi* 
      ​    *// ul.insertBefore(cloneLi, ul.children[0])*
      ​    ul.insertBefore(cloneLi, ul.children[ul.children.length - 1])
      
      ​    console.log(ul.children[0])
      ​    console.log(ul.children[ul.children.length - 1])
      // 1.第一个子元素节点 ： parentNode.children [0]*
      // 2.最后一个子元素节点：parentNode.children [parentNode.children.length - 1]
      ```

      #### 3. 三种创建元素的方式

         1.   
         
            ```html
            <button>点击</button>
            <p>abc</p>
            <div class="inner">inner</div>
            <div class="create">create</div>
            ```
         
              
         
         2. 
         
            1. document.write()  
            2. innerHTML
            3. document.createElement()
            
            ```javascript
             // 1. document.write() 创建元素  如果页面文档流加载完毕，再调用这句话会导致页面重绘
            ​    var btn = document.querySelector('button')
            ​    btn.onclick = function () {
            ​      document.write('<p>你是猪吗！</p>')
            ​    }
            
            ​    *// 2. innerHTML 创建元素*
            ​    var inner = document.querySelector('.inner')
            ​    	inner.onclick = function () {
            ​    	inner.innerHTML = '<a href="#">del</a>'
            ​    }
            
            ​    *// 3.document.createElement() 创建元素*
            		略。。
            ```
      
         3.innerHTML 拼接效率
      
         ```javascript
         //方式一   垃圾 影响性能
         console.time()
                 var str = '';
                 for (var i = 0; i < 1000; i++) {
                     document.body.innerHTML += '<div style="width:100px; height:2px; border:1px solid blue;"></div>';
                 }
         console.timeEnd()
         
         //方式二   推荐
         console.time()
                 var array = [];
                 for (var i = 0; i < 1000; i++) {
                 array.push('<div style="width:100px; height:2px; border:1px solid blue;"></div>');
                 }
                 // 使用 innerHTML 的形式 数组的形式效率更高
                 // join 数组转为字符串
                 document.body.innerHTML = array.join('');
         console.timeEnd()
         
         //方式三 
             function fn() {
                 var d1 = +new Date();
                 for (var i = 0; i < 1000; i++) {
                     var div = document.createElement('div');
                     div.style.width = '100px';
                     div.style.height = '2px';
                     div.style.border = '1px solid red';
                     document.body.appendChild(div);
                 }
                 var d2 = +new Date();
                 console.log(d2 - d1);
             }
             fn();
         ```
      

#### 4. 注册事件的两种方式

   1. ```html
      <button>传统注册事件</button>
      <button>方法监听注册事件</button>
      <button>ie9 attachEvent</button>
      ```

      ```javascript
      //第一种传统方式注册 
       	var btns = document.querySelectorAll('button')
              btns[0].onclick = function () {
                  console.log('传统第一次注册')
              }
              btns[0].onclick = function () {
                  console.log('传统第二次注册')
              }
      //第二次注册的会覆盖掉第一次注册的
      ```
   ```javascript
			//使用事件监听的方式注册  以后特别常使用的
              btns[1].addEventListener('click', function () {
                  console.log('我是addEventListener注册的第一次')
              })
      
              btns[1].addEventListener('click', function () {
                  console.log('我是addEventListener注册的第二次')
              })
      
              // 为什么表达式的写法，不能放在监听后面?
              var fn = function () {
                  console.log('i am listener')
              }
      
              function demo() {
                  console.log('test')
              }
      
              btns[1].addEventListener('click', demo)
              btns[1].addEventListener('click', fn)
      // 1.我们绑定的事件类型  如果监听的方式写   那么不需要 on 是字符串
      // 2.同一个元素，同一个事件，我们可以多次添加多个事件监听
      // 3.他们会按照我们添加注册的顺序。依次执行
   ```

#### 5.  删除（解绑）事件

   1. ```html
      <button>传统 解绑事件</button>
      <button>监听事件 解绑事件</button>
      ```

      ```javascript
      // 删除事件   传统方法
      var btns = document.querySelectorAll('button')
      btns[0].onclick = function () {
          console.log('极客')
          btns[0].onclick = null
      }
      
      // 监听事件 解绑     
      // 需要在事件 处理程序里面进行解绑
      var fn = function () {
          console.log('辛迪加')
          btns[1].removeEventListener('click', fn)
      }
      btns[1].addEventListener('click', fn)
      ```

      

#### 6.  DOM的事件流 三个阶段

   1. 事件捕获  
   2. 目标阶段
   3. 事件冒泡

#### 7.  事件对象

   1. ```javascript
      div.addEventListener('click', function(e) {
      console.log(e);
      ```

      e.target 返回的是触发事件的对象（元素）

      this 返回的是绑定事件的对象（元素）

      /*ul li 的关系 当ul绑定事件 this就会指向ul  但是e.target 很可能是触发 ul里面的 li 所以...*/

#### 8.  事件对象阻止默认行为  e.preventDefault()

   1. ```javascript
      // 2. 阻止默认行为（事件） 让链接不跳转 或者让提交按钮不提交
              var a = document.querySelector('a');
              a.addEventListener('click', function(e) {
                      e.preventDefault(); //  dom 标准写法
                  })
      // 3. 传统的注册方式
              a.onclick = function(e) {
      // 我们可以利用return false 也能阻止默认行为  return 后面的代码不执行了， 而且只限于传统的注册方式
                  return false;
                  alert(11);
              }
      ```

      

#### 9.  阻止事件冒泡    stopPropagation() 

   1. ```javascript
       // 阻止冒泡  dom 推荐的标准 stopPropagation() 
              var son = document.querySelector('.son');
              son.addEventListener('click', function(e) {
                  alert('son');
                  e.stopPropagation(); // stop 停止  Propagation 传播    
              }, false);
      ```

      //阻止默认行为，阻止事件冒泡都是  event 的属性方法

#### 10.  事件委托

    1. **事件委托的核心原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点**

```html
  <ul>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
    </ul>
```

```javascript
		var ul = document.querySelector('ul');
        ul.addEventListener('click', function (e) {
            // alert('知否知否，点我应有弹框在手！');
            // e.target 这个可以得到我们点击的对象
            e.target.style.backgroundColor = 'pink';
        })
        // 1.只需要操作一次dom 提高程序性能 只需要一次绑定
        // 2.动态创建的子元素 也拥有咱们注册的事件

        // 对比传统
        var lis = document.querySelectorAll('li')
        for (let i = 0; i < lis.length; i++) {
            lis[i].onclick = function () {
                console.log('for 循环绑定！')
            }
        }

        var li = document.createElement('li')
        ul.appendChild(li)
```

