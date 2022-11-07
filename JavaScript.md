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