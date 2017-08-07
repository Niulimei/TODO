# JSON

JSON：JavaScript Object Notation(JavaScript 对象表示法)   

JSON 是存储和交换文本信息的语法。类似XML。      

JSON 比 XML 更小、更快，更容易解析。     

JSON - 转化为 JavaScript对象：JSON文本格式在语法上与创建JavaScript对象的代码相同。      

由于这种相似性，无需解析器，JavaScript程序能够使用内建的 eval()函数，用JSON数据来生成原生的JavaScript对象。     


## JSON 键/值对 
  JSON键值对是用来保存JS对象的一种方式，和JS对象的写法也大同小异，键/值对组合中的键名写在前面并用双引号""包裹，使用冒号:分隔，然后紧接着值(其中，键名表示对象的属性，键值表示对象属性的值)：       
  
  {"firstName":"John"}     
  
  这很容易理解，等价于这条JavaScript语句：      
  
  {firstName = "John"}     

## JSON与JS对象的关系
  
  很多人搞不清楚JSON和JS对象的关系，甚至连谁是谁都不清楚。其实，可以这么理解：     
  
  JSON是JS对象的字符串表示法，它使用文本表示一个JS对象的信息，本质是一个字符串。     
  如：    
  >> var obj = {a:'Hello',b:'World'}; // 这是一个对象，注意键名也是可以使用引用包裹的    
  
  >> var json = '{"a":"Hello","b":"world"}'; //这是一个JSON字符串，本质是一个字符串    

## JSON和JS对象互转

要实现从对象转换为JSON字符串，使用JSON.stringify()方法:      

>> var json = JSON.stringify({a:'Hello',b:'World'}); //结果是'{"a":"Hello"}'     

要实现从JSON转换为对象，使用JSON.parse()方法：      

>> var obj = JSON.parse('{"a":"Hello","b":"World"}'); //结果是{a:'Hello',b:'World'}     

## 常用类型

  在JS语言中，一切都是对象。因此，任何支持的类型都可以通过JSON来表示，例如字符串、数字、对象、数组等。但是对象和数组是比较特殊且常用的两类类型。    

  对象：对象在 JS 中是使用花括号包裹 {} 起来的内容，数据结构为 {key1：value1, key2：value2, ...} 的键值对结构。在面向对象的语言中，key 为对象的属性，value 为对应的值。键名可以使用整数和字符串来表示。值的类型可以是任意类型。      

  数组：数组在 JS 中是方括号 [] 包裹起来的内容，数据结构为 ["java", "javascript", "vb", ...] 的索引结构。在 JS 中，数组是一种比较特殊的数据类型，它也可以像对象那样使用键值对，但还是索引使用得多。同样，值的类型可以是任意类型。    

## 基础示例

  简单地说，JSON可以将JavaScript对象中表示的一组数据转化为字符串，然后就可以在网络或者程序之间轻松地传递这个字符串，并在需要的时候将它还原为各编程语言所支持的数据格式，例如在PHP中，可以将JSON还原为数组或者一个基本对象。 在用到AJAX时，如果需要用到数组传值，这时就需要用JSON将数组转化为字符串。       

## 表示对象

  JSON最常用的格式是对象的 键值对。例如下面这样：  

  >> {"firstName":"Brett","lastName":"McLaughlin"}     

## 表示数组

  和普通的JS数组一样，JSON表示数组的方式也是使用方括号[].     

```
  {
   "people":[
      {
      "firstName":"Brett",
      "lastName":"McLaughlin"
      },

      {
      "firstName":"Jason",
      "lastName":"Hunter"
      }
   ]
  }

```

  这不难理解。在这个实例中，只有一个名为people的变量，值是包含两个条目组，每个条目是一个人的记录，其中包含名和性。上面的示例演示如何用括号将记录组合成一个值。当然，可以使用相同的语法表示更多的值     

  在处理JSON格式的数据时，没有需要遵守的预定的约束。所以，在同样的数据结构中，可以改变表示数据的方式，也可以使用不同方式表示同一事物。      

## JSON对象

### 对象语法

- 实例

>> { "name":"runoob", "alexa":10000, "site":null }   

