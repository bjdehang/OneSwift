# 如何给Tableview、Collectionview添加动效
> OneSwift - iOS Tips Only Based On Swift

Tableview和Collectionview在开发产品中使用非常频繁，不管是独立使用还是组合使用，掌握它们都是所有iOS开发者必备的技能。

今天为大家来分享我使用它们时，如何实现动效的？内容分两部分：
1.加载动效
2.点击动效

一、加载动效
当组件加载时，为了让页面显得动感有趣，可以为Tableview/Collection整体添加动效。
用到的方法是：

方案一，Cell逐个呈现，例如OneDay的首页加载。
实现方法是在tableview加载后增加整体的动效，通过循环和延迟，让每个cell从不同的时间开始经历相同的时间动效结束。


方案二，Cell同时呈现，例如OneClock的菜单加载。
实现方式是在Collectionview加载后，为整体增加动效，因为不需要做延迟处理，所以可以直接以CollectionView整体做动效。



二、点击动效

Tableview和Collectionview在被点击时可以添加一定的动效，同时在点击完成后我们需要恢复最初始的状态。
用到的方法是：

Tablview的点击效果，例如OneDay的列表点击，代码如下：

Collection的点击效果，例如OneClock的菜单点击，代码如下：

两种方案都用了比较平滑的方式实现，如果直接修改大小，你们点击效果显得非常生硬。


更多Swift教程，欢迎大家关注微博或者OneSwift。
