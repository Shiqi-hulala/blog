# 数组方法

常见的一些**数组**操作
push 、 pop、unshift、 shift

### push 在一个数组前面添加 （前面加）

- 语法: array.push(item1, item2, …, itemX)

- push( )方法：可以将一个或者更多的参数添加在数组的尾部；返回添加后的数组的长度，原数组发生改变。

- 代码示例如下：
```js
var arr = [1,2,3,4]
var a = arr.push(9,8,7)
console.log(a,arr) //1,2,3,4,9,8,7
```

### unshift  在一个数组后面添加 （后面加）

- 语法: array.unshift(item1,item2, …, itemX)

- unshift( )方法：可以将一个或者更多的参数添加在数组的头部；返回添加后的数组的长度，原数组发生改变。

- 代码示例如下：

```js
var arr=[1,2,3,4];
var a=arr.unshift(9,8,7);
console.log(a,arr);//9,8,7,1,2,3,4；
```


### pop  删除数组末尾  （尾部删除）

- 语法：array.pop()
- pop( )方法：从数组尾部删除一个元素，返回这个被删除的元素，原数组发生改变。
- 代码示例如下：

```js
var arr=[1,2,3,4];
var a=arr.pop();
console.log(a,arr)//4；1,2,3，
```

### shift 删除数组头部 （头部删除）

- 语法：array.shift()
- shift( ) 方法：从数组头部删除一个元素，返回这个被删除的元素，原数组发生改变。
- 代码示例如下：
```js
  var arr = [1,2,3,4];
  var a = arr.shift();
  console.log(a,arr)//1；2,3,4，
```

### slice 截取数组  

- 语法：array.slice(start, end)
- slice（）方法：如果不传参数，会返回原数组；如果一个参数，从该参数表示的索引开始截取，直至数组结束，返回这个截取数组，原数组不变；
两个参数，从第一个参数对应的索引开始截取，到第二个参数对应的索引结束，但包括第二个参数对应的索引上的值，原数组不改变 &最多接受两个参数
- 代码示例如下：

```js
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus = fruits.slice(1,3);
console.log(citrus )//Orange,Lemon
```

### splice 增加数据（三个参数） 和 删除数据 （两个参数）

- 语法：array.splice(index,howmany,item1,…,itemX)
- splice( ) 方法：没有参数，返回空数组，原数组不变；
一个参数，从该参数表示的索引位开始截取，直至数组结束，返回截取的 数组，原数组改变；
两个参数，第一个参数表示开始截取的索引位，第二个参数表示截取的长度，返回截取的 数组，原数组改变；
三个或者更多参数，第三个及以后的参数表示要从截取位插入的值。

- 代码示例如下：
```js
  var fruits = ["Banana", "Orange", "Apple", "Mango"];
  fruits.splice(2,2);
  console.log(fruits )//Banana,Orange
```

### reverse 翻转数组

- 语法：array.reverse()
- reverse( )方法：用于颠倒数组中元素的顺序。。
- 代码示例如下：

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.reverse();
console.log(fruits)//Mango,Apple,Orange,Banana
```

### sort  数组排序
- 语法：array.sort(sortfunction)
- sort( ) 方法：用于对数组的元素进行排序。
- 代码示例如下：

```js
var Array = [1,2,3,4,5];
var fruits = Array.sort(function(a,b){
	//return a - b; //从小到大
	return b-a; //从大到小
})
```

### join 数组转为字符串 然后添加分隔符
- 语法：array.join(separator)
- join( ) 方法：于把数组中的所有元素转换一个字符串,元素是通过指定的分隔符进行分隔的。
- 代码示例如下：

```js
var arr = [1,2,3,4]
var bbc = arr.join()
console.log(bbc)//1,2,3,4
```

### concat  数组拼接
- 语法：string.concat(string1, string2, …, stringX)
- concat( ) 方法：属于字符串的方法，数组也可以用，接受一个或多个参数，将参数中的值放到操作的数组后边，返回拼接的数组，原数组不变。如果参数是一个数组，则先把值提取出来再操作。
- 代码示例如下：

```js
var arr = [1,2,3,4];
arr.concat([5,6,7])//[1,2,3,4,5,6,7]
```



# ES5新增的一些数组方法

### indexOf（） 查询指定字符在字符串中首次出现位置 返回 对应索引值

- 语法：string.indexOf(searchvalue,start)
- indexOf( ) 方法：字符串的方法，数组也可适用，此方法可返回某个指定的字符串值在字符串中首次出现的位置；若一个参数，返回这个参数在数组里面的索引值，如果参数不在操作的数组中，则返回 -1。
- 代码示例如下：

```js
var arr = [1,2,3,4];
  arr.indexOf(1) // 0
  arr.indexOf(5) // -1 