JSON 对象使用在大括号({})中书写。    
对象可以包含多个 key/value（键/值）对。    
key 必须是字符串，value 可以是合法的 JSON 数据类型（字符串, 数字, 对象, 数组, 布尔值或 null）。    
key 和 value 中使用冒号(:)分割。    
每个 key/value 对使用逗号(,)分割。    

### 访问对象值

1. 你可以使用点号(.)来访问对象的值：     

例如：   

```
  var myObj,x;

  myObj = {"name":"runoob","alexa":10000,"site":null};

  x = myObj.name;

```

2. 你也可以使用中括号([])来访问对象的值：     

```
  var myObj,x;
  
  myObj = myObj = {"name":"runoob","alexa":10000,"site":null};

  x = myObj["name"];

```

3. 循环对象     

你可以使用for-in 来循环`对象的属性`：    

```
var myObj = {"name":"runoob","alexa":10000,"site":null};

for(x in myObj){
  document.getElementById("demo").innerHTML += x + "<br>";
}
```

在 for-in 循环对象的属性时，使用中括号([])来访问`属性的值`：     

```
  var myObj = {"name":"runoob","alexa":10000,"site":null};

  for(x in myObj){
    document.getElementById("demo").innerHTML += myObj[x] + "<br>";
  }
```

### 嵌套JSON对象

JSON对象中可以包含另一个JSON对象：      

```
 myObj = {
  "name":"runoob",
  "alexa":10000,
  "sites":{
    "site1":"www.runoob.com",
    "site2":"m.runoob.com",
    "site3":"c.runoob.com"
  }
 }
```

`你可以使用点号(.)或者中括号([])来访问嵌套的JSON对象`       

```
  x = myObj.sites.site1;  // www.runoob.com
    //或者
  x = myObj.sites["site1"]; // www.runoob.com

```

### 修改值

`1. 你可以使用点号(.)来修改JSON对象的值：`      

>> myObj.sites.site1 = "www.google.com";     

`2. 你可以使用括号([])来修改JSON对象：`      

>> myObj.sites["site1"] = "www.google.com";    

### 删除对象属性

我们可以使用delete关键字来删除JSON对象的属性：     

>> delete myObj.sites.site1;     

你也可以使用中括号([])来删除JSON对象的属性：     

>> delete myObj.sites["site1"]      

## JSON 数组

### 数组作为JSON对象

>> ["Google","Runoob","Taobao"]      

JavaScript中，数组值可以是以上的JSON数据类型，也可以是JavaScript的表达式，包括函数，日期，及undefined。    
### JSON对象的数组

对象属性的值可以是一个数组：      

```
var myObj,x;

myObj = {
    "name":"网站",
    "num":3,
    "sites":["Google","Runoob","Taobao"]
}

```

我们可以使用索引值来访问数组：      

>> x = myObj.sites[0];     

### 循环数组 

你可以使用for-in来访问数组：    

```
var myObj, i, x = "";
myObj = {
  "name":"网站",
  "num":3,
  "sites":[ "Google", "Runoob", "Taobao" ]
};

for(i in myObj.sites){
  x += myObj.sites[i] + "<br>"
}
```

### 嵌套JSON对象中的数组

JSON对象中数组可以包含另一个数组，或者另外一个JSON对象：     

```
myObj = {
  "name":"网站",
  "num":3,
  "sites":[
    {"name":"Google","info":["Android","Google 搜索","Google 翻译"]},
    {"name":"Runoob","info":["菜鸟教程","菜鸟工具","菜鸟微信"]}，
    {"name":"TaoBao","info":["淘宝","网购"]}
  ]
}

```

我们可以使用for-in来循环访问每个数组：   

```
for (i in myObj.sites){
  x += "<h1>"+ myObj.sites[i].name + "</h1>";
  for (j in myObj.sites[i].info){
    x += myObj.sites[i].info[j] + "<br>";
  }
}
```

### 修改数组值

你可以使用索引值来修改数组值：      

>> myObj.sites[1] = "Gitehub";

### 删除数组元素

我们可以使用delete 关键字来删除数组元素：     

>> delete myObj.sites[1];

## JSON.parse()

