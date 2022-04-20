# webpack

webpack基础使用

### 第一步： yarn init         初始化包环境      

按完 enter （回车） 

包名叫...  base   (不能有特殊符号和中文)

第二个是版本

第三个描述

第四个是主入口  --- 默认index.js

第五个是 get  的  url 地址 目前不用

第六个是作者     shiqi

第七个开源许可   默认就行

第八个仓库是否是私有的  默认就行

总结：yarn init  一路回车敲到底

现象：会在你的文件夹下面生成一个   package.json  的文件



### 第二步： yarn add webpack webpack-cli -D  安装依赖包

现象：生成一个 node_modules 文件夹  和  yarn.lock 文件



### 第三步：在  package.json 定义一个自定义命令

```json
"scripts": {
    "build":"webpack"
  }
```





#### webpack基础使用  

2个js文件 -----> 打包成1个js文件

1.新建src文件夹  

2.新建一个add文件夹 新建add.js  

文件结构：

![image-20220419213739688](C:\Users\22684\AppData\Roaming\Typora\typora-user-images\image-20220419213739688.png)

add.js 

```javascript
export const addFn = (a,b) => a + b
```

index.js

```javascript
// webpack 打包入口
import { addFn } from './add/add'

console.log(addFn(5, 2));
```



最后在 cmd 里面 操作   yarn  build  会生成一个  dist文件夹

里面就是我们打包好的 js 文件



#### webpack更新打包

1.在src下面新建一个 tool 文件夹  放入  tool.js

文件结构

![image-20220419214021712](C:\Users\22684\AppData\Roaming\Typora\typora-user-images\image-20220419214021712.png)

tool.js

```javascript
export const getArrSum = arr => arr.reduce((sum,val) => {sum+=val}, 0)
```

index.js

```javascript
// webpack 打包入口
import { addFn } from './add/add'
import { getArrSum } from './tool/tool'

console.log(addFn(5, 2));
console.log(getArrSum([1, 2, 3, 4]));
```

最后再操作  yarn  build



#### webpack入口和出口

1.新建一个  webpack.config.js 文件

webpack.config.js

```javascript
const path = require('path');

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  }
};
```

配置完了然后修改 主入口名字  改 index.js  ====>  main.js

webpack 文档：

[https://www.webpackjs.com/concepts/#%E5%85%A5%E5%8F%A3-entry-](https://www.webpackjs.com/concepts/#入口-entry-)

yarn  build



#### 案例 -- 隔行换色  依赖 jQuery 完成

1.yarn init

2.yarn add webpack webpack-cli -D

3.添加自定义命令

```json
"scripts": {
    "build":"webpack"
  }
```

4.yarn add jquery

5.新建puilc 文件夹 在里面 新建 index.html  然后 ul>li{$}*10

6.新建src文件夹  和 里面新建 main .js

main.js 

```javascript
import $ from 'jquery'

// 编写隔行变色
$('#myUl > li:odd').css('color', 'pink')
$('#myUl > li:even').css('color', 'skyblue')
```

 yarn build



#### webpack 自动生成

1.yarn add html-webpack-plugin -D

webpack 文档：

https://webpack.docschina.org/plugins/html-minimizer-webpack-plugin/

2.webpack.config.js

```json
plugins: [new HtmlWebpackPlugin({  // 插件
    template: './public/index.html' //告诉webpack使用
    // 插件时候，用我们自己的html文件作为模板去生成一个dist/html 文件
  })],
```

yarn build...



#### webpack 加载器打包css文件

1.yarn add css-loader style-loader -D

2.webpack.config.js

```json
module: { //加载器
    rules: [ //规则
      {     //一个具体的对象
        test: /\.css$/, //正则 匹配.css 结尾的文件
        use: ['style-loader', 'css-loader'] 
        //让webpack使用这两个 loader处理css文件
        // 从右到左使用装备，不能颠倒顺序
        // css-loader ：webpack解析css代码 把css代码一起打包进js中
        // style-loader ： css代码插入到DOM上 （style标签） 
      }
    ]
  },
```

3.新建css文件夹  写入css文件  

4.main.js

```javascript
// 5.引入css文件
import "./css/index.css"
```

yarn  build ....



#### webpack 加载器打包less文件

1.新建less文件夹  写入less文件

2.yarn add less less-loader -D

3.使用图片 main.js 

```json
 {
        test: /\.less$/,
        use: ['style-loader','css-loader', 'less-loader']
      }
```

4.webpack.config.js

```javascript
// 6.引入less文件
import "./less/index.less"
```

yarn build ..



#### webpack打包图片文件

1.在src下面新建一个文件夹 assets 放入图片

2.main.js

```json
// 7.手动引入一个图片文件
// webpack 眼里万物皆模块
import imgObj from './assets/jennie.jpg'
let theImg = document.createElement('img')
theImg.src = imgObj
document.body.appendChild(theImg)
```

3.webpack.config.js

```json
 {  // 图片文件的配置 （仅适用于webpack 5 版本）
        test: /\.(png|svg|jpg|gif)$/,
        type: 'asset', // 匹配到上面的文件后 webpack会把他们当成
        // 静态资源处理打包
        // 如果你设置的是asset模式 以8kb大小区分图片文件
        // 小于8kb 把图片文件转base64  打包进js中
        // 大于8kb 直接把图片文件输出到dist下面
      },

```

yarn build...



#### webpack打包字体图标

1.把font文件夹放在 assets 文件夹下面

文件结构：

![image-20220420084113407](C:\Users\22684\AppData\Roaming\Typora\typora-user-images\image-20220420084113407.png)

2.main.js

```javascript

// 8. 引入字体图标文件
import './assets/font/iconfont.css'
let theI = document.createElement('li')
theI.className = 'iconfont icon-jewelry'
document.body.appendChild(theI)
```

3.webpack.config.js

```json
 {
        test: /\.(eot|svg|ttf|woff|woff2)$/,
        type: 'asset/resource',// 所有的字体图标 都输出道 dist下
        generator: { // 生成文件名字  -- 定义规则
          filename: 'fonts/[name].[hash:6][ext]'  //[ext]会替换为 .eot / .woff
        },
      },
```

yarn build .......



#### webpack集babel降级高版本js语言

1.main.js

```javascript
// 9. 书写高版本的js语法
const fn = () => { console.log('我是箭头函数') }
console.log(fn)
```

2.yarn add babel-loader @babel/core @babel/preset-env -D

3.webpack.config.js

```json
{
        test: /\.m?js$/,
        exclude: /(node_modules|bower_components)/, //不去匹配这些文件夹下的文件
        use: {
          loader: 'babel-loader', // 使用这个loader 处理js文件
          options: { // 加载器 选项
            presets: ['@babel/preset-env'] // 预设 ：@babel/preset-env 降级规则
            // 按照这里的规矩降级我们的js语法
          }
        }
      },
```

yarn build ....



#### webpack开发服务器

1.下载模块包

yarn add webpack-dev-server -D

2.package.json

```
"scripts": {
    "build": "webpack",
    "serve": "webpack serve",
  },
```

```
"scripts": {
    "build": "webpack --mode production",
    "serve": "webpack serve",
    "dev": "webpack-dev-server --open --mode development"
  },
```

本来实现 开发服务器  上面就可以了  但是打开网页会有警告 然后下面这个是配置后无警告弹出

3.修改文件内容  自动打包上传

yarn build ...

4.webpack.config.js   更改端口的位置

```json
devServer: {
    port: 1717,
  },
```

yarn build ...