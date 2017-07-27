# 浅谈 Web API 接口之 Blob

>一个Blob对象表示一个不可变的，原始数据的类似文件对象。Blob表示的数据不一定是JavaScript原生格式。`File`接口基于Blob，继承blob功能并将其扩展为支持用户系统上的文件。     

***

要从其他非blob对象和数据构造一个Blob，请使用`Blob()`构造函数。要创建一个包含另一个blob的数据子集的blob，使用`slice()`方法。要从用户文件系统上的一个文件中获取一个Blob对象，请参阅 [File](https://developer.mozilla.org/zh-CN/docs/Web/API/File)文档。     

接受Blob对象的APIs也被列在File文档中。     

>注：slice()一开始的时候接受length作为第二个参数，以表示复制到新的Blob对象的字节数。如果设置其为start+length,超出了源Blob对象的大小，那返回的Blob则是整个源Blob的数据。      

> 注：请注意，slice() 方法在某些浏览器和版本上仍带有供应商前缀：比如 Firefox 12及更早版本的blob.mozSlice() 和Safari中的blob.webkitSlice()。 slice() 方法的旧版本，没有供应商前缀，具有不同的语义，并且已过时。 使用Firefox 30 删除了对 blob.mozSlice() 的支持。     

## 构造函数

[Blob()](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob/Blob)     
返回一个新创建的Blob对象，其内容由参数中给定数组串联组成。     

## 属性

- Blob.isClosed `只读`       

布尔值，指示Blob.close()是否在该对象上调用过。关闭的blob对象不可读。    

- Blob.size `只读`     

Blob对象中所包含数据的大小(字节)。    

- Blob.type `只读`    

一个字符串，表明该Blob对象所包含数据的MIME类型。如果类型未知，则该值为空字符串。    

## 方法

- Blob.close()      

关闭Blob对象，以便能释放底层资源。     

- Blob.slice()   

返回一个新的Blob对象，包含了源Blob对象中指定范围内的数据。      

## 示例

`Blob构造函数用法举例`       

Blob()构造函数允许用其它对象创建一个Blob对象。比如，用字符转构建以blob：    

```
  var debug = {hello:"world"};
  var blob = new Blob([JSON.stringfy(debug,null,2)],
  {type:'application/json'});
```

> `BlobBuilder`接口提供了另一个创建Blob对象的方法，但该方法现在已经废弃，所以已经不应该再使用了：     

>>  var builder = new BlobBuilder();      
>>  var fileParts = ['<a id="a"><b id="b">hey!</b></a>'];      
>>  builder.append(fileParts[0]);     
>>  var myBlob = builder.getBlob('text/xml');

### 使用类型数组和Blob创建一个URL

> var typedArray = GetTheTypeArraySomehow();    
// 传入一个合适的MIME类型     
var blob= new Blob([typeedArray],{type:"application/octet-binary"});    
// 会产生一个类似blob：d3958f5c-0777-0845-9dcf-2cb28783acaf 这样的URL字符串    
// 你可以像使用一个普通URL那样使用它，比如用在img.src上。   
  var url = URL.createObjectURL(blob);    

## 从Blob中提取数据

从Blob中读取内容的唯一方法是使用 `FileReader`。以下代码将Blob的内容作为类型数组读取：     

```
  var render = new FileReader();
  reader.addEventListener("loadend",function(){
    // reader.result contains the content of blob as a typed array
  });
  reader.readAsArrayBuffer(blob);
```

使用 FileReader 以外的方法读取到的内容可能会是字符串或者数据URL。     

[参考文献](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)    





