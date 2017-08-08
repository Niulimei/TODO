# HTML DOM setInterval() 方法与clearInterval() 

## 定义和用法

setInterval()方法可按照指定的周期(以毫秒计)来调用函数或计算表达式。      

setInterval()方法会不停地调用函数，直到 clearInterval()被调用函数或计算表达式。由setInterval()返回的ID值可作 clearInterval()方法的参数。       

### 语法

>> setInterval(code,millisec[,"lang"])

`code`是一个函数，是必须的，要调用的函数或要执行的代码串。    

`millisec` 必须的，周期性执行或调用 `code` 之间的时间间隔，以毫秒计。     

```
   componentDidMount() {
    let time = 5;
    this.timer = setInterval(() => {
      if (time <= 0) {
        this.timer && clearInterval(this.timer)
        this.setState({ time: 0 })
        this.props.history.push('/customer')  //时间为0的时候调到 customer 页面
      } else {
        time--;
        this.setState({ time });
      }
    }, 1000);
  }

  componentWillUnmount() {
    clearInterval(this.timer);
  }
```

`注意:` this.timer 表示在整个函数中都可以调用，可以看做是全局的变量，不然，如果只是timer的话只能在componentDidMount函数内使用，而无法在componentWillUnmount中使用。     

## clearInterval() 

clearInterval() 方法可取消由 setInterval() 设置的 timeout。      

clearInterval() 方法的参数必须是由 setInterval() 返回的 ID 值。      