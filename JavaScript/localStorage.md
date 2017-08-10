# localStorage 使用总结

## 一、什么是localStorage、sessionStorage

在HTML5中，新添加了一个localStorage特征，这个特性主要是来作为本地存储来使用的，解决了cookie存储空间不足的问题(cookie中每条cookie的存储空间为4k),localStorage中一般浏览器支持的是5M大小，这个在不同的浏览器中localStorage会有所不同。       

## 二、localStorage的优势与局限

- localStorage的优势     

1. localStorage拓展了cookie 的4K限制    

2. localStorage 会可以将第一次请求的数据直接存储到本地，这个相当于一个5M大小的针对于前端页面的数据库，相当于cookie可以节约宽带，但是这个却是只有在高版本的浏览器中才支持的       

- localStorage 的局限     

1. 浏览器的大小不统一，并且在IE8以上的IE版本才支持localStorage这个属性    

2. 目前所有的浏览器中都会把localStorage的值类型限定为string类型，这个在对我们日常比较常见的JSON对象类型需要一些转换       

3. localStorage在浏览器的隐私模式下面是不可读取的     

4. localStorage本质上是对字符串的读取，如果存储内容多的话会消耗内存空间，会导致页面变卡     

5. localStorage不能被爬虫抓取到     

`localStorage与sessionStorage的唯一一点区别就是localStorage属于永久性存储，而sessionStorage属于当会话结束的时候，sessionStorage中的键值对会被清空`       


```
  sessionStorage.getItem(key):获取指定key本地存储的值
  sessionStorage.setItem(key,value)：将value存储到key字段
  sessionStorage.removeItem(key):删除指定key本地存储的值
  sessionStorage.length是sessionStorage的项目数

```

[参考链接](http://www.css88.com/archives/tag/localstorage)