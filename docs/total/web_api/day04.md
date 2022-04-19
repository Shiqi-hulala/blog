#### 1.  常用的鼠标事件

​	*1.禁用右键菜单*    contextmenu

```javascript
document.addEventListener('contextmenu', function (e) {
            // 阻止默认行为
            e.preventDefault();
            console.log('禁止右键点击!')
        })
```

2.*禁止选中文字*   *selectstart*

```javascript
  document.addEventListener('selectstart', function (e) {
            e.preventDefault();
            console.log('禁止选中文字!')
        })
```

3.单独某个元素 阻止。。。

```javascript
  var span = document.querySelector('span')
        span.addEventListener('selectstart', function (e) {
            e.preventDefault()
        })
```



4.*client 鼠标在浏览器窗口的可视区的 x y坐标*

```javascript
 //不管页面有没有滚动条 总是相对页面框内
document.addEventListener('click', function (e) {
            console.log(e.clientX)
            console.log(e.clientY)
            }
```



5.*page 鼠标在页面文档的x y坐标* 

```javascript
 // 重点掌握
//可以得到页面滚动后的距离，*****
            console.log(e.pageX)
            console.log(e.pageY)
```

6.*screen 鼠标在电脑屏幕上的 x y 坐标*

```javascript
			console.log(e.screenX)
            console.log(e.screenY)
```



#### 2.  常用的键盘事件

​	**keyup**

```javascript
1. keyup : 键盘抬起时候触发
 document.addEventListener('keyup', function (e) {
            // console.log(e.type)// 表示事件类型
            console.log('keyup')
        })
```

​	**keydown**

```javascript
 2.keydown  键盘按下时候触发 那个键的值没有输入前就触发
 //  能识别功能键  ctrl shift 上下左右箭头
document.addEventListener('keydown', function (e) {
            console.log('keydown')
        })
```

​	**keypress**

```javascript
3.  keypress
document.addEventListener('keypress', function (e) {
            console.log('keypress')
        })
```

总结：

 keydown 和  keypress 一直按住 会一直触发

 keydown 和 keypress 在咱们输入键值就触发了

执行顺序： keydown  -->  keypress -->  keyup

```javascript
//判断键盘按的哪一个键 
document.addEventListener('keypress', function (e) {
            console.log('press:' + e.keyCode)
            console.log(String.fromCharCode(e.charCode));
        })
```



 #### 3. BOM顶级对象 

   浏览器对象模型（BOM） ----  与浏览器交互的方法和接口

BOM 比 DOM 还大

#### 4.  定时器 setTimeout

**setTimeout（callback， wait）**

时间单位是毫秒	 1000ms = 1s

​	

```javascript
方式一:
 setTimeout(function () {
            console.log('show time')
        }, 1000)
方式二:
	// fn 是回调函数  就是延时结束后执行
        var fn = function () {
            console.log('函数体')
        }
   function callback() { //回调函数
            console.log('bang bang bang')
        }
    //一般定义一个变量来区分多个定时器
     var timer = setTimeout(callback, 3000)
     var timer1 = setTimeout(callback, 5000)
     var timer2 = setTimeout(fn, 5000)
```

​	**clearTimeout**

```javascript
      var btn = document.querySelector('button')
        var fn = function () {
            console.log('show time')
        }
        var timer = setTimeout(fn, 3000)
        // 清楚定时器  在延时前  清楚  回调函数就不会执行
        btn.addEventListener('click', function () {
            clearTimeout(timer)
        })

```

​	**setInterval  （callback， wait）**

​	callback 函数体会被重复执行 每隔 wait 设置的时间执行一次

```javascript
  setInterval(function () {
            console.log('胡丽是猪');
        }, 1000);
```

​	**clearInterval**

```html
 <button class="begin">开启定时器</button>
 <button class="stop">停止定时器</button>
```

```javascript
var begin = document.querySelector('.begin');
var stop = document.querySelector('.stop');

...重点一
var timer = null; // 全局变量  null是一个空对象
        // 让定时器的标记作为全局变量

begin.addEventListener('click', function() {
    timer = setInterval(function() {
        console.log('ni hao ma');

    }, 1000);
})
、、、重点二：设置清除定时器（类似clearTimeout）
stop.addEventListener('click', function() {
    clearInterval(timer);
})
```



#### 5.  this 指向问题

1. 全局作用域或者普通函数中this指向全局对象window（ 注意定时器里面的this指向window）
	
```javascript
    1.----- console.log(this);
    2.----- function fn() {
    console.log(this);
    
    }
    window.fn();
    3.----- window.setTimeout(function() {
        console.log(this);
    }, 1000);
```

2. 方法调用中谁调用this指向谁

  ```javascript
   ① ：var o = {
          sayHi: function() {
          console.log(this); // this指向的是 o 这个对象
              }
          }
   o.sayHi();
   ② ：var btn = document.querySelector('button');
    	btn.addEventListener('click', function() {
      console.log(this); // this指向的是btn这个按钮对象
  	})
  ```

3. 构造函数中this指向构造函数的实例

   ```javascript
   function Fun() {
         console.log(this); // this 指向的是fun 实例对象
       }
   var fun = new Fun();
   ```

   

#### 6. location常见的方法

   