JSON通常用于与服务端交换数据。    

在接收服务器数据时一般是字符串。   

我们可以使用JSON.parse()方法将数据转化为JavaScript对象。    

### 语法

```
 JSON.parse(text[,reviver])
```

#### 参数说明：

- text必需，一个有效的JSON字符串。   

- reviver:可选，一个转换结果的函数，将为对象的每个成员调用此函数。    

### JSON 解析实例

例如我们从服务器接受了以下数据：  

>> {"name":"runoob","alexa":10000,"site":"www.runoob.com"}    

我们使用JSON.parse()方法处理以上数据，将其转换为JavaScript对象：     

>> var obj = JSON.parse('{"name":"runoob","alexa":10000,"alexa"}');    

解析前要确保你的数据是标准的JSON格式，否则会解析出错。     

解析完成后，我们可以在网页上使用JSON数据了：      

```
<p id="demo"></p>

<script>
var obj = JSON.parse('{ "name":"runoob", "alexa":10000, "site":"www.runoob.com" }');
document.getElementById("demo").innerHTML = obj.name + "：" + obj.site;
</script>
```

### 从服务端接收JSON数据

我们可以使用AJAX从服务器端请求JSON数据，并解析为JavaScript对象。     

```
var xmlhttp = AJAX XMLHttpRequest();
xmlhttp.onreadystatechange = function(){
  if(this.readyState == 4 && this.status == 200){
    myObj =  JSON.parse(this.responseText);
    document.getElementById("demo").innerHTML = myObj.name;
  }
};
xmlhttp.open("GET","/try/ajax/json_demo.txt",true);
xmlhttp.send();
```

### 从服务端接受数组的JSON数据

如果从服务端接收的是数组的JSON数据，则JSON.parse会将其转换为JavaScript数组：     

```
  var xmlhttp = new XMLHttpRequest();
  xmlhttp.onreadystatechange = function(){
    if(this.readyState == 4 && this.status ==200){
      myArr = JSON.parse(this.responseText);
      document.getElementById("demo").innerHTML = myArr[1];
    }
  };
  xmlhttp.open("GET","/try/ajax/json_demo_array.text",true);
  xmlhttp.send();
```

### 异常

#### 解析数据

JSON不能存储Date对象。    

如果你需要存储Date对象，需要将其转换为字符串。    

之后再将字符串转换为Date对象。    

```
 var text = '{"name":"Runoob","initDate":"2013-12-14","site":"www.runoob.com"}';
 var obj = JSON.parse(text);
 obj.initDate = new Date(obj.initDate);
 document.getElementById("demo").innerHTML = obj.name + "创建日期："+obj.initDate;

```

### 解析函数

JSON不允许包含函数，但你可以将函数作为字符串存储，之后再将字符串转换为函数。    

```
  var text = '{"name":"Runoob","alexa":"function(){return 10000;}","site":"wwww.runoob.com"}';
  var obj = JSON.parse(text);
  obj.alexa = eval("("+ obj.alexa + ")");
  document.getElementById("demo").innerHTML = obj.name + " Alexa 排名：" + obj.alexa();
```


## JSON.stringfy()

JSON通常用于与服务端交换数据。      

在向服务发送数据时一般是字符串。      

我们可以使用JSON.stringify()方法将JavaScript对象转换为字符串。      

### 语法

>> JSON.stringify(value[,replacer[,space]])       

#### 参数说明：

- value:    

  必需，一个有效的JSON字符串。      

- replacer:      

  可选。用于转换结果的函数或数组。        

  如果replacer为函数，则JSON.stringify将调用该函数，并传入每个成员的键和值。使用返回值而不是原始值。如果此函数返回undefined，则排除成员。根对象的键是一个空字符串：”“。如果replacer是一个数组，则仅转换该数组中具有键值的成员。成员的转换顺序与键在数组中的顺序一样。当value参数也为数组时，将忽略replacer数组。       

- space:    

  可选，文本添加缩进、空格和换行符，如果space是一个数字，则返回值文本在每一个级别缩进指定书目的空格，如果space大于10，则文本缩进10个空格。space有可以使用非数字，如：\t     

### JavaScript对象转换  

