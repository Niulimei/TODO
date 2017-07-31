# FormData 对象的使用

>> 通过FormData对象可以组装一组用 `XMLHttpRequest`发送请求的键/值对。它可以更灵活方便的发送表单数据，因为可以独立于表单使用。如果你把表单的编码类型设置为multipart/form-data,则通过FormData传输的数据格式和表单通过`submit()`方法传输的数据格式相同     

## 如何创建一个FormData对象

你可以自己创建一个FormData对象，然后通过调用它的`append()`方法添加字段，就这样：     

```
  var formData = new FormData();
  formData.append("username",Groucho);
  formData.append("accountnum",123456);//数字 123456 会被立即转化成字符串"123456"

  //HTML 文件类型input,由用户选择
  formData.append("userfile",fileInputElement.files[0]);

  //JavaScript file-like 对象
  var content = '<a id="a"><b id="b">hey!</b></a>';//新文件的正文...
  var blob = new Blob([content],{type:"text/xml"});

  formData.append("webmasterfile",blob);

  var request = new XMLHttpRequest();
  request.open("POST","http://foo.com/submitform.php");
  request.send(formData); 


```

> `注意：`字段 ”userfile“和"webmasterfile"都包含一个文件.字段”accountnum“是数字类型，它将被FormData.append()方法转换成字符串类型(FormData 对象的字段类型可以是Blob,File,或者 string:如果它的字段类型不是Blob也不是File,则会被转换成字符串类型。)      

上面的实例创建了一个FormData实例，包含”username“,"accountnum","webmasterfile"四个字段，然后使用XMLHttpRequest的send()方法发送表单数据。字段”webmasterfile“是Blob类型。 一个Blob对象表示一个不可变的，原始数据的类似文件对象。Blob表示的数据不一定是一个JavaScript原生格式。File接口基于Blob，继承blob功能并将其扩展为支持用户系统上的文件。你可以通过Blob()构造函数创建一个Blob对象。     

## 通过HTML表单创建FormData对象

想要构造一个包含Form表单数据的FormData对象，需要在创建FormData对象时指定表单的元素。    

> var formData = new FormData(someFormElement);    

- 示例：   

```
  var formElement = document.querySelector("form");
  var request = new XMLHttpRequest();
  request.open("POST","submitform.php");
  request.send(new FormData(formElement));
```

你可以在创建一个包含Form表单数据的FormData对象之后和发送请求之前，附加额外的数据到FormData对象里，像这样：    

```
  var formElement = document.querySelector("form");
  var formData = new FormData(formElement);
  var request = new XMLHttpRequest();
  request.open("POST","submitform.php");
  formData.append("serialnumber",serialNumber++);
  request.send(formData);

```

这样你就可以在发送请求之前自由的附加不一定是用户编辑的字段到表单数据里      

## 使用FormData对象上传文件

你还可以使用FormData上传文件。使用的时候需要在表单中添加一个文件类型的input：      

```
  <form enctype="multipart/form-data" method="post" name="fileinfo">
    <label>Your email address:</label>
    <input type="email" autocomplate="on" autofocus name="userid" placeholder="email" required size="32" maxlength="64" /><br />
    <label>Custom file label:</label>
    <input type="text" name="filelabel" size="12" maxlength="32" /><br />
    <label>File to stash:</label>
    <input type="file" name="file" required />
    <input type="submit" value="Stash the file!" />
  </form>
  <div></div>
```

然后使用下面的代码发送请求：     

```
  var form = document.forms.namedItem("fileinfo");
  form.addEventListener('submit',function(ev){
    var oOutput = document.querySelector("div"),
    oData = new FormData(form);
    oData.append("CustomField","This is some extra data");
    var oReq.open("POST","stash.php",true);
    oReq.onload = function(oEvent){
      if(oReq.status == 200){
        oOutput.innerHTML = "Uploaded!";
      }else {
        oOutput.innerHTML = "Error" + oReq.status + "occurred when trying to upload your file.<br \/>";
      }
    };
    oReq.send(oData);
    ev.preventDefault();
  },false);

```

> `注意：`如果FormData对象是通过表单创建的，则表单中指定的请求方式会被应用到方法open()中。    

你还可以直接向FormData对象附加File或Blob类型的文件，如下所示：      

> data.append("myfile",myBlob,"filename.txt");    

使用的append()方法时，可以通过第三个可选参数设置发送请求的头 Content-Disposition 指定文件。如果不指定文件名(或者不支持该参数时)，将使用名字”blob“。     

如果你设置正确的配置项，你也可以通过jQuery来使用FormData对象：     

