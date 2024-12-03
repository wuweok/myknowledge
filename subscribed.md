参考资料：

1. https://developers.weixin.qq.com/community/develop/article/doc/000c2a2911cc889cdf5052f1e61013
2. https://developers.weixin.qq.com/doc/offiaccount/Message_Management/Template_Message_Interface.html#%E5%8F%91%E9%80%81%E6%A8%A1%E6%9D%BF%E6%B6%88%E6%81%AF
3. https://blog.csdn.net/qq_39687901/article/details/85243514

Q1: 公众号推送消息，需要订阅吗？
A1：不需要订阅，每个模板日调用测试
所有服务号都可以在功能->添加功能插件处看到申请模板消息功能的入口，但只有认证后的服务号才可以申请模板消息的使用权限并获得该权限；
需要选择公众账号服务所处的2个行业，每月可更改1次所选行业；
在所选择行业的模板库中选用已有的模板进行调用；
每个账号可以同时使用25个模板。
当前每个账号的模板消息的日调用上限为10万次，单个模板没有特殊限制。【2014年11月18日将接口调用频率从默认的日1万次提升为日10万次，可在MP登录后的开发者中心查看】。当账号粉丝数超过10W/100W/1000W时，模板消息的日调用上限会相应提升，以公众号MP后台开发者中心页面中标明的数字为准。


一天调用


1. 用户订阅
订阅分类：
a. 用户订阅了70大城市报告
b. 订阅了某个城市的数据。
c. 订阅了某个指标


为前端每个订阅定义一个订阅标识符

这个订阅标识符， 会关联若干个子表。 

当一个依赖的指标发生变化后， 就会创建一个action item 待激活。 放入代办事件列表。

然后自动任务定时从列表中取出一个代办项执行相应工作。

这里要确保，任务产生和任务执行的先后次序。 防止重复多通知。



subscribe_dependce
	subscribe_identifier
	indicator_id
	action

subscribe_to_do_list
	subscribe_identifier
	indicator_id   => source
	data_date      => 
	action         =>
    status         => new


Step1： 当某个子表创建新的数据后， 
Step2： 参看subscribe_dependce表， 为每个 subscribe_identifier创建相应的待通知消息。放到todo list中。
Step3:  schedule 服务定时从todo list 中找到subscribe 的人发送消息。并软删除待办工作项，更新相应信息。


公众号通知： 有两类

1. 客户在小程序上订阅了。 然后数据更新会执行通知。

2. 主动通知：
2.1 主动通知 会招来客户烦。 => 暂不使用，



3. implement
3.1 获得公众号，关注列表
3.1.1 https://developers.weixin.qq.com/doc/offiaccount/User_Management/Getting_a_User_List.html
 






