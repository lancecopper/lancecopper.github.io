---
title: 设计模式系列--observer
---

### 适用性

在以下任一情况下可以使用观察者模式 :

* 当一个抽象模型有两个方面 , 其中一个方面依赖于另一方面。将这二者封装在独立的对象中以使它们可以各自独立地改变和复用。

* 当对一个对象的改变需要同时改变其它对象 , 而不知道具体有多少对象有待改变。

* 当一个对象必须通知其它对象，而它又不能假定其它对象是谁。换言之 , 你不希望这些对象是紧密耦合的。


```python
from abc import ABCMeta, abstractmethod

class Subject():
    '''
    Subject 知道它的 Observer。可以有任意多个Observer观察同一个Subject。
    提供注册和删除Observer对象的接口。
    '''
    def __init__(self):
        self.__observers = []

    def attach(self, observer):
        self.__observers.append(observer)

    def detatch(self, observer):
        self.__observers.remove(observer)
    
    def notify(self):
        for o in self.__observers:
            o.update()

class Observer():
    '''
    为那些在Subject发生改变时需获得通知的对象定义一个更新接口。
    用abc库实现了一个简单的抽象类。
    '''
    __metaclass__ = ABCMeta
    
    @abstractmethod
    def update(self):
        pass

class ConcreteSubject(Subject):
    '''
    将有关状态存入具体的Observer对象
    在具体主题的内部状态改变时，给所有登记过的Observer发出通知
    '''
    @property
    def status(self):
        return self._status
    @status.setter
    def status(self, value):
        self._status = value
        self.notify()
    
class ConcreteObserver(Observer):
    '''
    维护一个指向ConcreteSubject对象的引用。
    存储有关状态，这些状态应与目标的状态保持一致。
    实现Observer的更新接口以使自身状态与目标的状态保持一致。
    '''
    def __init__(self, subject, name):
        self.subject = subject                      # 指向ConcreteSubject的引用
        self.name = name                            
        self.objserver_status = None                # object status 

    def update(self):                               # 覆写抽象Object类，否则无法实例化
        self.objserver_status = self.subject.status
        print("observer %s status changed to %s: " % (self.name, self.objserver_status))

if __name__ == '__main__':
    s = ConcreteSubject()
    s.attach(ConcreteObserver(s, "X"))
    s.attach(ConcreteObserver(s, "Y"))
    s.attach(ConcreteObserver(s, "Z"))

    s.status = "A"
    s.status = "B"    
```