```
  var fd = new FormData(document.querySelector("form"));
  fd.append("CustomField","This is some extra data");
  $.ajax({
    url:"stash.php",
    type:"POST",
    data:fd,
    processData:false,  //不处理数据
    contentType:false   //不设置内容类型
  });
```

## 通过AJAX提交表单和上传文件可以不使用FormData对象



## 简单的实例和使用方法

### 概述理解

FormData类型其实是在XMLHttpRequest2级定义的，它是为序列化表以及创建与表单格式相同的数据(当然是用于XHR传输)提供便利。    
### 构造函数

创建一个formData对象实例有几种方式

1. 创建一个`空对象`实例    

```
 var formData = new FormData();
```

此时可以调用append()方法来添加数据     

2. 使用已有的表单来初始化一个对象实例     

假如现在页面已经有一个表单     

```
  <form id="myForm" action="" method="post">
    <input type="text" name="name">名字
    <input type="password" name="psw">密码
    <input type="submit" value="提交">
  </form>

```

我们可以使用这个表单元素作为初始化参数，来实例化一fromData对象     

```
  //获取页面已有的一个form表单
  var form = documnent.getElementById("myForm");
  //用表单来初始化
  var formData = new FormData(form);
  //我们可以根据name来访问表单中的字段
  var name = formData.get("name"); //获取名字
  var psw = formData.get(psw); //获取密码
  //当然也可以在此基础上，添加其他数据
  formData.append("token","kshdeojdkjkd");

```

3. 操作方法    

***

首先，我们要明确formData里面存储的数据形式，一对key/value组成一条数据，key是唯一的，一个key可能对应多个value。如果是使用表单初始化，每个表单字段对应一条数据，它们的HTML name属性即为key值。      

| key | value|
|:----|:-----|
|  k1 |[v1,v2,v3]|
|  k2 |  v4  |

***

#### 3.1 获取值

我们可以通过get(key)/getAll(key)来获取对应的value,     

```
  formData.get("name"); //获取key为name的第一个值
  formData.get("name"); //返回一个数组，获取key为name的所有值   
```

#### 3.2 添加数据

我们可以通过append(key,value)来添加数据，如果指定的key不存在则会新增一条数据，如果key存在，则会添加到数据的末尾    

```
formData.append("k1","v1");
formData.append("k1","v2");
formData.append("k1","v1");

formData.get("k1"); //"v1"
formData.getAll("k1"); //["v1","v2","v1"]

```

#### 3.3设置修改数据

我们可以通过set(key,value)来设置修改数据，如果指定的key不存在则会新增一条，如果存在，则会修改对应的value值。     

```
  formData.append("k1","v1");
  formData.set("k1","1");
  formData.getAll("k1"); //["1"]
```

#### 3.4判断是否该数据

我们可以通过has(key)来判断是否对应的key值    

```
 formData.append("k1","v1");
 formData.append("k2",null);
 formData.has("k1");//true
 formData.has("k2");//true
 formData.has("k3");//false
```

#### 3.5删除数据

通过delete(key),来删除数据     

```
formData.append("k1","v1");
formData.append("k1","v2");
formData.append("k1","v2");
formData.delete("k1");

formData.getAll("k1");//[]

```

#### 3.6遍历

我们可以通过entries()来获取一个迭代器，然后遍历所有的数据，     

```
formData.append("k1","v1");
formData.append("k1","v2");
formDara.append("k2","v1");

var i = formData.entries();

i.next(); //{done:false,value:["k1","v1"]}
i.next(); //{done:false,value["k1","v2"]}
i.next(); //{done:false,value["k2","v1"]}
i.next(); //{done:value,value:undefined}

```

可以看到返回迭代器的规则     

  1. 每调用一次next()返回一条数据，数据的顺序由添加的顺序决定     

  2. 返回的是一个对象，当其done属性为true时，说明已经遍历完所有的数据，这个也可以作为判断的依据      

  3. 返回的对象的value属性以数组形式存储了一对key/value,数组下标0为key,下标1为value,如果一个key值对应多个value，会变成多个key/value返回      

我们也可以通过values()方法只获取value值    

```
formData.append("k1","v1");
formData.append("k1","v2");
formData.append("k2","v1");

var i = formData.entries();

i.next(); //{done:false,value:"v1"}
i.next(); //{done:false,value:"v2"}
i.next(); //{done:false,value:"v1"}
i.next(); //{done:true,value:undefined}

```

#### 4.发送数据

我们可以通过xhr来发送数据   

```
var xhr = new XMLHttpRequest();
xhr.open("post","login");
xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xhr.send(formData);
```

这种方式可以实现文件的异步上传。      

[参考文献1](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData/Using_FormData_Objects)   

[参考文献2](https://segmentfault.com/a/1190000006716454)
