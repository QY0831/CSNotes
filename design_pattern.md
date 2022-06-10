# 1 面向对象设计原则
## 1.1 单一职责原则
一个类只负责一个功能领域中的相应职责，或者可以定义为：就一个类而言，应该只有一个引起它变化的原因。  
一个类（大到模块，小到方法）承担的职责越多，它被复用的可能性就越小!
## 1.2 开闭原则
一个软件实体应当对扩展开放，对修改关闭。即软件实体应尽量在不修改原有代码的情况下进行扩展。  
抽象化是开闭原则的关键。如果需要修改系统的行为，无须对抽象层进行任何改动，只需要增加新的具体类来实现新的业务功能即可，
实现在不修改已有代码的基础上扩展系统的功能，达到开闭原则的要求。
## 1.3 里氏代换原则
所有引用基类（父类）的地方必须能透明地使用其子类的对象。  
子类的所有方法必须在父类中声明，或子类必须实现父类中声明的所有方法；尽量把父类设计为抽象类或者接口，让子类实现在父类中声明的方法，
在程序中尽量使用基类类型来对对象进行定义，运行时，子类实例替换父类实例，我们可以很方便地扩展系统的功能，同时无须修改原有子类的代码，
增加新的功能可以通过增加一个新的子类来实现。  
里氏代换原则是实现开闭原则的重要方式之一。
## 1.4 依赖倒转原则
抽象不应该依赖于细节，细节应当依赖于抽象。换言之，要针对接口编程，而不是针对实现编程。  
在引入抽象层后，系统将具有很好的灵活性，在程序中尽量使用抽象层进行编程，而将具体类写在配置文件中，这样一来，如果系统行为发生变化，
只需要对抽象层进行扩展，并修改配置文件，而无须修改原有系统的源代码，在不修改的情况下来扩展系统的功能，满足开闭原则的要求。  
针对抽象层编程，将具体类的对象通过依赖注入(DependencyInjection, DI)的方式注入到其他对象中，
依赖注入是指当一个对象要与其他对象发生依赖关系时，通过抽象来注入所依赖的对象。（里氏代换原则保证了所有子类都能被使用）  
**开闭原则是目标，里氏代换原则是基础，依赖倒转原则是手段。**
## 1.5 接口隔离原则
使用多个专门的接口，而不使用单一的总接口，即客户端不应该依赖那些它不需要的接口。  
接口应该尽量细化，同时接口中的方法应该尽量少，每个接口中只包含一个客户端（如子模块或业务逻辑类）所需的方法即可，
客户端在实现接口，不应该需要实现那些客户端用不到的方法。
## 1.6 合成复用原则
尽量使用对象组合，而不是继承来达到复用的目的。  
对继承而言，如果基类发生改变，那么子类的实现也不得不发生改变；从基类继承而来的实现是静态的，不可能在运行时发生改变，没有足够的灵活性。    
由于组合或聚合关系可以将已有的对象（也可称为成员对象）纳入到新对象中，使之成为新对象的一部分，因此新对象可以调用已有对象的功能，
相对继承关系而言，其耦合度相对较低，成员对象的变化对新对象的影响不大。  
一般而言，如果两个类之间是“Has-A”的关系应使用组合或聚合，如果是“Is-A”关系可使用继承。"Is-A"是严格的分类学意义上的定义，
意思是一个类是另一个类的"一种"；而"Has-A"则不同，它表示某一个角色具有某一项责任。
## 1.7 迪米特法则
一个软件实体应当尽可能少地与其他实体发生相互作用。  
应该尽量减少对象之间的交互，如果两个对象之间不必彼此直接通信，那么这两个对象就不应当发生任何直接的相互作用，
如果其中的一个对象需要调用另一个对象的某一个方法的话，可以通过第三者转发这个调用。简言之，就是通过引入一个合理的第三者来降低现有对象之间的耦合度。