```


### forEach（）遍历数组
- 语法：array.forEach(function(currentValue, index, arr), thisValue)
- forEach( ) 方法：数组遍历，且只能够遍历数组，不接受返回值或返回值为 undefined。
- 代码示例如下：

```js
var arr = [1,2,3,4,5];
arr.forEach((item,index,arr)=>{
   //item 为当前数组元素
   // index 为当前索引
   // arr 为数组名字
})
```


### map（） 遍历某个数组 然后对这个数组进行操作 返回操作后的数组
- 语法：array.map(function(currentValue,index,arr), thisValue)
- map( ) 方法：数组的遍历，用来接收一个返回值，创建一个新数组，不改变原数组。
- 代码示例如下：

```js
var arr = [1,2,3,4,5,6];
arr.map(function(item,index,arr){
	return item * 2
})
//输出 [2,4,6,8,10,12]
```

### filter（）过滤
- 语法：array.filter(function(currentValue,index,arr), thisValue)
- filter( ) 方法：过滤出一些符合条件的元素，返回一个新数组。
- 代码示例如下：

```js
var ages = [32, 33, 16, 40];

function checkAdult(age) {
    return age >= 18;
    //返回数组 ages 中所有元素都大于 18 的元素:
}
function myFunction() {
    document.getElementById("demo").innerHTML = ages.filter(checkAdult);
}
//输出结果为：32,33,40
```

### some（）检测是否有某个值  有返回 true 没有返回 false
- 语法：array.some(function(currentValue,index,arr),thisValue)
- some( ) 方法：检测数组中是否含有某一个值，返回一个布尔值，如果数组中有任意一个元素满足给定的条件，结果就为 true否则则为false。
- 代码示例如下：

```js
var ages = [3, 10, 18, 20];

function checkAdult(age) {
    return age >= 18;
}
function myFunction() {
    document.getElementById("demo").innerHTML = ages.some(checkAdult);
}
//输出结果为：true
```

### every（） 检测所有值是否满足某个条件 返回值为布尔值
- 语法：array.every(function(currentValue,index,arr), thisValue)
- every( ) 方法：方法用于检测数组所有元素是否都符合指定条件（通过函数提供）,返回一个布尔值,结果为 true或false。
- 代码示例如下：

```js
var ages = [32, 33, 16, 40];

function checkAdult(age) {
    return age >= 18;
    //检测数组 ages 的所有元素是否都大于等于 18 
}

function myFunction() {
    document.getElementById("demo").innerHTML = ages.every(checkAdult);
}
//输出结果为：false
```

### reduce（）
- 语法：array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
- reduce( ) 方法：对数组中的所有元素调用指定的回调函数，该回调函数的返回值为累计结果。并且把返回值在下一次回调函数时作为参数提供。
- 代码示例如下：

```js
var numbers = [65, 44, 12, 4];

