---
title: vue2基础知识03
date: 2022/7/22 19:54:40
author: shilizhuang
categories: vue2
tags: 
	- vue2 
	- Markdown
---

### `vue`组件

1. 组件之间的父子关系

	组件在被封装好了以后，彼此之间是相互独立的

#### `vue`组件的使用步骤

1. 导入组件

	```js
	import HelloWorld from './components/HelloWorld.vue'
	```

	

2. 在`compoents`节点下注册组件

	```js
	export default {
	  name: 'App',
	  components: {
	    HelloWorld
	  }
	}
	```

	

3. 在template标签里面通过标签的形式使用组件

	```js
	<HelloWorld msg="Welcome to Your Vue.js App"/>
	// 注意在componets节点下注册的子组件是私有组件，只能在当前组件中使用
	```

	

4. 注册全局组件

	```js
	// 在main.js文件的script标签中，导入要注册的组件
	import left from '@/componets/left.vue'
	// 使用Vue.componets()方法注册全局组件
	Vue.componets('Left',left)
	// 参数1 要注册的全局组件名
	// 参数2 导入的组件名
	// 在想要使用该全局组件的组件的template标签中使用就行了
	<Left></Left>
	```

5. 组件的props

	+ props是组件的==自定义属性==，在封装通用组件的时候，合理地使用props可以极大的提高组件的复用性！

		```js
		export default {
		    props:['init'],
		}
		```

		

	+ props自定义属性时如果不加`v-bind:props`，那么传入的值是字符串类型

	+ props的值不能直接修改

	+ props的默认值

		```js
		// 定义成数组形式的props是没有默认值的
		export default {
		    props:{
		        init: {
		            default: 0,
		        },
		    },
		}
		```

	+ props的type类型

		```js
		export default {
		    props:{
		        init: {
		            //default选项指定init属性的默认值
		            default: 0,
		            // type选项指定init属性的类型
		            type: Number,
		        }
		    },
		}
		```

	+ props的必填选项required

		```js
		export default {
		    props:{
		        init: {
		            //default选项指定init属性的默认值
		            default: 0,
		            // type选项指定init属性的类型
		            type: Number,
		            // required选择指定在使用该组件的时候props自定义属性为必填
		            required: true,
		        }
		    },
		}
		```

		

#### 组件的样式冲突

1. 冲突的根本原因

	+ 组件的样式定义好了之后是全局生效的
	+ 只有一个`html`页面

2. scoped解决样式冲突的底层原理

	+ 在每个组件模板的每个标签中自动添加上一个自定义属性，然后通过属性选择器来定义样式

	+ ```js
		<style scoped></style>
		```

	+ 使用/deep/修改子组件的样式

		如果需要修改第三方组件或者子组件的样式，则可以在样式表里的选择器前面加上/deep/

		```css
		/deep/ h5 {
		    color: red
		}
		```

		

#### 生命周期

​	生命周期指的是一个组件从创建->运行->销毁的整个阶段

+ `vue`生命周期图例

	<img src="F:\前端\3. 第三阶段 Vue 开发\2.Vue2+Vue3全套教程\Vue2\视频\day4\day4\讲义\lifecycle.png" alt="lifecycle" style="zoom:50%;" />

##### 生命周期函数

1. 由`vue`框架提供的内置函数，会伴随组件的生命周期，自动按次序执行

2. 生命周期函数类型

	+ 创建阶段

		```js
		new Vue() -> beforeCreate -> created -> beforeMount -> mounted
		beforeCreate()// 组件的props/data/methods尚未被创建，因此无法使用，此节点函数没有实际意义
		created()// 组件的props/data/methods创建完毕，可以使用，但是组件模板结构尚未生成，此节点函数多用于ajax请求获取数据
		beforeMount()//准备将内存中编译好的HTML结构渲染到浏览器上，这个节点的函数也没有太大意义
		mounted()//已成功将编译的HTML结构渲染到浏览器上了，此节点函数多用于操作DOM节点
		```

	+ 运行阶段

		```js
		beforeUpdate -> updated
		updated//数据发生变化，updated函数可以获得最新的DOM节点
		```

	+ 销毁阶段

		```
		beforeDestroy -> destroyed
		```

		

#### 组件之间的数据共享

1. 组件之间的关系

	+ 父子关系

	+ 兄弟关系

		

##### 父子之间的数据共享

父组件向子组件共享数据需要使用自定义属性

```js
// 子组件中定义props属性用来接受父组件传递的值
export default{
    props: {
        init: {
            // 设置自定义属性为必填属性
            required:,
            // 设置自定义属性类型
            type: Number,
            // 设置自定义属性默认值
            default: 0,      
        }
    }
}
```

##### 子组件向父组件共享数据

子组件向父组件共享数据通过自定义事件

```js
// 子组件
export default{
    data(){
         message: 0,
    }
    },
    methods: {
        add(){
            this.message++,
            this.$emit('numChange',this.message)
        }
    }
}
// 父组件
<son @numChange="getNew"></son>
export default{
    data(){
        mesFromSon: 0,
    },
    methods: {
        // 通过val接受子组件的message
        getNew(val){
            // 用父组件的mesFromSon来接受val
            this.mesFromSon = val
        }
    }
}
```

##### 兄弟组件之间的数据共享

在`Vue2`的版本中，兄弟组件之间的数据共享方案是`EventBus`

```js
// 兄弟组件数据发送方
// 导入一个新的vue实例对象
import bus from './eventBus.js'
export default {
    data(){
        return{
            message: 0,
        }
    },
    methods: {
        sendMsg(){
            bus.$emit('share', this.message)
        }
    }
}
```



```js
// eventBus.js
// 导入vue构造函数
import Vue from 'vue'
// 向外共享vue的实例对象
export default new Vue()
```

```js
// 兄弟组件 数据接收方
// 导入一个新的vue实例对象
import bus from './eventBus.js'
export default {
    data(){
        return{
            mesFromBro: 0,
        }
    },
    created(){
        // 绑定兄弟组件里面的自定义事件
        bus.$on('share', val => {
            this.mesFromBro = val
        })
    }
}
```