例如我们向服务器发送一下数据：      

>> var obj = {”name“:"runoob","alexa":10000,"site":"www.runoob.com"};   

我们使用JSON.stringify()方法处理以上数据，将其转化为字符串：       

>> var myJSON = JSON.stringify(obj);      

myJSON 为字符串。    

我们可以将 myJSON 发送到服务器：     

```
  var obj = {"name":"runoob","alexa":10000,"site":"wwww.runoob.com"};
  var myJSON = JSON.stringify(obj);
  document.getElementById("demo").innerHTML = myJSON;

```

### JavaScript数组转换

我们也可以将JavaScript数组转换为JSON字符串：      

```
  var arr = ["Google","Runoob","Taobao","Facebook"];
  var myJSON = JSON.stringify(arr);
```

myJSON 为字符串。    

我们可以将myJSON 发送到服务器：     

```
  var arr = ["Google","Runoob","Taobao","facebook"];
  var myJSON = JSON.stringify(arr);
  document.getElementById("demo").innerHTML = myJSON;
```


### 异常

#### 解析数据

JSON不能存储Date对象。      

JSON.stringify()会将所有日期转换为字符串。      

```
  var obj = {"name":"Runoob","initDate":new Date(),"site":"www.runoob.com"};
  var myJSON = JSON.stringify(obj);
  document.getElementById("demo").innerHTML = myJSON;


```


之后你可以再将字符串转换为Date对象。      

### 解析函数

JSON不允许包含函数，JSON.stringify()会删除JavaScript对象的函数，包括 key 和 value.   

```
  var obj = {"name":"Runoob","alexa":function(){return 10000;},"site":"www.runoob.com"};

  var myJSON = JSON.stringify(obj);
  document.getElementById("demo").innerHTML = myJSON;

```


我们可以在执行JSON.stringify()函数前将函数转换为字符串来避免以上问题的发生：       

```
  var obj = {"name":"Runoob","alexa":function(){return 10000;},"site":"www.runoob.com"};
  obj.alexa = obj.alexa.toString();
  var myJSON = JSON.stringify(obj);
  document.getElementById("demo").innerHTML = myJSON;
```

不建议在JSON中使用函数。       

## JSON使用

### 把 JSON 文本转换为JavaScript对象 

JSON最常见的用法之一，是从web服务器上读取JSON数据(作为文件或作为HttpRequest),将JSON数据转化为JavaScript对象，然后在网页中使用该数据。     

为了更简单地为您讲解，我们使用字符串作为输入进行演示(而不是文件)   

### JSON实例 - 来自字符串的对象

创建包含JSON语法的JavaScript字符串：     

```
  var txt = '{ "sites" : [' +
  '{ "name":"菜鸟教程" , "url":"www.runoob.com" },' +
  '{ "name":"google" , "url":"www.google.com" },' +
  '{ "name":"微博" , "url":"www.weibo.com" } ]}';
```

由于JSON语法是JavaScript语法的子集，JavaScript函数eval()可用于将JSON文本转换为JavaScript对象。      
eval()函数使用的是JavaScript编译器，可解析JSON文本，然后生成JavaScript对象。必须把文本包含在括号中，这样才能避免语法错误：     

>> var obj = eval("("+ txt +")");     

在网页中使用JavaScript对象：      

```
  var txt = '{ "sites" : [' +
  '{ "name":"菜鸟教程" , "url":"www.runoob.com" },' +
  '{ "name":"google" , "url":"www.google.com" },' +
  '{ "name":"微博" , "url":"www.weibo.com" } ]}';
 
  var obj = eval ("(" + txt + ")");
   
  document.getElementById("name").innerHTML=obj.sites[0].name 
  document.getElementById("url").innerHTML=obj.sites[0].url

```

### JSON解析器

eval() 函数可编译并执行任何 JavaScript 代码。这隐藏了一个潜在的安全问题。
使用 JSON 解析器将 JSON 转换为 JavaScript 对象是更安全的做法。JSON 解析器只能识别 JSON 文本，而不会编译脚本。
在浏览器中，这提供了原生的 JSON 支持，而且 JSON 解析器的速度更快。

