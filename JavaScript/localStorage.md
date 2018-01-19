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

## 三、localStorage的使用

1. 写入数据

```
    localStorage.setItem("name","caibin");//在localStorage中存储为 name:"caibin"
    // 或者
    localStorage.name = "lucy"; //改变localStorage中存入的值
```

2. 读取数据

```
    localStorage.getItem("name"); //打印结果为你caibin
    // 或者
    let name = window.localStorage.name; //数据调取也可以使用这种方法
```

`注意：写入和读取的时候数据都是字符串`

3. 删除数据

```
    localStorage.removeItem("name"); //删除name字段存储的数据
```

4. 清空数据

```
    localStorage.clear();  //清空所有存储的数据
```

5. 对象存取

```
    const students = {
        xiaomin:{
            name:"xiaoming",
            grade:1
        },
        teemo:{
            name:"teemo",
            grade:3
        }
    }
    const stuStr = JSON.stringify(students); //{"xiaomin":{"name":"xiaoming","grade":1},"teemo":{"name":"teemo","grade":3}}

    // 将JSON对象先转化成字符串
    localStorage.setItem("students",stuStr);
    // 将读取的字符串再转化为JSON格式
    const stus = JSON.parse(localStorage.getItem("students"));

```

## cookie的使用

1. 设置cookie的值

> 每个 cookie 都是一个名/值对，可以把下面的字符串赋值给 document.cookie：

```
document.cookie="userId=828"; 
// 如果要一次存储多个名/值对，可以使用分号（;）隔开，
document.cookie="userId=828;userName=hulk";
```


2. 修改cookie值

> 重新赋值即为修改。

```
document.cookie="userId=929";
```

3. cookie的读取

```
let strCookie = document.cookie;
console.log(strCookie); // userName=hulk;userId=828
```

4. 设置cookie的失效日期

> 在默认情况下，一个 cookie 的生命周期就是在浏览器关闭的时候结束。如果想要 cookie 能在浏览器关掉之后还可以使用，就必须要为该 cookie 设置有效期，也就是 cookie 的失效日期。

5. 设置cookie可访问的路径

> 为了控制cookie可以访问的目录，需要使用path参数设置cookie

```
document.cookie="userId=929; path=/shop"; // 表示当前cookie仅在shop目录下使用。 
document.cookie="userId=929; path=/";     // 表示当前cookie在整个网站下可用。
```

## sessionStorage

```
  sessionStorage.getItem(key):获取指定key本地存储的值
  sessionStorage.setItem(key,value)：将value存储到key字段
  sessionStorage.removeItem(key):删除指定key本地存储的值
  sessionStorage.length是sessionStorage的项目数

```

[参考链接](http://www.css88.com/archives/tag/localstorage)