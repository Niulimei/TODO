# Object

## object.assign()方法用于将所有可枚举的属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。       

### 语法

>> Object.assign(target,...sources)      

### 参数

target 目标对象。     

sources  （多个）源对象。     

### 返回值

目标对象。     

### 描述

如果目标对象中的属性具有相同的键，则属性将被源中的属性覆盖。后来的源属性将类似地覆盖早先的属性。      

object.assign方法只会拷贝源对象自身的并且可枚举的属性到目标对象身上。该方法使用元对象的[[Get]]和目标对象的[[Set]],所以它会调用相关getter和setter。因此，它分配属性而不是复制或定义新的属性。如果合并包含了getter，那么该方法就不适合将新属性合并到原型里。假如是拷贝属性定义到原型里，包括它们的可枚举性，那么应该使用Object.getOwnPropertyDescriptor()和Object.defineProperty()。      

String类型和Symbol类型的属性都会被拷贝。      


注意，在属性拷贝过程中可能会产生异常，比如目标对象的某个只读属性和对象的某个属性同名，这时该方法会抛出一个TypeError异常，拷贝过程中断，已经拷贝成功的属性不会受到影响，还未拷贝的属性将不会再被拷贝。      

注意，Object.assign会跳过哪些值为null或undefined的源对象。       

### 示例

复制一个object      

```
  var obj = {a:1};
  var copy = Object.assign({},obj);
  console.log(copy); //{a:1}
```

### 深度拷贝问题

针对深度拷贝，需要使用其他方法，因为Object.assign()拷贝的是属性值。假如源对象的属性值是一个指向对象的引用，它也只拷贝那个引用值。      

```
function test() {
  let a = { b: {c:4} , d: { e: {f:1}} }
  let g = Object.assign({},a)
  let h = JSON.parse(JSON.stringify(a));
  console.log(g.d) // { e: { f: 1 } }
  g.d.e = 32
  console.log('g.d.e set to 32.') // g.d.e set to 32.
  console.log(g) // { b: { c: 4 }, d: { e: 32 } }
  console.log(a) // { b: { c: 4 }, d: { e: 32 } }
  console.log(h) // { b: { c: 4 }, d: { e: { f: 1 } } }
  h.d.e = 54
  console.log('h.d.e set to 54.') // h.d.e set to 54.
  console.log(g) // { b: { c: 4 }, d: { e: 32 } }
  console.log(a) // { b: { c: 4 }, d: { e: 32 } }
  console.log(h) // { b: { c: 4 }, d: { e: 54 } }
}
test();
```


### 合并objects

```
  var o1 = { a: 1};
  var o2 = { b: 2};
  var o3 = { c: 3};

  var obj = Object.assign(o1,o2,o3);
  console.log(obj);//{a:1,b:2,c:3}
  console.log(o1);//{a:1,b:2,c:3}，注意，目标对象自身也会改变。
```


### 拷贝 symbol类型的属性

```
  var o1 = {a:1};
  var o2 = {[Symbol("foo")]:2};

  var obj = Object.assign({},o1,o2);
  console.log(obj);//{a:1,[Symbol("foo")]:2}

```

### 继承属性和不可枚举属性是不能拷贝的

```
  var obj = Object.create({foo:1},{  //foo是个继承属性
      bar:{
        value:2 //bar 是个不可枚举属性。
      },
      baz:{
        value:3,
        enumerable:true //baz 是个自身可枚举属性。
      }
  })

  var copy = Object.assign({},obj);
  console.log(copy);//{baz:3}
```

### 拷贝访问器(accessor)

```
  var obj = {
    foo:1,
    get bar(){
      return 2;
    }
  };

  var copy = Object.assign({},obj);
  // {foo:1,bar:2}
  // copy.bar的值来自obj.bar的getter函数的返回值
  console.log(copy);

  // 下面这个函数会拷贝所有自有属性的属性描述符
    function completeAssign(target, ...sources) {
      sources.forEach(source => {
      let descriptors = Object.keys(source).reduce((descriptors, key) => {
        descriptors[key] = Object.getOwnPropertyDescriptor(source, key);
        return descriptors;
      }, {});

      // Object.assign 默认也会拷贝可枚举的Symbols
      Object.getOwnPropertySymbols(source).forEach(sym => {
        let descriptor = Object.getOwnPropertyDescriptor(source, sym);
        if (descriptor.enumerable) {
          descriptors[sym] = descriptor;
        }
      });
      Object.defineProperties(target, descriptors);
    });
    return target;
  }

    var copy = completeAssign({}, obj);
    // { foo:1, get bar() { return 2 } }
    console.log(copy);
```

