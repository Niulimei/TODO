# apply()

## 常用作用就是将一个数组转化为一个接一个的参数，因为好多方法中的参数不接受数组

apply 中文意思就是`应用、运用` 所以，apply()方法就是用来改变或者 运用 某些执行环境。比如：找数组中的最小值，但数组中并没有min这个方法，但是Math对象可以求最小值，因为Math对象中有min这个方法。      

如： var a = Math.min(3,2,1,4),这时候a将赋值为1.      

一个数组想要使用Math对象的min方法，就要使用call/apply来改变执行环境了。     

Math.min(3,2,1,4)<====>Math.min.apply(null,[3,2,1,4]),null 是上下文，传入的对象对应函数中的this，min函数并没有使用this,因此这里可以为null,[3,2,1,4]是给min函数的参数列表。    

```
var A={
  a:1
}
A.add = function(b){
  console.log(this.a+b);
}
A.add(3);//=>4
var  B={
  a:4
}

A.add.apply(B,[3]);// ==>7,add函数中的this换成了B
```

```
Function.apply(obj,args)方法能接受两个参数   
obj:这个对
```



# call()

```
function add (a,b)
{
alter(a+b);
}
function sub(a,b){
  alter(a-b);
}
add.call(sub,3,1);

这个例子中的意思就是用 add来替换sub,add.call(sub,3,1)==add(3,1),所以运行的结果为：alter(4)；




function Animal(){
  this.name = "Animal";
  this.showName = function(){
  alert(this.name);
  }
}

function Cat(){
  this.name = "Cat";
}
var animal = new Animal();
var cat = new Cat();
//通过call 或 apply方法，将原本属于Animal对象的showName()方法交给对象cat来使用了。
//输入结果为"Cat"
animal.showName.call(cat,",");
//animal.showName.apply(cat,[]);

注意：call和apply的区别在于call()接受一个参数列表，同时apply()接受一个参数数组。

call的意思是把animal的方法放到cat上执行，原来cat是没有showName()方法，现在是把animal的showName()方法放到cat上来执行，所以this.name应该是Cat



3. 实现继承

function Animal(name){
  this.name = name;
  this.showName = function(){
  alert(this.name);
  }
}

function Cat(name){
  Animal.call(this,name);
}
var cat = new Cat("Black Cat");
cat.showName();

//Animal.call(this)的意思就是使用Animal对象代替this对象，那么Cat中你就有Animal的所有属性和方法了吗，Cat对象就能够直接调用Animal的方法以及属性了
```

` Function.apply(obj,args)方法接受两个参数`        

obj:这个对象将代替Function类里this对象      
args：这个数组，它将作为参数传给FUnction(args->arguments)

```
function Person(name,age){   //定义一个类，人类
  this.name=name;
  this.age=age;
  this.sayhello=function(){alert("hello")};
}
function Print(){  //显示类的属性
  this.funcName="Print";
  this.show=function(){
  var msg=[];
  for(var key in this){
  if(typeof(this[key])!="function"){
  msg.push([key,":",this[key]].join(""));
  }
  }
  alert(msg.join(""));
  };
}

function Student(name,age,grade,school){   //学生类
  Person.apply(this,arguments);  //自我理解：Person类的所有属性和方法被运用到当前(this)函数中;arguments是一个数组，指的就是[name,age,grade,school];apply方法可以自动将数组转化为(name,age,grade,school)
  Print.apply(this,arguments);//Print方法中的show（）被运用到当前方法中
  this.grade=grade;
  this.school=school;
}

var p1 =new Person("jake",10);
p1.sayhello();
var s1 =new Student("tom",13,6,"清华小学");
s1.show();
s2.sayhello();
alert(s1.funcName);


//学生本来不具备任何方法，但是在Person.apply(this.arguments)后，他就具备了Person类的sayhello方法和所有属性。

Print.apply(this,arguments)后就自动得到了show()方法


```

## 利用Apply的参数数组化来提高

Function.apply()在提升性能方面的技巧     

我们先从Math.max()函数说起，Math.max后面可以接任意个参数，最后返回所有参数中的最大值。     

比如    

alert(Math.max(5,8))//8      
alert(Math.max(5,7,3,1,6)) //9   
但是在很多情况下，我们需要找出数组中最大的元素。

```
var arr=[5,7,9,1]

alert(Math.max(arr))  //这样写是不行的，

function getMax(arr){
  var arrLen=arr.length;
  for(var i=0,ret=arr[0];i<arrLen;i++){
  ret=Math.max(ret,arr[i]);
  }
  return ret;
}


//上面的写法麻烦而且低效。如果用apply呢，代码如下：

function getMax2(arr){
  return Math.max.apply(null,arr);
}


//两段代码达到了同样的目的，但是getMax2却优雅，高效，简介的多。


再比如：

var arr1=[1,3,4];
var arr2=[3,4,5];

//如果我们要把arr2展开，然后一个一个追加到arr1中去，最后arr1=[1,3,4,3,4,5]
arr1.push(arr2)显然是不行的。因为这样做会得到[1,3,4,[3,4,5]]



//我们只能用一个循环去一个一个的push(当然也可以用arr1.concat(arr2),但是concat方法并不改变arr1本身)
var arrLen = arr2.length
for(var i =0;i<arrLen;i++){
  arr1.push(arr2[i]);
}


//使用Apply事情就变得简单了
Array.prototype.push.apply(arr1,arr2);







```

## apply的一些妙用

1. Apply有一个巧妙地用处，可以将一个数组默认的转化为一个参数列表([param1,param2,param3]转化为 param1,param2,param3)    

2. Matn.max 可以实现得到数组中最大的一项     

因为Math.max参数里面不支持Math.max([param1,param2]) 也就是不支持数组，但是它支持Math.max(param1,param2,param3...),所以根据上面的妙用  1 来解释 var max=Math.max.apply(null,array),这样就得到数组中最大的一项。       

`(apply会将一个数组转化为一个参数接一个参数的传递给方法)`     

这块在调用的时候第一个参数给了一个null，这个是因为没有对象去调用这个方法，我们只需要用这个方法帮我运算，得到返回的结果就行，所以直接传递了一个null过去      

同理，Math.min 可以实现得到数组中的最小的一项：var min=Math.min.apply(null,array);       

3. Array.prototype.push可以实现两个数组合并    

同样push方法没有提供push一个数组，但是它提供了push(param1,param2,...paramN)所以通过apply来转换一下这个数组，即：       

vararr=new Array("1","2","3");    

vararr2=new Array("4","5","6");    

Array.prototype.push.apply(arr1,arr2);