# 2 创建型模式
## 2.1 简单工厂模式
定义一个工厂类，它可以根据参数的不同返回不同类的实例，被创建的实例通常都具有共同的父类。  
包含三个角色：
 - 工厂类：负责实现创建所有产品实例的内部逻辑；工厂类可以被外界直接调用，创建所需的产品对象；在工厂类中提供了静态的工厂方法factoryMethod()，
它的返回类型为抽象产品类型Product。
 - 抽象产品类：它是工厂类所创建的所有对象的父类，封装了各种产品对象的公有方法，它的引入将提高系统的灵活性，
使得在工厂类中只需定义一个通用的工厂方法，因为所有创建的具体产品对象都是其子类对象。
 - 具体产品类：它是简单工厂模式的创建目标，所有被创建的对象都充当这个角色的某个具体类的实例。
每一个具体产品角色都继承了抽象产品角色，需要实现在抽象产品中声明的抽象方法。  
我们可以将静态工厂方法的参数存储在XML或properties格式的配置文件中，在不修改源代码的情况下，控制需要创建的产品，符合开闭原则。  
### 优点
 - 免去客户端创建对象的职责，实现了对象创建和使用的分离。  
 - 客户端无需知道具体产品的类名，只要知道具体的参数名。  
 - 参数可以存储在配置文件中，提高了系统的灵活性。  
### 缺点
 - 工厂类承担所有创建逻辑，职责过重，一旦出现问题，整个系统都会出现问题。
 - 势必会引入更多的工厂类，增加了系统复杂度。
 - 系统扩展困难，一旦添加新产品就不得不修改工厂逻辑。
### 适用场景
 - 工厂需要创建的对象较少。
 - 客户端只知道传入工厂的参数，不关心对象如何创建。
```python
# python中,抽象类和接口类没有明确的界限,若是类中所有的方法都没有实现,则认为是一个接口,若是部分方法实现,
# 则认为是一个抽象类,抽象类和接口类都仅用于被继承,不能被实例化。
from abc import ABC, abstractmethod
class AbstractProduct(ABC):
    @abstractmethod
    def do_something(self):
        pass

class ProductA(AbstractProduct):
    def do_something(self):
        print('I am A')

class ProductB(AbstractProduct):
    def do_something(self):
        print('I am B')

class Factory:
    @staticmethod
    def get_product(name):
        if name == 'A':
            return ProductA()
        elif name == 'B':
            return ProductB()

if __name__ == '__main__':
    product_name = 'A' # 可从配置文件得到
    product = Factory.get_product(product_name)
```

# 2.2 工厂方法模式
简单工厂模式虽然简单，但存在一个很严重的问题。当系统中需要引入新产品时，由于静态工厂方法通过所传入参数的不同来创建不同的产品，
这必定要修改工厂类的源代码，将违背“开闭原则”，如何实现增加新产品而不影响已有代码？  
在工厂方法模式中，我们不再提供一个统一的工厂类来创建所有的产品对象，而是针对不同的产品提供不同的工厂，
系统提供一个与产品等级结构对应的工厂等级结构。定义一个用于创建对象的接口，让子类决定将哪一个类实例化。工厂方法模式让一个类的实例化延迟到其子类。  
包含四个角色：
 - 抽象工厂类：声明了工厂方法(Factory Method)，用于返回一个产品。抽象工厂是工厂方法模式的核心，所有创建对象的工厂类都必须实现该接口。
 - 具体工厂类：抽象工厂类的子类，实现了抽象工厂中定义的工厂方法，并可由客户端调用，返回一个具体产品类的实例。
 - 抽象产品类：产品对象的公共父类。
 - 具体产品类：实现了抽象产品接口，某种类型的具体产品由专门的具体工厂创建，具体工厂和具体产品之间一一对应。

