---
title: 无框架版TodoList
permalink: ch1015
date: 2017-3-21 10:10:10
categories:
- 前端
tags:
- javascript
- 前端
- todolist
- API
---
## 前言
花了两天终于撸完todolist这个玩意了，
效果看:[TodoList](http://cheesekun.top/todolist/)
感觉学习到和意识到一些东西
## 前前言
身为个前端萌新，很多时候都不知道拿什么练手
而很多时候，大多数人都推荐做个TodoList
网上大部分人做的例子都是使用了各种框架各种库
作为打基础，还是手撸个原生的TodoList比较好
(其实是不会用框架，😱)
## 知识点
- `localStorage`存储获取task数据
- `JSONP()`跨域获取api数据
- `Animate`CSS3小动画
- 字体图标的使用
- ~~contenteditable~~

## localStorage存储获取task
这个使用到上次我发的那个`localStorage`来操纵数据
不了解的先跳转: [localStorage](http://cheesekun.top/2017/03/13/cheesekun.top/ch1010/)
> fench()函数先获取浏览器上"todolist"的数据，若没有，就用todos作为数组存储数据并转化为json
> save()函数将获取到数据转化为json字符串，在存入到STORAGE_KEY中

```javascript
var STORAGE_KEY = "todolist";
var todoStorage = {
  fetch: function() {
    var todos = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
    return todos;
  },
  save: function(todos) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(todos));
  }
};
var todos = todoStorage.fetch();
```
## JSONP跨域获取api数据
这个我之前也总结过一篇
具体见[getJSONP跨域](http://cheesekun.top/2017/03/19/cheesekun.top/ch1014/)
这里面使用到一个天气api和一个地图api
## CSS3小动画
很少使用css3动画，不过一旦使用效果拔群，至少有点小动画，整体页面也不会特别单调
不过兼容性还是需要解决的
> 先建一个动画帧
> 再将帧名加入`animate`参数中
`animation: name duration timing-function delay iteration-count direction play-state;`
> 分别为 帧名，动画完成时间，运动周期曲线，延迟时间，执行次数，是否往返播放动画，暂停或运行

```css
@keyframes swing {
  20% {
    -webkit-transform: rotate3d(0, 0, 1, 15deg);
    transform: rotate3d(0, 0, 1, 15deg);
  }
  40% {
    -webkit-transform: rotate3d(0, 0, 1, -10deg);
    transform: rotate3d(0, 0, 1, -10deg);
  }
  60% {
    -webkit-transform: rotate3d(0, 0, 1, 5deg);
    transform: rotate3d(0, 0, 1, 5deg);
  }
  80% {
    -webkit-transform: rotate3d(0, 0, 1, -5deg);
    transform: rotate3d(0, 0, 1, -5deg);
  }
  to {
    -webkit-transform: rotate3d(0, 0, 1, 0deg);
    transform: rotate3d(0, 0, 1, 0deg);
  }
}
animation: swing 5s infinite;
```
## 字体图标
和使用外部字体差不多
使用了:before, 显示如： 😃按钮
```css
@font-face {
  font-family: '字体名';
  src: url('字体链接') format('字体格式后缀');
  font-weight: normal;
  font-style: normal;
}
.btn:before {
  font-family: '字体名';
  content: "\e00f";   //图标码
}
```
```html
<button class="btn">按钮</button>
```
## contenteditable
一个神奇的属性
`<p contenteditable>123<p>`
添加到文本标签上居然就可以在页面上编辑 p标签了，突然了解到，不过我在todolist里面并没有使用它
## 就在刚刚
发现数组居然是json的一种，一直以为像对象这种键值对的存在才是json
没想到维基百科说数组也是
> 值的有序列表（Array）：一个或者多个值用,分区后，使用[，]括起来就形成了这样的列表，形如：
> [collection, collection]

具体看维基百科对JSON的定义L: [JSON](https://zh.wikipedia.org/wiki/JSON#WEB.E5.BC.80.E5.8F.91)
## 感想
一开始只是想不使用任何的框架和库来做个TodoList
不过在做的过程中想添加个天气预报，添加个随机语句，添加个css动画
都可以拓展出很多自己很少或者未曾去了解的知识
而且学习起来更有趣
之前有花了一段时间去了解的vue，es6类似的新知识，但是没使用到，渐渐地就遗忘了
十分消耗时间成本
发现去寻找制作一个东西，再在此基础上进行新的拓展，比起刻意去学习新知识，获益更多
## 结语
虽然没有使用封装，闭包，原型之类的知识，但是效果能实现已经是很大的勉励了
说到底就是自己太水了，继续加油
