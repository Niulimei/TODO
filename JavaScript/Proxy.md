# Proxy

Proxy对象用于定义基本操作的自定义行为(例如，属性查找，赋值，枚举，函数调用，等)。        

## 术语

`handler`   包含traps(陷阱)的占位符对象。      

`traps`   提供属性访问的方法。这类似于操作系统中traps(陷阱)的概念。     

`target`  代理虚拟化的对象。它通常用作代理的存储后端。     

根据目标验证关于对象不可扩展性或不可配置性的不变量(保持不变的语义)

## 语法

>> let p = new Proxy(target,handler);     

### 参数

`target` 一个目标对象(可以是任何类型的对象，包括本机数组，函数，甚至另一个代理)用Proxy来包装。    

`handler` 一个对象，其属性是当执行一个操作时定义代理的行为的函数。      

## 方法

Proxy.revocable()    
创建一个可撤销的代理对象。    

## handler 对象的方法

handler 对象是一个占位符对象，它包含代理的陷阱。     

## 示例

### 基础示例





# 参考文献

[参考文献](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy)