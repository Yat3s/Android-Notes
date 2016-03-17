# 自己在Android开发中遇到的一些问题Summary

## Speed up
- 在写企业项目适合尽量每个文件名加上企业缩写前缀，用Android studio为每个Java文件加上头标注
- 用ButterKnife和ButterKnife Zelezny搭配起来让你写完布局时候快速生成View的Java代码


## Be a habit
- 代码函数块中除了无意义的0等以为，请不要在代码中出现Magic number，请给它取个漂亮的名字，并final static
- 在if判断中尽量做到 `if（null == object）` 而不要`if(object == null)`,很容易你少了一个等号，这种bug极其难被察觉
- 在一个app中会有很多文字按钮等，尽量自己建立一个ContentTextView来继承TextView，如果设计师说要统一换字体样式的话只要改一个文件就好，其他按钮、layout同理，酌情考虑
- 注释中//后空一格，首字母大写！
- 没完成或没写好的功能或者trick的功能块，请加上 // TODO，并且在github上加issue，避免以后遗漏掉该问题
- 回调函数的命名尽量是onXXX(){}，加载网络数据函数可命名为loadXXX(){},

## Memory optimize
- 在有键盘弹出的情况下不要在该页面设置View的Y方向的weight，因为这样你弹出键盘的时候你设置adjustSize的时候那个view会被挤压很难看。
- 合理利用Java的内存管理机制，activity中intent传递对象也是传递地址，所以只需要在另外页面改变当前指，回到原页面后只需要update一下即可，不需要再onActivityResult中再取值。
- 用MVP模式中一定要主要内存泄露问题，Presenter注意要弱应用, 注意在处理Fragment和Adapter情况下的数据同步问题
- 用Handler一定要考虑内存泄露问题，在任何子线程中回调的接口中考虑一下这个页面已经被关闭的情况。
- 你的Activity的Context给别人的时候，一定要考虑它是不是static等类，是不是会持有你的Context引用，不然的话不给！！！
- 请考虑统一管理Exception，可使用Bugly等工具来收集统一。
- 封装一个函数或接口尽量不要对外暴露你是如何实现，随时想着这个函数或接口是给一个陌生网友用的。


## Persistence
- 用户的个人信息千万不要存储在app目录下的Cache文件下，不然用户清除一下垃圾，“什么？我又要登录了？”。反过来，如果是不重要的缓存文件，请尽量存储在Cache下，不然app不主动清理，系统是清理不了的。
- 如果想做缓存方案，请先确立详细的策略再下手，不然发现有问题，再升级是很伤脑筋的...比如更换数据库等
- GreenDao需要一定的学习成本，如果不是极其大的App可以不考虑这个库（反正我是折腾了几天，发现除了速度快没其他了...怪我笨），Ormlite也是好的选择。


