---
title: vue2基础知识02
date: 2022/7/22 19:53:45
author: shilizhuang
categories: vue2
tags: 
	- vue2 
	- Markdown
---
## 过滤器

#### 什么是过滤器

​	过滤器是`vue`为开发者提供的功能，常用于文本的格式化。过滤器可以用在两个地方：

​	过滤器应该被添加到JavaScript表达式的尾部，由__管道符__进行调用

+ 插值表达式

	+ ```js
		 <!-- 通过管道符调用过滤器 -->
		        <p>{{message | capi}}</p>
		```

+ v-bind属性绑定

+ 注意，在`vue3`中过滤器已被移除

+ 过滤器的声明必须在filters节点下

	+ ```js
		filters: {
		                // 过滤器函数中的形参val永远代表管道符|前面的值
		                capi(val) {
		                    let newStr = val.toUpperCase()
		                    return newStr
		                },
		            }#### 私有过滤器
		```

		

	

+ 私有过滤器

​		在filters节点下定义的过滤器函数就是私有过滤器，只能在当前`vue`实例中起效

+ 全局过滤器

	可以在多个`vue`实例中共享的过滤器

	```js
	// 定义全局过滤器
	        // Vue.filter()方法定义的过滤器独立于vue实例，不同的vue实例都可以使用
	        // vue.filter()方法需要传递两个参数，第一个是过滤器函数名，第二个是处理函数
	        // str参数代表管道符前的数据
	        Vue.filter('capi', function (str) {
	            let first = str.charAt(0).toUpperCase()
	            let other = str.slice(1)
	            return first + other
	        })
	```

	如果全局过滤器和私有过滤器名字重复，`vue`实例对象会根据就近原则调用私有过滤器，可以连续调用多个过滤器，过滤器可以进行传参，但是第一个参数默认是管道符前面的数据

#### 侦听器

+ 侦听器watch是用来监视数据的变化，并针对数据的变化作出特定的操作

	语法格式如下：

	```js
	// 侦听器
	        watch: {
	            // 侦听username的变化
	            // newVal是变化后的值，oldVal是是原来的值
	            username(newVal, oldVal) {
	                console.log(newVal, oldVal);
	            },
	        }
	```

	

##### 侦听器的格式

1. 方法格式的侦听器

	+ 缺点：无法在刚进入页面的时候自动触发
	+ 缺点2：如果侦听的是一个对象，对象里面的属性发生变化，侦听器不会触发

2. 对象格式的侦听器

	+ 优点：可以通过**immediate**选项，让侦听器自动触发

	+ 可以通过deep选项让侦听器进行深度侦听

	+ ```js
		username: {
		                // 侦听器的处理函数
		                handler(newVal) {
		                    console.log(newVal);
		                },
		                // immediate选项的默认值是false，true是让处理函数自动触发一次
		                immediate: true,
		            }
		 // 如果要侦听具体的对象属性，则要在外套一层单引号
		            'info.name': {
		                handler(newVal) {
		                    console.log(newVal);
		                },
		                deep: true,
		            }
		```

​		

##### 计算属性

特点： 

1. 定义的时候要定义成**方法**
2. 在使用计算属性的时候，当成普通的属性使用即可

好处： 

1. 实现了代码复用
2. 只要计算属性中依赖的数据源变化了，则计算属性会自动重新求值

实例： 

```js
// 计算属性必须定义咋computed节点下
      computed: {
        rgb() {
          return `rgb(${this.r},${this.g},${this.b})`
        },
      },
```



##### `axios`

1. 调用`axios`返回的是`primise`的对象

2. `axios`得到数据后会在真实数据外层套上一层配置

3. `axios`get请求

	```js
	 // 调用axios
	        axios({
	            methods: 'GET',
	            url: 'http://liulongbin.top:3006/api/getbooks',
	            // 查询参数
	            params: {
	                id: 1,
	            }
	        }).then((res) => {
	            console.log(res)
	        })
	```

	

4.  只要是`primise`实例对象，都可以在前面添加await await只能用在`async`修饰的方法中

	```js
	document.querySelector('#btn').addEventListener('click', async function () {
	            // 只要是primise实例都可以在前面修饰await,也就是异步任务可以进行等待
	            await axios({
	                method: 'POST',
	                url: 'http://liulongbin.top:3006/api/post',
	                // 请求体参数
	                data: {
	                    name: 'zs',
	                    age: 14,
	                }
	            }).then((res) => {
	                console.log(res);
	            })
	        })
	```

	

5.  解构赋值

	```js
	// 只要是primise实例都可以在前面修饰await,也就是异步任务可以进行等待
	            // 解构赋值，可以使用:重命名
	            const { data: body } = await axios({
	                method: 'POST',
	                url: 'http://liulongbin.top:3006/api/post',
	                // 请求体参数
	                data: {
	                    name: 'zs',
	                    age: 14,
	                }
	            })
	```

	

#### `vue-cli`的使用

1. 在终端下使用一下命令，创建指定项目

	```js
	vue create demo-first
	```

	![image-20220703085737387](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220703085737387.png)

	建议在开发过程中选择第三项手动配置需要安装的功能

2.  选择要安装的功能

	![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220703090814184.png)

3.  `vue`项目`src`目录的构成

	```
	assets 文件夹：存放项目中用到的静态资源文件
	comments 文件夹：程序员封装的、可复用的组件
	main.js 是项目的入口文件。整个项目的运行，都要先执行main.js
	app.vue 是项目的根组件
	```

	

4. `vue`项目的运行流程

	将`app.vue`里面的内容通过`main.js`渲染到`index.html`的指定区域,

	$mount()方法和el属性的效果是一样的

5. `vue`组件

	+ template：组件的模板解构

	+ script：组件的**js**行为

		组件里面的script标签里面必须写export default()默认导出，固定写法，

		定义数据data必须是函数

	+ style：组件的样式

		
