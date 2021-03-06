# 数据缓存Data

# 简介

jQuery的队列模块,动画模块,样式操作模块,事件系统模块,都需要用到缓存的Data

例如队列模块只负责如何去操控队列中的每一个元素如何执行,而队列的元素存储,是靠数据缓存Data的

# 结构

Data缓存模块是一个很典型的把方法存储在原型中,而动态的属性放在实体中

```javascript

function Data() {
	this.expando = jQuery.expando + Data.uid++;
}

Data.uid = 1;

Data.prototype = {
    cache: function(owner) // 获取owner的cache对象
    set: function(owner, data, value) //设置缓存值
    get: function(owner, key) {return 缓存值} //获取缓存值
    access: function(owner, key, value) {return 缓存值}//设置或获取缓存值
    remove: function(owner, key) {return 缓存值} //移除key
    hasData: function(owner) {return 缓存值} //判断是否含有key值
}
```

这样别的地方new Data(),就能

1. 分别占用this.expando属性值
2. 没被获取的uid
3. 共享Data.prototype的方法

因为uid是用来区分唯一标识expando的,但无需被实例知道,只需要知道最终的expando即可

但是在jquery里只会被new两次,

一个是src/data/var/dataPriv里用 是jquery内部使用的

另一个是src/data/var/dataUser里用的,专门给用户调用缓存



