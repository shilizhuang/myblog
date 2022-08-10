---
title: DOM节点和BOM节点
date: 2022/7/22 19:48:12
author: shilizhuang
categories: javascript
tags: 
	- js 
	- Markdown
---

### 什么是DOM？

- DOM就是文档对象模型，用来呈现以及和交互任意HTML或XML文档的API
- DOM用来开发网页特效和实现人机交互

### DOM树

- 将HTML文档结构通过树状结构直观的表现出来，就叫DOM树
- 描述网页内容结构的名词
- 作用：文档树直观的体现了标签与标签之间的关系

### DOM对象（重要）

- DOM对象：浏览器根据html标签生成的 JS对象
	-  所有的标签属性都可以在这个对象上面找到
	- 修改这个对象的属性会自动映射到标签身上
- DOM的核心思想
	- 把网页内容当做对象来处理
- document 对象
	- 是 DOM 里提供的一个对象
	- 所以它提供的属性和方法都是用来访问和操作网页内容的
	- 例：document.write()
	-  网页所有内容都在document里面

### 获取DOM对象

- 根据css选择器来获取

  ```
  let 变量名 = document.querySelecter('css选择器') 
  ```

  这种方法只能匹配到第一个符合条件的元素，如果没匹配到就返回null

  ```
  let 变量名 = document.querySelecterAll()
  ```

  返回匹配到的nodelist对象集合，这个集合是一个伪数组，想要对集合里面的对象进行操作的话得先遍历集合或者通过下标来获取集合里面的对象

- 其他方法来获取

	![65405013321](C:\Users\ADMINI~1\AppData\Local\Temp\1654050133218.png)

### 设置/修改DOM元素内容有哪3钟方式？

- document.write() 方法
- 元素.innerText 属性
- 元素.innerHTML 属性

### 三者的区别是什么？

- document.write() 方法 只能追加到body中 
- 元素.innerText 属性 只识别内容，不能解析标签
- 元素.innerHTML 属性 能够解析标签
- 如果还在纠结到底用谁，你可以选择innerHTML

### 修改对象属性

- 修改自身属性

​	对象名.属性名 = ‘属性值’

- 修改样式属性

	对象名.style.属性名 = ‘属性值’

	还可以先给类名设置样式属性，设置好了之后给对象添加类名来修改对象样式属性

	对象名.className = '类名' 这种方法添加的类名会覆盖原有的类名

	- 追加一个类

		对象名.classNameList.add('类名')

	- 删除一个类

		对象名.classNameList.remove('类名')

	- 切换一个类

		对象名.classNameList.toggle('类名')

### 修改表单元素属性

​	表单对象.属性名 = ‘属性值’

​	表单元素中一些属性值用布尔值来表示，true代表添加，false代表删除，例如：disabled、checked、		selected

### 定时器-间歇函数

1. 定时器函数有什么作用？

	可以根据时间自动重复执行某些代码

2. 定时器函数如何开启？

	setInterval(函数名, 时间)

3. 定时器函数如何关闭？

	clearInerval(定时器变量名)

​		