```python
from abc import ABC, abstractmethod
class AbstractProduct(ABC):
    @abstractmethod
    def do_something(self):
        pass

class ProductA(AbstractProduct):
    def do_something(self):
        print('I am A')

class ProductB(AbstractProduct):
    def do_something(self):
        print('I am B')

class AbstractFactory(ABC):
    
    @staticmethod
    @abstractmethod
    def get_product():
        pass

class FactoryA(AbstractFactory):
    @staticmethod
    def get_product():
        return ProductA()

class FactoryB(AbstractFactory):
    @staticmethod
    def get_product():
        return ProductB()

if __name__ == '__main__':
    factory = FactoryA() # 可从配置文件得到
    product = factory.get_product()
```
### 优点
 - 用户只需要关心所需产品对应的工厂。  
 - 工厂可以自主确定创建何种产品对象。  
 - 系统中加入新产品时，无须修改抽象工厂和抽象产品提供的接口，无须修改客户端，也无须修改其他的具体工厂和具体产品，而只要添加一个具体工厂和具体产品就可以了。  
### 缺点
 - 在添加新产品时，需要编写新的具体产品类，而且还要提供与之对应的具体工厂类，系统中类的个数将成对增加，在一定程度上增加了系统的复杂度。
### 适用场景
 - 客户端不知道它所需要的对象的类。
 - 抽象工厂类通过其子类来指定创建哪个对象。

## 2.3 抽象工厂模式
由于工厂方法模式中的每个工厂只生产一类产品，可能会导致系统中存在大量的工厂类，势必会增加系统的开销。
此时，我们可以考虑将一些相关的产品组成一个“产品族”，由同一个工厂来统一生产。
抽象工厂模式(Abstract Factory Pattern)提供一个创建一系列相关或相互依赖对象的接口，而无须指定它们具体的类。
包含四个角色：
 - 抽象工厂类：它声明了一组用于创建一族产品的方法，每一个方法对应一种产品。
 - 具体工厂类：实现了在抽象工厂中声明的创建产品的方法，生成一组具体产品，这些产品构成了一个产品族。
 - 抽象产品类：为每种产品声明接口，声明了产品所具有的业务方法。
 - 具体产品类：定义具体工厂生产的具体产品对象，实现抽象产品接口中声明的业务方法。  

```python
from abc import ABC, abstractmethod
class AbstractProductA(ABC):
    @abstractmethod
    def do_something(self):
        pass

class ProductA1(AbstractProductA):
    def do_something(self):
        print('I am A1')

class ProductA2(AbstractProductA):
    def do_something(self):
        print('I am A2')
        
class AbstractProductB(ABC):
    @abstractmethod
    def do_something(self):
        pass

class ProductB1(AbstractProductB):
    def do_something(self):
        print('I am B1')

class ProductB2(AbstractProductB):
    def do_something(self):
        print('I am B2')

class AbstractFactory(ABC):
    
    @staticmethod
    @abstractmethod
    def create_productA():
        pass
    
    @staticmethod
    @abstractmethod
    def create_productB():
        pass

class Factory1(AbstractFactory):
    @staticmethod
    def create_productA():
        return ProductA1()
    
    @staticmethod
    def create_productB():
        return ProductB1()

class Factory2(AbstractFactory):
    @staticmethod
    def create_productA():
        return ProductA2()
    
    @staticmethod
    def create_productB():
        return ProductB2()

if __name__ == '__main__':
    factory = Factory1() # 可从配置文件得到
    product = factory.create_productA()
```
在抽象工厂模式中，增加新的产品族很方便，但是增加新的产品等级结构很麻烦，抽象工厂模式的这种性质称为“开闭原则”的倾斜性。  
### 优点
 - 隔离了具体类的生成，使得客户并不需要知道什么被创建。  
 - 当一个产品族中的多个对象被设计成一起工作时，它能够保证客户端始终只使用同一个产品族中的对象。  
 - 增加新的产品族很方便，无须修改已有系统，符合“开闭原则”。 
### 缺点
 - 增加新的产品等级结构麻烦，需要对原有系统进行较大的修改，甚至需要修改抽象层代码，这显然会带来较大的不便，违背了“开闭原则”。
