# JS开发中。如何减少 if else语句的使用

  由于if-else的往往嵌套导致代码不美观，所以可以进行简化美观   

  代码整洁强迫症必须要来一个抛砖引玉：    

  1. 

```
  if(a为真){
    a=a
  }else{
    a=b
  }


  可以写成： a = a || b 

```
 
 2. 

 ```
 if(a==b){
   a=c
 }else{
   a=d
 }


 可以写成: a = (a==b)?c:d



 ```


 3. 后天接口常常会返回这种数据：     

    fruit:0// 0=苹果，1=梨子， 2=橘子， 3=柠檬, 4=芒果...    

    这时候写if-else是很痛苦的事，不妨使用这个方法：


```
    var _f = ['苹果','梨子','橘子','芒果'];

    shuiguo = _f[fruit];
  
```

### 建议：

### 第一步：优化if逻辑

   人们考虑东西的时候  ，都会把最可能发生的情况先做好准备。优化if逻辑的时候也可以这样想：
   把最可能出现的条件放在前面，把不可能出现的条件放后面，这样程序执行时总会按照名字的先后顺序逐一检测所有的条件，直到发现匹配的条件才会停止继续检测。      

   if的优化目标：最小化找到分支之前所判断条件体的数量。if优化的方法：将最常见的条件放在首位。     
   ```
    if(i<5){
     //执行一些代码
    }else if(i>5&&i<10){
     //执行一些代码
    }else{
    //执行一些代码
    }
   ```

   例如上面的例子，只有在i值经常出现小于5的时候是最优化。如果i值经常大于或者等于10的话，那么在进入正确的分支之前，就必须两次运算条件体，导致表达式的平均运算时间增加。if中的条件体应该总是按照从最大化概率到最小概率排列，以保证理论速度最快。      

### 第二步：尽量少使用else

  如果在函数中，可以使用 if + return,先判断错误条件，然后立马结束函数，防止进入 else分支。  

  举个简单的例子，后端返回数据，前端根据状态进行不同操作    

  ```
  $.ajax().done(function(res){
   if(res.state === 'SUCCESS'){
    //TODO
   }else if(res.state === 'FAIL'){
     //TODO
   }else{
     //TODO
   }
  });
  ```

   这里的if else不是挺好的么，有什么问题？不过更倾向于 switch     
   解决方法：

  1. switch/case    

   switch和if else 在性能上是没有什么区别的，主要还是根据需求进行分析和选择。    

- 如果条件较小的话选择 if else 比较合适。
- 相反，条件数量较大的话，就建议选用switch.

一般来说， if else 适用于两个离散的值或者不同的值域。如果判断多个离散的值，适用switch比较合适。     

在大多数的情况下switch 比if else运行的更快。    

在大多数的情况下，switch的性能不会比if else 低。switch的确在实质上跟 if else if完全一样的效果，不过在很多情况下，使用switch要比 if else 方便不少      

比如经典的值等分支，匹配一些状态常量的时候，比 if else 结构方便许多，不会反复写 xx==yy

```
$.ajax().done(function(res){
  switch(res.state){
   case:'SUCCESS':
   //TODO
   break;
   case:'FAIL':
   //TODO
   break;
   default:
   //TODO 
  }
});
```

注意：千万不要忘记在每一个case语句后面放一个break语句。也可以放一个return或者throw.   

case语句匹配expression是用 ===而不是 ==


2. hash表

```
  if(key=="Apple"){
    val = "Jobs";
  }else if(key=="microsoft"){
    val = "Gates";
  }else if(key == "Google"){
    val = "Larry";
  }

```

  这个也可以用 switch case解决，不过推荐的方法是hash表   

  ```
   var ceos = {"Apple":"Jobs","microsoft":"Gates","Google":"Larry"};
   val = ceos[key];
  ```

  3. 重构，用OO里边的继承或者组合

  ```
  1. 如果是狗，则汪汪
  2. 如果是猫，则喵喵
  3. 如果是鸭，则嘎嘎
  ```
  可以重构一下，改成OO

  ```
  *定义类：动物（或者接口）
  *定义方法：叫
  *定义子类：狗、猫、鸭
  *重写方法  ----叫
  ```

也就是说将同类的判断按照功能，写成函数，这样也便于阅读   
比如我有一个方法根据类型获取名称，用if else会这样

 ```
  function getName(type){
   if(type == 'monkey'){
    return 'monkey name';
   }else if(cat name){
    return 'cat name';
   }else{
   return 'dog name';
   }
  }
 ```

 如果写成函数，改写下面的会更好
```
 function getName(type){
   var data = {
    monkey: 'monkey name',
    cat: 'cat name',
    dag:'dog name'
   }
   return data[type]?data[type]:data['dag'];
 }
```

硬要把设计模式添加到JS里不是不可以，但要看情况，生搬硬套过来的东西并没有什么卵用。     


## 补充 哈希表知识点

- 若关键字为k，则其值存放在f(k)的位置上。因此，不需要比较便可以直接取得所有记录。称这个对应关系f为散列函数，按这个思想建立的表为散列表。

- 



