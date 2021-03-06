# ES6学习

## 令你蒙逼的ES6语法

虽然ES6很多语法令你蒙逼的语法,但是相对之前的JS是有改进的

觉得不错的改进

1. let

    传统的`var`存在变量提升的作用,例如在if里执行`var`代码,其实其作用域是和if同级别的,而非if的下一级别,这个原因是因为JS本身没有块级作用域
    
    而在if里声明`let`,这样let变量会存在if作用域内.
2. const: 该变量为常量.
3. `...`拷贝数组: const copy_array = [...array];
4. `Array.from`: 将类似数组的对象转化为数组

    ```javascript
    const foo = document.querySelectorAll('.foo');
    const nodes = Array.from(foo);
    ```
5. `箭头函数`: 主要函数绑定了`this`

   ```javascript
  //第一个x代表参数,后面`x*x`表示返回的结果.
  [1,2,3].map(x =>x * x) ;
  
  //旧写法
  const self =this;
  const boundMethod = function(...params) {
      return method.apply(self,params);
  }
  //新写法
  const boundMethod = (...params) => method.apply(this,params);
  ```
6. `class代替prototype`: 

    ```javascript
    //旧写法
    function Queue (contents = [] ) {
      this._queue = [...contents];
    }
    Queue.prototype.pop = function () {
      const value = this._queue[0];
      this._queue.splice(0.1);
      return value; 
    }
    
    //新写法
    class Queue {
      constructor(contents = []) {
        this._queue = [...contents];
      }
      
      pop() {
          const value = this._queue[0];
          this._queue.splice(0,1);
          return value;
      }
    }
    ```
7. `extends`实现继承

    ```javascript
    //旧写法
    const inherts = require('inherits');
    function PeekbleQueue(contents) {
        Queue.apply(this,contents);
    }
    innherits(PeekableQueue,Queue);
    PeekableQueue.prototype.peek = function() {
      return this._queue[0];
    }
    
    //新写法
    class PeekableQueue extends Queue {
      peek() {
        return this._queue[0];
      }
    }
    ```
8. `Module`模块写法

    ```javascript
    //旧写法
    const moduleA =require('ModuleA');
    const func1 = moduleA.func1;
    const func2 = modulea.func2;
    
    //新写法
    import {func1,func2} from 'ModuleA';
    ```
    
    export取代module.exports
    
    ```javascript
    var React = require('react');
    
    var Breadcrumbs = React.createClass({
      render() {
        return <nav />;
      }
    });
    
    module.exports = Breadcrumbs;
    
    //ES6写法
    import React from 'react';
    
    const Breadcrmbs = React.createClass({
        render () {
          return <nav />;
        }
    });
    //当模块只有一个输出值的时候使用export default
    //而是使用export
    //主要export default 与export同时使用
    export default Breadcrmbs;
    
    ```
9. `Object.assign`: Object.assign(target, ...sources),可以将来自一个或多个源对象,复制到一个目标对象

   ```javascript
   //下来就是把todo,添加一个text属性给一个空对象
   Object.assign({}, todo, { text: action.text })
   ```

令我蛋疼的改进

1. 反引号: 动态字符串可使用`${}`获取变量 eg: let k = `a${b}c`
2. 解构赋值: 可以解构数组/对象

    ```javascript
    //数组解构
    const arr = [1,2,3,4];
    const [first,second] = arr; //first=1,second=2
    
    //对象解构
    //旧写法
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;
    }
    
    //解构写法
    function getFullName ({firstName,lastName}) {
    }
    ```


## 参考链接


<http://es6.ruanyifeng.com/>
    