### 适用场景
 - 用户无须关心对象的创建过程。
 - 系统中有多于一个的产品族，而每次只使用其中某一产品族。可以通过配置文件等方式来使得用户可以动态改变产品族，也可以很方便地增加新的产品族。
 - 属于同一个产品族的产品将在一起使用。
 - 产品等级结构稳定，设计完成之后，不会向系统中增加新的产品等级结构或者删除已有的产品等级结构。

## 2.4 单例模式
为了节约系统资源，有时需要确保系统中某个类只有唯一一个实例，当这个唯一实例创建成功之后，我们无法再创建一个同类型的其他对象，
所有的操作都只能基于这个唯一实例。为了确保对象的唯一性，我们可以通过单例模式来实现，这就是单例模式的动机所在。  

单例模式(Singleton Pattern)：确保某一个类只有一个实例，而且自行实例化并向整个系统提供这个实例，这个类称为单例类，它提供全局访问的方法。  
```python
class SingletonClass(object):
  def __new__(cls):
    if not hasattr(cls, 'instance'):
      cls.instance = super(SingletonClass, cls).__new__(cls)
    return cls.instance

singleton = SingletonClass()
new_singleton = SingletonClass()
 
print(singleton is new_singleton)  # True
 
singleton.singl_variable = "Singleton Variable"
print(new_singleton.singl_variable)  # Singleton Variable  


class SingletonChild(SingletonClass):
    pass
   
singleton = SingletonClass() 
child = SingletonChild()
print(child is singleton)  # True
 
singleton.singl_variable = "Singleton Variable"
print(child.singl_variable)  # Singleton Variable
```
假如在某一瞬间线程A和线程B都在调用new()方法，此时instance对象为null值，均能通过instance == null的判断。
由于加锁机制，线程A进入锁定的代码中执行实例创建代码，线程B处于排队等待状态，
必须等待线程A执行完毕后才可以进入synchronized锁定代码。
但当A执行完毕时，线程B并不知道实例已经创建，将继续创建新的实例，导致产生多个单例对象，违背单例模式的设计思想，
因此需要进行进一步改进，进行一次(instance == null)判断，这种方式称为双重检查锁定(Double-Check Locking)。  
```python
class Singleton:
  _instance = None
  _lock = threading.Lock()

  def __new__(cls, *args, **kwargs):
    if not cls._instance:
        with cls._lock:
          # another thread could have created the instance
          # before we acquired the lock. So check that the
          # instance is still nonexistent.
          if not cls._instance:
            cls._instance = super(Singleton, cls).__new__(cls)
    return cls._instance
```
### 优点
 - 单例模式提供了对唯一实例的受控访问。因为单例类封装了它的唯一实例，所以它可以严格控制客户怎样以及何时访问它。  
 - 由于在系统内存中只存在一个对象，因此可以节约系统资源。  
 - 允许可变数目的实例。基于单例模式我们可以进行扩展，使用与单例控制相似的方法来获得指定个数的对象实例，既节省系统资源，又解决了单例单例对象共享过多有损性能的问题。 
### 缺点
 - 由于单例模式中没有抽象层，因此单例类的扩展有很大的困难。
 - 单例类的职责过重，在一定程度上违背了“单一职责原则”。因为单例类既充当了工厂角色，提供了工厂方法，同时又充当了产品角色，包含一些业务方法，将产品的创建和产品的本身的功能融合到一起。
 - 现在很多面向对象语言(如Java、C#)的运行环境都提供了自动垃圾回收的技术，因此，如果实例化的共享对象长时间不被利用，系统会认为它是垃圾， 会自动销毁并回收资源，
下次利用时又将重新实例化，这将导致共享的单例对象状态的丢失。
### 适用场景
 - 系统只需要一个实例对象，如系统要求提供一个唯一的序列号生成器或资源管理器，或者需要考虑资源消耗太大而只允许创建一个对象。
 - 客户调用类的单个实例只允许使用一个公共访问点，除了该公共访问点，不能通过其他途径访问该实例。

