# 面试总结
## js面试问题
### 如何编写Vue插件
- 参考:
[Vue插件编写](https://blog.csdn.net/sinat_17775997/article/details/72085163)

---
1. 使用全局变量的对象来用作单例模式来使用,在这个单例对象下来写我们的插件
2. 给我们的插件添加install方法,将我们的插件挂载到Vue的原型上,然后将我们的插件导出到全局
3. 在Vue中引入我们的插件,使用Vue.use,将我们的插件传入第一个参数,将我们的配置参数传入第二个参数

### 说说你对webpack的理解
1. webpack是一个js最新的模块管理器,当webpack处理应用的时候,他会递归创建一个依赖图谱,这个图谱会详细的列出应用需要的每一个模块,最终将这些模块打包到小的输出文件中

### Promise有几种方法

```
1. Promise.all
2. Promise.race
3. Promise.reject
4. Promise.resolve
5. Promise.prototype.catch
6. Promise.prototype.finally
7. Promise.prototype.then
```


### 如何判断数组是不是数组

```
1. objectName instanceof Array
2. objectName.constructor == Array
3. 特性判断
  function isArray(object){
    return  object && typeof object==='object' &&    
            typeof object.length==='number' &&  
            typeof object.splice==='function' &&    
             //判断length属性是否是可枚举的 对于数组 将得到false  
            !(object.propertyIsEnumerable('length'));
}
4.Array.isArray(objectName);
5.Object.prototype.toString.call(objectName)
```
### js继承有哪几种方式

```
        //js继承的方式
        /*
            1.借助构造函数实现继承
            缺点: 不能继承父类原型的属性和方法
        */
        function Parent1(){
            this.name = 'parent1'
        }
        Parent1.prototype.say = 'hi'

        function Child1(){
            Parent1.call(this);
            this.name = 'child1'
        }

        new Child1

        /*
            2.借助原型链实现继承
            缺点: 父类的属性和方法,子类实例都是共享的
        */
        function Parent2(){
            this.name = 'Parent2'
            this.play = [1,2,3,4]
        }

        function Child2(){
            this.name = 'Child2'
        }

        Child2.prototype = new Parent2()

        var o1 = new Child2();
        var o2 = new Child2();

        o1.play.push(5)
        o1.play // [1,2,3,4,5]
        o2.play // [1,2,3,4,5]

        /*
            3.组合方式
            缺点: 子类实例化的时候,父类被调用了2次
        */
        function Parent3(){
            this.name = 'parent3'
            this.play = [1,2,3,4]

        }

        function Child3(){
            Parent3.call(this)
            this.name = 'child3'
        }

        Child3.prototype = new Parent3();

        var o1 = new Child3();
        var o2 = new Child3();

        o1.play.push(5)
        o1.play //[1,2,3,4,5]
        o2.play //[1,2,3,4]

        /*
            组合方式的优化1
            缺点: 子类实例无法确定构造函数是谁
        */
        function Parent4(){
            this.name = 'parent4'
            this.play = [1,2,3,4]

        }

        function Child4(){
            Parent3.call(this)
            this.name = 'child4'
        }

        Child4.prototype = Parent4.prototype;

        var o1 = new Child4();

        o1 instanceof Child4 //true
        o1 instanceof Parent4 //true
        
        o1.constructor //Parent4

        /*
            组合继承优化2
        */
        function Parent5(){
            this.name = 'Parent5';
        }
        function Child5(){
            Parent5.call(this)
            this.name = 'Child5';
        }
        Child5.prototype = Object.create(Parent5.prototype)
        Child5.prototype.constructor = Child5

        var o1 = new Child5();
        
        o1 instanceof Child5 //true
        o1 instanceof Parent5 //true
        o1.constructor //Child5
```

### 什么是闭包,闭包有什么用
闭包是在某个作用域内定义的函数,它可以访问这个作用域内的所有变量,闭包作用域链通常包含三个部分:

1.函数本身作用域

2.闭包定义时的作用域

3.全局作用域

常见用途:

1.创建特权方法用于访问控制
2.事件处理程序及回调

### Vuex如何实现单向数据流动

单向数据流”理念的极简示意：
![image](https://vuex.vuejs.org/zh-cn/images/flow.png)

Vuex分成四个部分：

- State：单一状态树
- Getters：状态获取
- Mutations：触发同步事件
- Actions：提交mutation，可以包含异步操作

![Vuex](http://img.souche.com/20161214/png/750205ca124c5065c6ef47c5913221a3.png)

```
1. 用户访问页面并触发action
2. action提交mutation事件
3. mutation事件更改state状态
4. state状态改变后更新页面(vue comptents)
```

### Vue组件如何传递数据

> 父向子传递数据

1.使用props，父组件可以使用props向子组件传递数据。

2.使用$children使用$children可以在父组件中访问子组件。

> 子向父通信

1.父组件向子组件传递事件方法，子组件通过$emit触发事件，回调给父组件。

2.使用$parent可以访问父组件的数据。

> 兄弟通信

1.eventBus

> 深层父子,子孙组件通信

1.$attrs

2.$listeners

> Vuex通信

复杂的单页应用数据管理
当应用足够复杂情况下，请使用vuex进行数据管理。





