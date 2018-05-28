
# vue-cli配置flexable

```js
//1.在命令行中运行如下代码
npm i lib-flexible --save-dev
//2.在main.js中引入flexible
import 'lib-flexible'
//3.在html中加入meta标签
<meta name="viewport" content="width=device-widthinitial-scale=1.0"/>
//4.安装px2rem-loader
npm i px2rem-loader --save-dev
//5.在utils.js中配置
var px2remLoader = {
    loader:'px2rem-loader',
    options:{
        remUnit:75
    }
}
//6.并放进loaders数组中
function generateLoaders(loader,loaderOptions){
    var loaders = [cssLoader,px2remLoader]
    //...
}

```