# Knowledge pipeline template

## Input
输入定义从个人数据来源转换成结构化的knowledge object的过程，并且定义在object上调用parser的粒度。比如典型的几种Input的实现：
+ 本地目录：指定本地目录，扫描本地目录的所有文件，并且监听他的更新；对每个一个文件生成object并且写入object store；对每一个新产生的object调用parser；
+ 个人邮箱：扫描个人邮箱收件箱，并且监听新的邮件；对每一封邮件生成email object并且写入object store；对每一个新产生的email object调用parser；
+ 浏览器上下文：实现浏览器插件，对当前浏览的页面元素通过rpc传入对应的input 后端实现，生成rich text object；对每一个新产生的rich text object调用parser；

## Parser
Parser定义从input 输入的object写入knowledge base的过程；包括但不限于以下主要手段，以及他们的组合：
+ 向量化之后写入vector store
+ 创建各种维度的RDB，NoSQL索引
+ 向Agent send object

配置Pipeline template应当包含以下几个部分：
+ Input method：包含实现input的 python module
+ Input params：inpu module的参数，比如本地路径，邮箱地址
+ Parser method：包含实现parser的 python module；如果Parser是指向Agent，这个配置是可以简化成Agent instance name；

# Knowlege pipeline manager
pipeline 管理会类似agent manager，manager管理template，从template 创建instance在后台持续运行，并且instance需要一些查询接口来获取pipeline的进度；

集成到aios shell中，加入如下命令行：
+ knowledge pipeline start $template $instance  
+ knowledge pipeline stop $instance
+ knowledge pipeline progress $instance




