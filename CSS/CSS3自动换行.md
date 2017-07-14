# CSS3 word-break 属性

在恰当的断字点进行换行。    

## 定义和用法

`word-break` 属性规定自动换行的处理方法。   

`提示：`通过使用 word-break属性，可以让浏览器实现在任意位置的换行。    

|默认值:|normal|
| 继承性:|yes  |
|版本: |CSS3   |
|JavaScript语法:|object.style.wordBreak="keep-all"|

## 语法

```
word-break:normal|break-all|keep-all;
```

|值      |描述     |
|:-------| :------|
|normal  |使用浏览器默认的换行规则。|
|break-all|允许在单词内换行。      |
|keep-all |只能在半角空格或连字符处换行。|

1. (IE浏览器)连续的英文字符和阿拉伯数字，使用word-wrap:break-word;或者 word-break:break-all;实行强制断行     

2. (Firefox浏览器)连续的英文字符和阿拉伯数字的断行，Firefox的所有版权的没有解决这个问题，我们只要让超出边界的字符隐藏或者给容器添加滚动条    

```
#wrap{word-break:break-all;width:200px;overflow:auto;}

<div id="wrap">sjdkfjslkjdafklsjdfkljsdkfjskdjfksdkfjksldjfdjskgk12345678</div>
```

效果：容器正常，内容隐藏       

[CSS样式自动换行(强制换行)](http://blog.csdn.net/ye987987/article/details/8011875)