function getSum(total, num) {
    return total + num;
    //计算数组相加的总和
}
function myFunction(item) {
    document.getElementById("demo").innerHTML = numbers.reduce(getSum);
}
//输出结果为：125
```



# ES6新增的数组方法

### Array.from( )
- 语法：Array.from(arrayLike[, mapFn[, thisArg]])
- Array.from( ) 方法：将类数组对象或可迭代对象转化为数组，比如arguments，js选择器找到dom集合和对象模拟的数组。
- 代码示例如下

```js
// 参数为数组,返回与原数组一样的数组
console.log(Array.from([1, 2])); // [1, 2] 
// 参数含空位
console.log(Array.from([1, , 3])); // [1, undefined, 3]
```



### Array.of( )
- Array.of( ) 方法：数组创建，将参数中所有值作为元素形成数组，如果参数为空，则返回一个空数组。
- 代码示例如下：

```js
console.log(Array.of(1, 2, 3, 4)); // [1, 2, 3, 4] 
// 参数值可为不同类型
console.log(Array.of(1, '2', true)); // [1, '2', true] 
// 参数为空时返回空数组
console.log(Array.of()); // []
```



### find( )
- find( ) 方法：查找数组中符合条件的元素,若有多个符合条件的元素，则返回第一个元素。
- 代码示例如下：

```js
let arr = Array.of(1, 2, 3, 4);
console.log(arr.find(item => item > 2)); // 3 
// 数组空位处理为 undefined
console.log([, 1].find(n => true)); // undefined
```



### findIndex( )
- 查找数组中符合条件的元素索引，若有多个符合条件的元素，则返回第一个元素索引。
- 代码示例如下：

```js
let arr = Array.of(1, 2, 1, 3);
// 参数1：回调函数
// 参数2(可选)：指定回调函数中的 this 值
console.log(arr.findIndex(item => item == 1)); // 0
// 数组空位处理为 undefined
console.log([, 1].findIndex(n => true)); //0
```


### includes( )
- includes( ) 方法：检测数组中是否包含一个值。
注意：与 Set 和 Map 的 has 方法区分；Set 的 has 方法用于查找值；Map 的 has 方法用于查找键名。
- 代码示例如下：

```js
// 参数1：包含的指定值
[1, 2, 3].includes(1);    // true
// 参数2：可选，搜索的起始索引，默认为0
[1, 2, 3].includes(1, 2); // false
// NaN 的包含判断
[1, NaN, 3].includes(NaN); // true
```



### fill( )
- fill( ) 方法：将一定范围索引的数组元素内容填充为单个指定的值。
- 代码示例如下：

```js
let arr = Array.of(1, 2, 3, 4);
// 参数1：用来填充的值
// 参数2：被填充的起始索引
// 参数3(可选)：被填充的结束索引，默认为数组末尾
console.log(arr.fill(0,1,2)); // [1, 0, 3, 4]
```



### entries( )
- entries( ) 方法：遍历键值对。
- 代码示例如下：

```js
for(let [key, value] of ['a', 'b'].entries()){
    console.log(key, value);
}
// 0 "a"
// 1 "b" 
// 不使用 for... of 循环
let entries = ['a', 'b'].entries();
console.log(entries.next().value); // [0, "a"]
console.log(entries.next().value); // [1, "b"]

// 数组含空位
console.log([...[,'a'].entries()]); // [[0, undefined], [1, "a"]]
```



### keys( )
- keys( ) 方法：遍历键名。
- 代码示例如下：

```js
for(let key of ['a', 'b'].keys()){
    console.log(key);
}
// 0
// 1 
// 数组含空位
console.log([...[,'a'].keys()]); // [0, 1]
```



### values( )
- values( ) 方法：遍历键值。
- 代码示例如下：

```js
for(let value of ['a', 'b'].values()){
    console.log(value);
}
// "a"
// "b"
// 数组含空位
console.log([...[,'a'].values()]); // [undefined, "a"]
```



### flat( )
- 嵌套数组转一维数组
- 代码示例如下：

```js
console.log([1 ,[2, 3]].flat()); // [1, 2, 3] 
// 指定转换的嵌套层数
console.log([1, [2, [3, [4, 5]]]].flat(2)); // [1, 2, 3, [4, 5]] 
// 不管嵌套多少层
console.log([1, [2, [3, [4, 5]]]].flat(Infinity)); // [1, 2, 3, 4, 5]
// 自动跳过空位
console.log([1, [2, , 3]].flat());<p> // [1, 2, 3]
```



### 复制数组
- …：扩展运算符
- 代码示例如下：

```js
let arr = [1, 2],
    arr1 = [...arr];
console.log(arr1); // [1, 2]

// 数组含空位
let arr2 = [1, , 3],
    arr3 = [...arr2];
console.log(arr3); [1, undefined, 3]
//合并数组
console.log([...[1, 2],...[3, 4]]); // [1, 2, 3, 4]

```



findIndex：