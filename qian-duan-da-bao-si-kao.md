# 前端打包思考

# 背景 

在公司里,很多一个个小项目

在这个一个个小项目里

如果快速的搭建构建部分

# 目标

通过命令行导入项目前端架构

直接把重构的代码丢进src,然后进行JS逻辑处理,然后输出到public

# 斟酌点

## all in one 还是 one in one

all in one 就是所有页面js都打包成一个

on in one 就是每个页面 只加载自己的js和css

all in one 

优点

1. 减少HTTP请求
2. 对一些公用的模块,不需要每个页面都显式的require

缺点

1. 增加了首次加载的大小
2. 对于一些其他页面不需要执行的js,需要判断哪个url,哪个JS要执行的 

最后还是选择了one in one

每个页面,有自己单独的js

原因是因为如果all in one,就迫不得已在一些不需要执行的js里判断location.path 然后return,实在强迫症


# 功能点

## 按chunks 划分模块

例如每个页面都是一个chunks,通用导航栏和底部栏是一个chunks,通用的lib是一个chunks


# 遗留问题

1. 一个页面需要单独的lib

