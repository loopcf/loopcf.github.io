###android的通知机制###

在android中，不同模块之间进行传值操作的时候，常见的会用到的android的通知机制有
>1.handler机制  
>2.callback机制  
>3.广播  
>4.自定义观察者设计模式

其中，广播和自定义观察者设计模式，是一对多的解决方案。假设，有一处数据变更的时候，涉及到几处ui的更新，就需要用到一对多的解决方案。

---

##观察者设计模式##

>观察者设计模式是一种一对多的依赖模式
>>多个观察者同时监听某个对象，当对象状态发生改变的时候，会发出通知，通知所有观察者更新自身状态。      
  

最贴近生活的例子就是订阅，当我们浏览一些博客的时候会有看到RSS
图标，就这的意思是，当你订阅了改文章，如果后续有更新，会及时通知你，简单的说就是当数据变化时候，就会通知你

则有两个角色
>1.发布者  对应被观察者
>2.接受者  对应观察者

在java中，提供了一快速实现观察者设计模式的方案。  
  
java中提供了一个类Observable和一个接口Observer

![](http://i.imgur.com/r8dMRJi.png)

其中Obervable有以下的方法 
![](http://i.imgur.com/DnVstlf.png)
需要注意的方法有
>1.addObserver(Observer)//添加观察者  
2.deleteObserver(Observer)//删除观察者  
3.notifyObservers()//通知所有的观察者有消息了(数据发生改变了)  4.setChanged()//数据记录发生改变的标记    

接下来简单的模拟写一个demo去实现观察者设计模式

继承类
![](http://i.imgur.com/tCiKYyr.png)
实现接口
![](http://i.imgur.com/pk9wV3w.png)
![](http://i.imgur.com/f6xz6Vv.png)

接着是测试
![](http://i.imgur.com/wJps3Dw.png)

输出结果是：
>![](http://i.imgur.com/nnyYbVs.png)

---

在java里面可以使用这种现成方式去实现观察者模式，但是这个方法放在android上有缺陷。因为java里面是单继承多实现，android里面组件需要继承父类组件，比如一般的控件都要继承view、viewGroup本身或者子类。  

这个时候我们要需要自定义观察者设计模式

##自定义观察者设计模式
自定义观察者设计模式分一下几个步骤  

举例子 中介 -- 买房    

买房的人
>1.自己需要知道房产信息 ==> 成为观察者  
2.找对应的中介 -- 订阅消息 ==>添加观察者到观察者集合   
3.中介还要在有消息的时候 -- 发布消息==>通知所有观察者

所以将上面的demo改成
![](http://i.imgur.com/aMQJFlT.png)

将继承类Observable改成在内部自定义一个接口和定义一个放置接口对象的集合，用集合去实现添加删除观察者。

在类Observable中，它实现几个重要功能，添加删除以及通知数据更新的方法的源码  
添加:
![](http://i.imgur.com/h9ckHJO.png)
删除:  
![](http://i.imgur.com/NJ46g1T.png)
通知数据更新:
![](http://i.imgur.com/UzgFoYk.png)

在自定义观察者中，我们模仿类Observable，给发布者添加上面三种方法，代码改成
![](http://i.imgur.com/A8DodMN.png)
再添加一段常用的发布消息的方法
![](http://i.imgur.com/1Ve975k.png)

	
