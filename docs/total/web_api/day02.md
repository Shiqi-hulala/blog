## 1.排他思想	

**按钮案例**

```html
<button>按钮1</button>
<button>按钮2</button>
<button>按钮3</button>
<button>按钮4</button>
<button>按钮5</button>
```

```javascript
		// 获取所有按钮
        var btns = document.querySelectorAll('button')
        console.log(btns) // 伪 []
        // 遍历绑定事件
        for (let i = 0; i < btns.length; i++) {
            btns[i].onclick = function () {
                // Kill the others and keep yourself
                // 清空全部按钮的背景色
                // kill other
                for (let j = 0; j < btns.length; j++) {
                    btns[j].style.backgroundColor = '';
                    // console.log(this)
                    // this.style.backgroundColor = '';
                }
                // keep youself
                // 然后给当前点击的按钮 添加背景色
                console.log(this)
                this.style.backgroundColor = 'pink';
            }
        }
        
        
        // jQuery
        $(function () {
            // 1. 隐式迭代  给所有按钮绑定了点击事件
            $('button').click(function () {
                // 2. 当前元素变化背景颜色
                $(this).css('background', 'pink');
                // 3.其余的兄的去掉背景颜色  隐式迭代
                // $(this).siblings().css('background', 'none');
                $(this).siblings('button').css('background', '');
            });
        })
```



## 2.自定义属性操作

1. ##### 获取属性值

   ```javascript
   div.className = 'xxxx'
   ```

   

2. ##### 设置自定义属性

   ```javascript
   div.setAttribute('orange', '颜色')
   ```

   

3. #####  移除属性

   ```javascript
    div.removeAttribute('index')
   ```


4. #####  H 5 自定义属性

    1. 设置H 5自定义属性
      
    
    H 5 规定自定义属性 data- 开头作为属性名并赋值
    
    ```javascript
    <div data-index="1"></div>
    或者使用js设置
    elemnet.setAttribute('data-index',2)
    ```

   2.获取H 5自定义属性

```javascript
1.兼容性获取  element.getAttribute('data-index')
2.H 5 新增 element.dataset.index 或者 element.dataset['index'] ie 11 才开始支持
<div getTime="20" data-index="2" data-list-name="andy"></div>
    <script>
        var div = document.querySelector('div');
        // console.log(div.getTime);
        console.log(div.getAttribute('getTime'));
        div.setAttribute('data-time', 20);
        console.log(div.getAttribute('data-index'));
        console.log(div.getAttribute('data-list-name'));
        // h5新增的获取自定义属性的方法 它只能获取data-开头的
        // dataset 是一个集合里面存放了所有以data开头的自定义属性
        console.log(div.dataset);
        console.log(div.dataset.index);
        console.log(div.dataset['index']);
        // 如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法
        console.log(div.dataset.listName);
        console.log(div.dataset['listName']);
    </script>
```



## 3.节点操作

元素节点  nodeType  为  1

属性节点  nodeType  为  2

文本节点  nodeType  为  3 （文本节点包括 文字 空格 换行 等）

我们实际开发中，节点操作主要是元素节点



>父级节点  ： node.parentNode
>
>parentNode 属性可返回某个节点的父节点，注意是最近的父节点
>
doc>如果指定的节点没有父节点则 返回 null

>```html
><div class="demo">
>        <div class="box">
>            <span class="erweima">×</span>
>        </div>
> </div>
>```

>```javascript
>// 1. 父节点 parentNode
>    	var erweima = document.querySelector('.erweima');
>        // var box = document.querySelector('.box');
>        // 得到的是离元素最近的父级节点(亲爸爸) 如果找不到父节点就返回为 null
>        console.log(erweima.parentNode);
>```



子节点  parentNode.childNode (标准)

>parentNode.childNode  返回包含指定节点的子节点的集合，该集合即为及时更新的集合
>
>注意：：返回值里面包含所有的子节点，包含 元素节点 文本节点
>
>如果只想要获得里面的元素节点，则需要专门处理，所以一般不建议使用childNodes
>
>
>
>子元素节点 parentNode.children (非标准)
>
>parentNode.children 是一个只读属性，返回所有的子元素节点，它返回子元素节点，其余节点
>
>不返回

>虽然是非标准。但是得到各个浏览器的支持，可以放心用

>```html
>   <ul>
>        <li>我是li</li>
>        <li>我是li</li>
>        <li>我是li</li>
>        <li>我是li</li>
>    </ul>
>```

>```javascript
> // DOM 提供的方法（API）获取
>        var ul = document.querySelector('ul');
>        var lis = ul.querySelectorAll('li');
>        // 1. 子节点  childNodes 所有的子节点 包含 元素节点 文本节点等等
>        console.log(ul.childNodes);
>        console.log(ul.childNodes[0].nodeType);
>        console.log(ul.childNodes[1].nodeType);
>        // 2. children 获取所有的子元素节点 也是我们实际开发常用的
>        console.log(ul.children);
>```

> 第一个子节点   	parentNode.firstChild

​	返回第一个子节点，找不到返回null  同样包含所有节点



> 最后一个子节点   	parentNode.lastChild

​	返回最后一个子节点，找不到返回null  同样包含所有节点



> 第一个元素节点  parentNode.firstElementChild

返回第一个子元素节点，找不到返回null  



> 最后一个元素节点  parentNode.lastElementChild

返回最后一个子元素节点，找不到返回null  



实际开发 firstChild 和 lastChild 包含 其他节点。操作不方便，而 lastElementChild 和

firstElementChild  存在兼容性 ，如何获取去第一个子元素节点或者最后一个元素节点啊？？

>解决方案：

1.第一个子元素节点 ： parentNode.children [0]

2.最后一个子元素节点：parentNode.children [parentNode.children.length - 1]



```html
    <ol>
        <li>我是li1</li>
        <li>我是li2</li>
        <li>我是li3</li>
        <li>我是li4</li>
        <li>我是li5</li>
    </ol>
```

```javascript
 var ol = document.querySelector('ol');
        // 1. firstChild 第一个子节点 不管是文本节点还是元素节点
        console.log(ol.firstChild);
        console.log(ol.lastChild);
        // 2. firstElementChild 返回第一个子元素节点 ie9才支持
        console.log(ol.firstElementChild);
        console.log(ol.lastElementChild);
        // 3. 实际开发的写法  既没有兼容性问题又返回第一个子元素
        console.log(ol.children[0]);j
        console.log(ol.children[ol.children.length - 1]);
```



> 兄弟节点

```javascript
 var div = document.querySelector('div')

//1. node.nextSibling  下一个兄弟节点
console.log(div.nextSibling)

// 2. node.nextElementSibling  下一个兄弟元素节点
console.log(div.nextElementSibling)


// 3. 上一个兄弟节点
console.log(div.previousSibling)

// 4.上一个 兄弟元素节点
console.log(div.previousElementSibling)

```



> 创建节点 

```javascript
     // 1.创建节点
        var li = document.createElement('li')


        // 2.添加节点
        var ul = document.querySelector('ul')
        // 它将我们新创建的li节点 添加到ul列表中
        // 它是从末尾中添加 从后面添加
        ul.appendChild(li)
```

> 添加节点

```javascript
 // insertBefore
        var li2 = document.createElement('li')
        ul.insertBefore(li2, ul.children[0])


        // node.insertBefore 
        var ol = document.createElement('ol')
        // ul.insertBefore(ol, ul)  // error  
        // insertBefore  插入的是  node的子节点
        ul.insertBefore(ol, ul.children[ul.children.length - 1])
```

