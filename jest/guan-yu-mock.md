# 关于mock

## mock整个第三方模块

例如 如果代码中仅有ajax操作

待测试代码

```javascript
_get_interface_url(callback) {
    $.ajax(...)
}
```

测试代码
```javascript
let Speed, $, speed, callback
beforeEach(() => {
    jest.resetModules() //令 $.ajax.mock.calls 不进行次数计算
    Speed = require('../src/index')
    $ = require('jquery')
    jest.mock('jquery')
    speed = new Speed()
    callback = jest.fn()
});

it('_get_interface_url success ', () => {
    let mock_data = {
            errno: 0,
            interface_ip: '127.0.0.1',
            interface_port: 80,
        }
    
    speed._get_interface_url(callback)
    
    $.ajax.mock.calls[0][0].success(mock_data) // 这里第一个0代表 $.ajax第一次被模拟时的第一个参数

    expect(callback.mock.calls[0][0]).toEqual({ // 这里第一个0代表 callback第一次被模拟时的第一个参数
        errno: 0,
        message: '',
        url: 'http://127.0.0.1:80/',
        data: {
            ajax_query_portal: mock_data
        }
    })
})
```
这样的方式实现简单

但有个问题 如果直接`jest.mock('jquery')` 整个模块都mock的 例如$.Deferred() 返回都是undefined

可以看看 [官网mock说明](https://facebook.github.io/jest/docs/en/jest-object.html#jestmockmodulename-factory-options)

## 自己实现mock 第三方库

回到刚刚的问题 

如果只想要mock jquery的ajax 又想用jquery的其他方法如何

[官网自行mock函数库](https://facebook.github.io/jest/docs/en/mock-function-api.html#content)

首先写好mock函数

```javascript
let jquery = jest .genMockFromModule('jquery')

let ajax_options 

jquery.__ajax_success = result =>{
    ajax_options.success(result)
}

jquery.__ajax_error = result => {
    ajax_options.error(result)
}


jquery.ajax = options => {
    
    ajax_options = options
}

module.exports = jquery
```

测试代码

```javascript
let Speed, $, speed, callback
beforeEach(() => {
    jest.resetModules()
    Speed = require('../src/index')
    $ = require('jquery')
    //注意 这里再也不用 jest.mock('jquery')
    speed = new Speed()
    callback = jest.fn()
});

it('_get_interface_url success ', () => {
    let mock_data = {
            errno: 0,
            interface_ip: '127.0.0.1',
            interface_port: 80,
        }
    
    speed._get_interface_url(callback)

    $.__ajax_success(mock_data)

    expect(callback.mock.calls[0][0]).toEqual({
        errno: 0,
        message: '',
        url: 'http://127.0.0.1:80/',
        data: {
            ajax_query_portal: mock_data
        }
    })
})
```

## 只mock $.ajax

以上方法都是整个jquery都是模拟的 只有ajax可用 其他所有函数方法都是返回undefined

所以把代码改成这样, 就可以只mock$.jquery

```javascript
let $
beforeEach(() => {
    $ =  require('jquery')
    $.ajax = jest.genMockFunction()

});
```
