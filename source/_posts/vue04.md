---
title: vue2基础知识04
date: 2022/7/23 20:52:20
author: shilizhuang
categories: vue2
tags: 
	- vue2 
	- Markdown
---
### vue指令

#### v-cloak指令

1. v-cloak没有具体值

2. v-cloak指令在vue实例绑定了容器以后就会消失

3. 
   ```html
	<style>
	    [v-cloak]: {
	        display: none
	    }
	</style>
	<div v-cloak>我是个演示案例</div>
	<!-- v-cloak指令可以用在网络加载慢的时候 --!>
	```

	

#### v-once指令

1. v-once指令也没有具体值

2. v-once指令绑定的容器在初次渲染完以后就不会在发生数据变化

3. 
```html
	<div class="app">
		<p v-once>{{n}}<//p> // 插值表达式里的n值在初次渲染显示出来以后，不管接下来n值在怎么变,p标签里的文本值都不会再改变了 
	<//div>
	<script>
		new Vue({
	    el: '.app'
	    data(){
	        n: 1
	    }
	})
	</script>
	```

4. 

#### v-pre指令

1. v-pre同样的也没有具体的值，它使绑定的DOM元素跳过Vue渲染的过程，加快加载速度

2. 所以这条指令最好用在没有模板语法的元素上

3. 
   ```html
	<div>
	    <p v-pre>这是个演示DOM</p>
	</div>
	```

4. 

### 自定义指令

1. 定义语法：

	+ 局部指令

		```js
		new Vue({
		    directives:{指令名:配置对象}
		})
		// 或者
		new Vue({
		    directives:{指令名:回调函数}
		})
		```


	+ 全局指令

		```js
		Vue.directive(指令名:配置对象)
		// 或者
		Vue.directive(指令名:回调函数)
		```

		

2. 配置对象中常用的3个回调函数:

	+ bind: 指令与元素成功绑定时调用
	+ inserted: 指令所在元素被插入页面时调用
	+ update: 指令所在模板结构被重新解析时调用

3. 备注：

	1. 指令定义时不加v-，但使用时要加v-
	2. 指令名如果是多个单词，要使用kebab-case命名方式，不要使用小驼峰命名
	3. 指令里的回调函数中的this指向window

### 生命周期

1. beforecreate 
	数据监测和数据代理创建之前，data和methods不可用
2. created
   数据监测和数据代理创建完毕，可以使用data和methods
3. beforemount
   虚拟DOM生成
4. mounted（重点）
   虚拟DOM插入页面生成实际DOM，
	 Ajax请求，定时器和订阅开启
5. beforechange
   数据源发生变化，页面还未重新渲染
6. changed
	 页面重新渲染完毕
8. beforedestroy（重点）
	 vm即将销毁，数据和方法还可以使用，但是不推荐
	 关闭定时器和订阅
9.  destroyed


### 组件
#### vue中使用组件的三大步骤：
1. 定义组件
2. 注册组件
3. 使用组件

#### 一、如何定义一个组件
使用Vue.extend(options)创建，其中options和new Vue(options)时传入的options几乎一样，但是也有区别：
区别如下：
   1. el不要写，为什么？-最终所有的组件都要经过一个vm的管理，其中vm中的el决定服务那个容器。
   2. data必须写成函数，为什么？-避免组件复用时，数据存在引用关系。
   备注：使用template可以配置组件结构。

#### 二、如何注册组件
   1. 局部注册：靠new Vue()时传入components选项
   2. 全局注册，靠Vue.component('组件名',组件)

#### 三、编写组件标签：

   1. 关于组件名：
      + 一个单词组成：
   			第一种写法： school
   			第二种写法：school
      + 多个单词组成：
   			第一种写法：my-school
   			第二种写法: MySchool(需要vue脚手架)
   2. 关于组件标签
     	第一种写法：<school></school>
     	第二种写法：<school/> (需要脚手架)

   3. 简写方式:
   		const school = Vue.extend(options) === const school = options