---
title: DOM节点和BOM节点
date: 2022/7/22 19:46:50
author: shilizhuang
categories: javascript
tags: 
	- js 
	- Markdown
---

#### 什么是事件？

​	事件就是在编程过程中系统内发生的动作或者事情，例如鼠标经过、点击、离开等等

#### 什么是事件监听？

​	事件监听就是让程序检测是否有事件发生，如果有，就调用一个函数做出响应，也叫注册事件

#### 语法：

​	元素.addEventListener('事件', 要执行的函数)

#### 事件监听三要素：

1. 事件源，那个DOM元素被触发了，就获取那个DOM元素
2. 事件，用什么方式触发的
3. 事件调用函数，DOM元素触发了之后要做什么事

```javascript
例如：
    给button按钮添加了一个事件监听，当点击按钮的时候浏览器会弹出一个消息
    `let btn = document.querySelector('button')
        btn.addEventListener('click', function () {
            alert('点了一下')
        })`
```

```javascript
拓展：
	绑定事件监听，这种写法也可以添加事件监听
    事件源.on事件 = function(){} 例如：
    let btn = document.querySelector('button')
    btn.onclick = function() {
        alert('检测到事件')
    }
```

#### 事件类型：

1. 鼠标事件

	1. 鼠标点击 click
	2. 鼠标经过 mouseenter
	3. 鼠标离开 mouseleave
	4. 鼠标移动 mousemove
	5. 鼠标双击 dblclick

2. 表单事件

  获得焦点 focus

  失去焦点 blur

  表单value值发生变化 changet

  表单提交 submit

3. 键盘事件

	键盘按下触发 keydown

	键盘抬起触发 keyup

4. 文本事件

	用户输入事件 input

5. 滚动事件

	  屏幕滚动 scroll

6. 加载事件

	 页面加载 window.addEventListener('load', function(){})

	  DOM内容加载事件 DOMContentLoade

7. 重置事件

	元素大小发生变化时候触发


```
i++ 和 i = i + 1 不一样，当i是数字时没有区别，但是当i是字符串的时候，i++会把i转换成数字,而i = i + 1则是字符串拼接
```

#### 高阶函数：

- 函数表达式

	- 函数可以作为值来进行参数传递

		```javascript
		let fn = function(){}
		/*这就是一个函数表达式*/
		```

		​

- 回调函数

	- 被作为参数传递的函数就叫回调函数

		```javascript
		btn.addEventListener('click', function(){
		    alert('这就是一个回调函数')
		})
		```

		​

#### 环境对象：

- 什么是环境对象？

	环境对象是函数内部特殊的变量this，它指向当前函数运行时所指向的环境

- 环境对象有什么用？

	明白this的指向之后我们可以使代码更清晰简洁

	谁调用this，this就指向谁。

	​

#### 编程思想-排他思想

```javascript
 let btnList = document.querySelectorAll('button')
 for (let i = 0; i < btnList.length; i++) {
     btnList[i].addEventListener('click', function () {
         //排他思想最重要的就是先排除数组里的所有元素属性或者样式
         /*for (let j = 0; j < btnList.length; j++) {
             btnList[j].classList.remove('pink')
         }*/
         //我们也可以通过查找第一个有pink类的对象来删除Pink类，这样就不用循环减少了代码复杂度
         document.querySelector('.pink').classList.remove('pink')
         //然后再通过this让自己添加属性或者样式
         this.classList.add('pink')
     })
 }
```

