# 错误与异常

```javascript
try {
	window.someNonexistentFunction();
} catch (error) {
  const { name, message, stack } = error
  console.log(name, message, stack);
}
```

catch的error参数是一个对象,typeof error = 'object'，有3个属性，name：异常类型，如TypeError；message：异常信息；stack：异常所在的堆栈(代码在哪行出错的)

# inner offset scroll client

inner系列只有window具有，而offset、scroll、client系列只有Element类型的dom节点具有

## window

- window.screenLeft 浏览器距离屏幕左侧的距离（兼容window.screenX）
- window.screenTop 浏览器距离屏幕上方的距离（兼容window.screenY）
- window.innerWidth 浏览器可视区域宽度，包含滚动条。（只计算在滚动区域里能看到部分的宽度，溢出隐藏的部分不计算，非文档整体宽度）
- window.innerHeight 浏览器可视区域高度， 包含滚动条。（只计算在滚动区域里能看到部分的高度，溢出隐藏的部分不计算，非文档整体高度）

## screen

- screen.width 屏幕的宽度（div宽度定义为屏幕的宽度是正好没有滚动条的）
- screen.height 屏幕的高度（div高度定义为屏幕的高度是有滚动条的，因为浏览器有标签栏、地址栏等占用一部分屏幕高度）

## element

只适用于Element类型，例如document.documentElement或任意一个dom节点，（window上不具有这些属性）

- element.clientWidth 内容宽度+padding，不包含滚动条（滚动条会挤占一部分内容宽度）
- element.clientHeight 内容高度+padding，不包含滚动条（滚动条会挤占一部分内容宽度）
- element.clientLeft 元素左边框的宽度（非距离浏览器左侧的距离）
- element.clientTop 元素上边框的高度（非距离浏览器上方的距离）

- element.offsetWidth 内容宽度+padding+边框，不包含滚动条（相比client多了边框）
- element.offsetHeight 内容高度+padding+边框，不包含滚动条

- element.offsetTop 元素相对于最近的定位祖先元素的距离（没有最近的定位祖先元素，就相对于body）
- element.offsetHeight 元素相对于最近的定位祖先元素的距离（没有最近的定位祖先元素，就相对于body）
- element.scrollWidth 计算具有滚动条时的实际宽度，实际内容宽度+padding
- element.scrollheigth 计算具有滚动条时的实际高度，实际内容高度+padding
- element.scrollTop 垂直滚动条滚动距离（window不具有此属性）
- element.scrollLeft 水平滚动条滚动距离（window不具有此属性）



# window专属事件

- resize 监听浏览器窗口大小改变事件
- scroll 监听滚动条事件（也可以监听document.documentElement的scroll事件）