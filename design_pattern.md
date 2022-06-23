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
编程时变量声明为超类型(抽象类或者接口或者父类)，不针对具体子类或者实际类型，不需要考虑执行的类型到时是哪种实际类型，这样能大大提高程序的灵活性，
是松耦合思想的体现。后期如果想更改实际类型，不需要更改很多代码，提高了程序的可维护性。
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

## 2.2 工厂方法模式
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
import threading
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

## 2.5 原型模式
使用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。  
需要注意的是通过克隆方法所创建的对象是全新的对象，它们在内存中拥有新的地址，通常对克隆所产生的对象进行修改对原型对象不会造成任何影响，
每一个克隆对象都是相互独立的。  
### 角色
 - 抽象原型类：声明克隆方法的接口，是所有具体原型类的公共父类，可以是抽象类也可以是接口，甚至还可以是具体实现类。
 - 具体原型类：实现在抽象原型类中声明的克隆方法，在克隆方法中返回自己的一个克隆对象。
 - 客户类：让一个原型对象克隆自身从而创建一个新的对象，在客户类中只需要直接实例化或通过工厂方法等方式创建一个原型对象，
再通过调用该对象的克隆方法即可得到多个相同的对象。

```python
import copy
from abc import ABC, abstractmethod
class Prototype(ABC):
    @abstractmethod
    def clone(self):
        pass

class ConcretePrototypeA(Prototype):
    def clone(self):
        return copy.deepcopy(self)

class ConcretePrototypeB(Prototype):
    def clone(self):
        return copy.deepcopy(self)
```
### 优点
 - 当创建新的对象实例较为复杂时，使用原型模式可以简化对象的创建过程，通过复制一个已有实例可以提高新实例的创建效率。
 - 扩展性较好，由于在原型模式中提供了抽象原型类，在客户端可以针对抽象原型类进行编程，而将具体原型类写在配置文件中，
增加或减少产品类对原有系统都没有任何影响。
 - 原型模式提供了简化的创建结构，产品的复制是通过封装在原型类中的克隆方法实现的。
 - 可以使用深克隆的方式保存对象的状态，使用原型模式将对象复制一份并将其状态保存起来，以便在需要的时候使用（如恢复到某一历史状态），可辅助实现撤销操作。
### 缺点
 - 需要为每一个类配备一个克隆方法，而且该克隆方法位于一个类的内部，当对已有的类进行改造时，需要修改源代码，违背了“开闭原则”。
 - 在实现深克隆时需要编写较为复杂的代码，而且当对象之间存在多重的嵌套引用时，为了实现深克隆，每一层对象对应的类都必须支持深克隆，实现起来可能会比较麻烦。(Python里已经封装好了)
### 适用场景
 - 创建新对象成本较大（如初始化需要占用较长的时间，占用太多的CPU资源或网络资源），新的对象可以通过原型模式对已有对象进行复制来获得，如果是相似对象，则可以对其成员变量稍作修改。
 - 如果系统要保存对象的状态，而对象的状态变化很小，或者对象本身占用内存较少时，可以使用原型模式配合备忘录模式来实现。

## 2.6 建造者模式
将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。  
建造者模式一步一步创建一个复杂的对象，它允许用户只通过指定复杂对象的类型和内容就可以构建它们，用户不需要知道内部的具体构建细节。  
### 角色
 - 抽象建造者：为创建一个产品Product对象的各个部件指定抽象接口，在该接口中一般声明两类方法，一类方法是buildPartX()，它们用于创建复杂对象的各个部件；
另一类方法是getResult()，它们用于返回复杂对象。Builder既可以是抽象类，也可以是接口。
 - 具体建造者：实现了Builder接口，实现各个部件的具体构造和装配方法，定义并明确它所创建的复杂对象，也可以提供一个方法返回创建好的复杂产品对象。
 - 产品角色：被构建的复杂对象，包含多个组成部件，具体建造者创建该产品的内部表示并定义它的装配过程。
 - 指挥者：又称为导演类，它负责安排复杂对象的建造次序，指挥者与抽象建造者之间存在关联关系，
可以在其construct()建造方法中调用建造者对象的部件构造与装配方法，完成复杂对象的建造。客户端一般只需要与指挥者进行交互。

```python
from abc import ABC, abstractmethod

class Product:
    
    def __init__(self, partA=None, partB=None):
        self.partA = partA
        self.partB = partB

class Builder(ABC):
    
    def __init__(self):
        self.product = Product()
    
    @abstractmethod
    def buildPartA(self):
        pass
    
    @abstractmethod
    def buildPartB(self):
        pass
    
    @abstractmethod
    def getResult(self):
        return self.product

class ConcreteBuilder(Builder):
    def buildPartA(self):
        self.product.partA = 'A'
    
    def buildPartB(self):
        self.product.partB = 'B'
    
    def getResult(self):
        return self.product

class Director:
    
    def __init__(self, builder):
        self.builder = builder
    
    def construct(self):
        self.builder.buildPartA()
        self.builder.buildPartB()
        return self.builder.getResult()

if __name__ == '__main__':
    builder = ConcreteBuilder()  # 可通过配置文件实现
    director = Director(builder)
    product = director.construct()
```
### 优点
 - 客户端不必知道产品内部组成的细节，将产品本身与产品的创建过程解耦。
 - 每一个具体建造者都相对独立，而与其他的具体建造者无关，因此可以很方便地替换具体建造者或增加新的具体建造者，用户使用不同的具体建造者即可得到不同的产品对象。
 - 将复杂产品的创建步骤分解在不同的方法中，使得创建过程更加清晰，也更方便使用程序来控制创建过程。
### 缺点
 - 建造者模式所创建的产品一般具有较多的共同点，其组成部分相似，如果产品之间的差异性很大，例如很多组成部分都不相同，不适合使用建造者模式，因此其使用范围受到一定的限制。
 - 如果产品的内部变化复杂，可能会导致需要定义很多具体建造者类来实现这种变化
### 适用场景
 - 需要生成的产品对象有复杂的内部结构，这些产品对象通常包含多个成员属性。
 - 需要生成的产品对象的属性相互依赖，需要指定其生成顺序。
 - 对象的创建过程独立于创建该对象的类。在建造者模式中通过引入了指挥者类，将创建过程封装在指挥者类中，而不在建造者类和客户类中。 
 - 隔离复杂对象的创建和使用，并使得相同的创建过程可以创建不同的产品。

# 3 结构型模式
## 3.1 适配器模式
将一个接口转换成客户希望的另一个接口，使接口不兼容的那些类可以一起工作，其别名为包装器(Wrapper)。适配器模式既可以作为类结构型模式，也可以作为对象结构型模式。  
### 角色
 - 目标抽象类: 目标抽象类定义客户所需接口，可以是一个抽象类或接口，也可以是具体类。  
 - 适配器类: 适配器可以调用另一个接口，作为一个转换器，对Adaptee和Target进行适配，适配器类是适配器模式的核心，在对象适配器中，它通过继承Target并关联一个Adaptee对象使二者产生联系。  
 - 适配者类: 适配者即被适配的角色，它定义了一个已经存在的接口，这个接口需要适配，适配者类一般是一个具体类，包含了客户希望使用的业务方法。(我们仅知道其参数和返回值，而不知道其细节，也不能修改其细节)
```python
from abc import ABC
class Adaptee:
    def need_method(self):
        pass

class Target(ABC):
    def methodA(self):
        pass

class Adaptor(Target):
    
    def __init__(self):
        self.adpatee = Adaptee()
    
    def methodA(self):
        self.adpatee.need_method()
```
除了对象适配器模式之外，适配器模式还有一种形式，那就是类适配器模式，类适配器模式和对象适配器模式最大的区别在于适配器和适配者之间的关系不同，
对象适配器模式中适配器和适配者之间是关联关系，而类适配器模式中适配器和适配者是继承关系。  
由于Java、C#等语言不支持多重类继承，因此类适配器的使用受到很多限制，类适配器较少使用。  

缺省适配器模式(Default Adapter Pattern)：当不需要实现一个接口所提供的所有方法时，可先设计一个抽象类实现该接口，
并为接口中每个方法提供一个默认实现（空方法），那么该抽象类的子类可以选择性地覆盖父类的某些方法来实现需求，
它适用于不想使用一个接口中的所有方法的情况，又称为单接口适配器模式。
### 角色
 - 适配者接口： 通常在该接口中声明了大量的方法。
 - 缺省适配器类：使用空方法的形式实现了在ServiceInterface接口中声明的方法。通常将它定义为抽象类。
 - 具体业务类：缺省适配器类的子类，在没有引入适配器之前，它需要实现适配者接口，因此需要实现在适配者接口中定义的所有方法，
而对于一些无须使用的方法也不得不提供空实现。在有了缺省适配器之后，可以直接继承该适配器类，根据需要有选择性地覆盖在适配器类中定义的方法。
```python
from abc import ABC
class AdapteeInterface(ABC):
    def methodA(self):
        pass
    def methodB(self):
        pass
    def methodC(self):
        pass

class Adapter(AdapteeInterface):
    def methodA(self):
        pass
    def methodB(self):
        pass
    def methodC(self):
        pass

class Service(Adapter):
    def methodA(self):
        print('only need this method')
```
### 优点
 - 将目标类和适配者类解耦，通过引入一个适配器类来重用现有的适配者类，无须修改原有结构。
 - 增加了类的透明性和复用性，将具体的业务实现过程封装在适配者类中，对于客户端类而言是透明的，而且提高了适配者的复用性，
同一个适配者类可以在多个不同的系统中复用。
### 缺点
 - 类适配器模式：对于Java、C#等不支持多重类继承的语言，一次最多只能适配一个适配者类，不能同时适配多个适配者。
### 适用场景
 - 系统需要使用一些现有的类，而这些类的接口（如方法名）不符合系统的需要，甚至没有这些类的源代码。 
 - 想创建一个可以重复使用的类，用于与一些彼此之间没有太大关联的一些类，包括一些可能在将来引进的类一起工作。

## 3.2 桥接模式
桥接模式是一种很实用的结构型设计模式，如果软件系统中某个类存在两个独立变化的维度，通过该模式可以将这两个维度分离出来，使两者可以独立扩展，
让系统更加符合“单一职责原则”。  
### 角色
 - 抽象类：用于定义抽象类的接口，它一般是抽象类而不是接口，其中定义了一个Implementor（实现类接口）类型的对象并可以维护该对象，
它与Implementor之间具有关联关系，它既可以包含抽象业务方法，也可以包含具体业务方法。
 - 扩充抽象类：扩充由Abstraction定义的接口，通常情况下它不再是抽象类而是具体类，它实现了在Abstraction中声明的抽象业务方法，
在RefinedAbstraction中可以调用在Implementor中定义的业务方法。
 - 实现类接口：定义实现类的接口，一般而言，Implementor接口仅提供基本操作，而Abstraction定义的接口可能会做更多更复杂的操作。
Implementor接口对这些基本操作进行了声明，而具体实现交给其子类。通过关联关系，在Abstraction中不仅拥有自己的方法，
还可以调用到Implementor中定义的方法，使用关联关系来替代继承关系。
 - 具体实现类：具体实现Implementor接口，在不同的ConcreteImplementor中提供基本操作的不同实现。
```python
from abc import ABC, abstractmethod

class Implementor(ABC):
    @abstractmethod
    def operationImpl(self):
        pass

class ConcreteImplementor(Implementor):
    def operationImpl(self):
        pass

class Abstraction(ABC):
    
    def __init__(self, impl):
        self.impl = impl
    
    @abstractmethod
    def operation(self):
        pass

class RefinedAbstraction(Abstraction):
    def operation(self):
        self.impl.operationImpl()
```
在使用桥接模式时，我们首先应该识别出一个类所具有的两个独立变化的维度，将它们设计为两个独立的继承等级结构，为两个维度都提供抽象层，
并建立抽象耦合。通常情况下，我们将具有两个独立变化维度的类的一些普通业务方法和与之关系最密切的维度设计为“抽象类”层次结构（抽象部分），
而将另一个维度设计为“实现类”层次结构（实现部分）。  

对于跨平台图像浏览系统的操作系统和图像文件格式两个维度，如果这样设计：
```python
from abc import ABC
class Image(ABC):
    pass
class JPGImage(Image):
    pass
class GIFImage(Image):
    pass
class WindowsJPGImage(JPGImage):
    pass
class LinuxJPGImage(JPGImage):
    pass
class WindowsGIFImage(JPGImage):
    pass
class LinuxGIFImage(JPGImage):
    pass
```
这种多层继承结构，类的数量极多，且扩展麻烦，会导致类的数量大量增大。  
采用桥接模式，将操作系统和图像文件格式两个维度分离，使它们可以独立改变：
```python
from abc import ABC, abstractmethod
class Image(ABC):
    def __init__(self, imp=None):
        self.imp = imp
    def parseFile(self, file_name):
        pass
class JPGImage(Image):
    def parseFile(self, file_name):
        self.imp.doPaint()
        print("This is JPG")
class GIFImage(Image):
    def parseFile(self, file_name):
        self.imp.doPaint()
        print("This is GIF")

class ImageImp(ABC):
    @abstractmethod
    def doPaint(self):
        pass
class WindowsImageImp(ImageImp):
    def doPaint(self):
        print("This is Windows")
class LinuxImageImp(ImageImp):
    def doPaint(self):
        print("This is Linux")

if __name__ == '__main__':
    imp = LinuxImageImp()  # 可从配置文件获得
    image = JPGImage()  # 可从配置文件获得
    image.imp = imp
    image.parseFile("xxx.jpg")
```
桥接模式和适配器模式用于设计的不同阶段，桥接模式用于系统的初步设计，对于存在两个独立变化维度的类可以将其分为抽象化和实现化两个角色，
使它们可以分别进行变化；而在初步设计完成之后，当发现系统与已有类无法协同工作时，可以采用适配器模式。  

### 优点
 - 分离抽象接口及其实现部分。抽象和实现不再在同一个继承层次结构中，而是“子类化”它们，使它们各自都具有自己的子类，以便任何组合子类，从而获得多维度组合对象。
 - 在很多情况下，桥接模式可以取代多层继承方案，多层继承方案违背了“单一职责原则”，复用性较差，且类的个数非常多，桥接模式极大减少了子类的个数。
 - 提高了系统的可扩展性，在两个变化维度中任意扩展一个维度，都不需要修改原有系统，符合“开闭原则”。
### 缺点
 - 增加系统的理解与设计难度，由于关联关系建立在抽象层，要求开发者一开始就针对抽象层进行设计与编程。
 - 要求正确识别出系统中两个独立变化的维度。
### 适用场景
 - 一个系统需要在抽象化和具体化之间增加更多的灵活性，避免在两个层次之间建立静态的继承关系。
 - “抽象部分”和“实现部分”可以以继承的方式独立扩展而互不影响，在程序运行时可以动态将一个抽象化子类的对象和一个实现化子类的对象进行组合，
即系统需要对抽象化角色和实现化角色进行动态耦合。
 - 一个类存在两个（或多个）独立变化的维度，且这两个（或多个）维度都需要独立进行扩展。

## 3.3 组合模式
对于树形结构，当容器对象（如文件夹）的某一个方法被调用时，将遍历整个树形结构，寻找也包含这个方法的成员对象（可以是容器对象，也可以是叶子对象）
并调用执行，牵一而动百，其中使用了递归调用的机制来对整个结构进行处理。由于容器对象和叶子对象在功能上的区别，
在使用这些对象的代码中必须有区别地对待容器对象和叶子对象，而实际上大多数情况下我们希望一致地处理它们，
因为对于这些对象的区别对待将会使得程序非常复杂。组合模式为解决此类问题而诞生，它可以让叶子对象和容器对象的使用具有一致性。  
### 角色
 - 抽象构件：可以是接口或抽象类，为叶子构件和容器构件对象声明接口，在该角色中可以包含所有子类共有行为的声明和实现。
在抽象构件中定义了访问及管理它的子构件的方法，如增加子构件、删除子构件、获取子构件等。
 - 叶子构件：表示叶子节点对象，叶子节点没有子节点，它实现了在抽象构件中定义的行为。
 - 容器构件：容器节点对象，容器节点包含子节点，其子节点可以是叶子节点，也可以是容器节点，它提供一个集合用于存储子节点，
实现了在抽象构件中定义的行为，包括那些访问及管理子构件的方法，在其业务方法中可以递归调用其子节点的业务方法。  
 
组合模式的关键是定义了一个抽象构件类，它既可以代表叶子，又可以代表容器，而客户端针对该抽象构件类进行编程，无须知道它到底表示的是叶子还是容器，
可以对其进行统一处理。  

```python
from abc import ABC, abstractmethod
class AbstractFile(ABC):
    @abstractmethod
    def add(self, file):
        pass
    @abstractmethod
    def remove(self, file):
        pass
    @abstractmethod
    def getChild(self, i):
        pass
    @abstractmethod
    def killVirus(self):
        pass

class ImageFile(AbstractFile):
    def __init__(self, name):
        self.name = name
    def add(self, file):
        print("do not support this method")
    def remove(self, file):
        print("do not support this method")
    def getChild(self, i):
        print("do not support this method")
    def killVirus(self):
        print("Killing virus in %s" % self.name)

class VideoFile(AbstractFile):
    def __init__(self, name):
        self.name = name
    def add(self, file):
        print("do not support this method")
    def remove(self, file):
        print("do not support this method")
    def getChild(self, i):
        print("do not support this method")
    def killVirus(self):
        print("Killing virus in %s" % self.name)

class Folder(AbstractFile):
    def __init__(self, name, file_list):
        self.name = name
        self.file_list = file_list
    
    def add(self, file):
        self.file_list.add(file)
    
    def remove(self, file):
        self.file_list.remove(file)
    
    def getChild(self, i):
        return self.file_list.get(i)
    
    def killVirus(self):
        for file in self.file_list:
            file.killVirus()
```
由于在本实例中使用了组合模式，在抽象构件类中声明了所有方法，包括用于管理和访问子构件的方法，如add()方法和remove()方法等，
因此在ImageFile等叶子构件类中实现这些方法时必须进行相应的异常处理或错误提示。
在容器构件类Folder的killVirus()方法中将递归调用其成员对象的killVirus()方法，从而实现对整个树形结构的遍历。  
在增加新的文件类型时，无须修改现有类库代码，只需增加一个新的文件类作为AbstractFile类的子类即可。  

但是由于在AbstractFile中声明了大量用于管理和访问成员构件的方法，例如add()、remove()等方法，我们不得不在新增的文件类中实现这些方法，
提供对应的错误提示和异常处理。为了简化代码，我们有以下两个解决方案：  
1. 将叶子构件的add()、remove()等方法的实现代码移至AbstractFile类中，由AbstractFile提供统一的默认实现。
透明组合模式中，抽象构件Component中声明了所有用于管理成员对象的方法，包括add()、remove()以及getChild()等方法，
这样做的好处是确保所有的构件类都有相同的接口。在客户端看来，叶子对象与容器对象所提供的方法是一致的，客户端可以相同地对待所有的对象。
缺点是不够安全，因为叶子对象和容器对象在本质上是有区别的。叶子对象不可能有下一个层次的对象，即不可能包含成员对象，因此为其提供add()、remove()以及getChild()等方法是没有意义的，这在编译阶段不会出错，但在运行阶段如果调用这些方法可能会出错（如果没有提供相应的错误处理代码）。

2. 在抽象构件AbstractFile中不声明任何用于访问和管理成员构件的方法，只有killVirus方法。 安全组合模式中，在抽象构件Component中没有声明任何用于管理成员对象的方法，而是在Composite类中声明并实现这些方法。这种做法是安全的，
因为根本不向叶子对象提供这些管理成员对象的方法，对于叶子对象，客户端不可能调用到这些方法。缺点是不够透明，因为叶子构件和容器构件具有不同的方法，且容器构件中那些用于管理成员对象的方法没有在抽象构件类中定义，
因此客户端不能完全针对抽象编程，必须有区别地对待叶子构件和容器构件。  
### 优点
 - 清楚地定义分层次的复杂对象，表示对象的全部或部分层次，它让客户端忽略了层次的差异，方便对整个层次结构进行控制。
 - 客户端可以一致地使用一个组合结构或其中单个对象，不必关心处理的是单个对象还是整个组合结构，简化了客户端代码。
 - 增加新的容器构件和叶子构件都很方便，无须对现有类库进行任何修改，符合“开闭原则”。
 - 组合模式为树形结构的面向对象实现提供了一种灵活的解决方案，通过叶子对象和容器对象的递归组合，可以形成复杂的树形结构，但对树形结构的控制却非常简单。  
### 缺点
 - 在增加新构件时很难对容器中的构件类型进行限制。有时候我们希望一个容器中只能有某些特定类型的对象，例如在某个文件夹中只能包含文本文件，使用组合模式时，不能依赖类型系统来施加这些约束，因为它们都来自于相同的抽象层，在这种情况下，必须通过在运行时进行类型检查来实现，这个实现过程较为复杂。
### 适用场景
 - 在具有整体和部分的层次结构中，希望通过一种方式忽略整体与部分的差异，客户端可以一致地对待它们。
 - 在一个使用面向对象语言开发的系统中需要处理一个树形结构。
 - 在一个系统中能够分离出叶子对象和容器对象，而且它们的类型不固定，需要增加一些新的类型。

## 3.4 装饰模式
装饰模式可以在不改变一个对象本身功能的基础上给对象增加额外的新行为，在现实生活中，这种情况也到处存在，例如一张照片，我们可以不改变照片本身，
给它增加一个相框，使得它具有防潮的功能，而且用户可以根据需要给它增加不同类型的相框，甚至可以在一个小相框的外面再套一个大相框。  

装饰模式是一种用于替代继承的技术，它通过一种无须定义子类的方式来给对象动态增加职责，使用对象之间的关联关系取代类之间的继承关系。
在装饰模式中引入了装饰类，在装饰类中既可以调用待装饰的原有类的方法，还可以增加新的方法，以扩充原有类的功能。  

### 角色
 - 抽象构件：具体构件和抽象装饰类的共同父类，声明了在具体构件中实现的业务方法，它的引入可以使客户端以一致的方式处理未被装饰的对象以及装饰之后的对象，
实现客户端的透明操作。
 - 具体构件：抽象构件类的子类，用于定义具体的构件对象，实现了在抽象构件中声明的方法，装饰器可以给它增加额外的职责（方法）。
 - 抽象装饰类：也是抽象构件类的子类，用于给具体构件增加职责，但是具体职责在其子类中实现。它维护一个指向抽象构件对象的引用，通过该引用可以调用装饰之前构件对象的方法，并通过其子类扩展该方法，以达到装饰的目的。
 - 抽象装饰类的子类，负责向构件添加新的职责。每一个具体装饰类都定义了一些新的行为，它可以调用在抽象装饰类中定义的方法，并可以增加新的方法用以扩充对象的行为。
```python
from abc import ABC,abstractmethod
class Component(ABC):
    @abstractmethod
    def operation(self):
        pass

class ConcreteComponent(Component):
    def operation(self):
        pass

class Decorator(Component):
    
    def __init__(self, component):
        self.component = component
    
    def operation(self):
        self.component.operation()

class ConcreteDecorator(Decorator):
    def __init__(self, component):
        super().__init__(component)
    
    def addedBehavior(self):
        # do something
        pass
        
    def operation(self):
        super().operation()
        self.addedBehavior()
```

### 优点
 - 对于扩展一个对象的功能，装饰模式比继承更加灵活性，不会导致类的个数急剧增加。
 - 可以通过一种动态的方式来扩展一个对象的功能，通过配置文件可以在运行时选择不同的具体装饰类，从而实现不同的行为。
 - 可以对一个对象进行多次装饰，通过使用不同的具体装饰类以及这些装饰类的排列组合，可以创造出很多不同行为的组合，得到功能更为强大的对象。
 - 具体构件类与具体装饰类可以独立变化，用户可以根据需要增加新的具体构件类和具体装饰类，原有类库代码无须改变，符合“开闭原则”。
### 缺点
 - 使用装饰模式进行系统设计时将产生很多小对象，这些对象的区别在于它们之间相互连接的方式有所不同，而不是它们的类或者属性值有所不同，大量小对象的产生势必会占用更多的系统资源，在一定程序上影响程序的性能。
 - 装饰模式提供了一种比继承更加灵活机动的解决方案，但同时也意味着比继承更加易于出错，排错也很困难，对于多次装饰的对象，调试时寻找错误可能需要逐级排查，较为繁琐。
### 适用场景
 - 在不影响其他对象的情况下，以动态、透明的方式给单个对象添加职责。
 - 当不能采用继承的方式对系统进行扩展或者采用继承不利于系统扩展和维护时可以使用装饰模式。

## 3.5 外观模式
在软件开发中，有时候为了完成一项较为复杂的功能，一个客户类需要和多个业务类交互，而这些需要交互的业务类经常会作为一个整体出现，
由于涉及到的类比较多，导致使用时代码较为复杂，此时，特别需要一个类似服务员一样的角色，由它来负责和多个业务类进行交互，
而客户类只需与该类交互。外观模式通过引入一个新的外观类(Facade)来实现该功能，外观类充当了软件系统中的“服务员”，
它为多个业务类的调用提供了一个统一的入口，简化了类与类之间的交互。在外观模式中，那些需要交互的业务类被称为子系统(Subsystem)。  

外观模式：为子系统中的一组接口提供一个统一的入口。外观模式定义了一个高层接口，这个接口使得这一子系统更加容易使用。  

### 角色
 - 外观角色：在客户端可以调用它的方法，在外观角色中可以知道相关的（一个或者多个）子系统的功能和责任；在正常情况下，
它将所有从客户端发来的请求委派到相应的子系统去，传递给相应的子系统对象处理。
 - 子系统角色：在软件系统中可以有一个或者多个子系统角色，每一个子系统可以不是一个单独的类，而是一个类的集合，它实现子系统的功能；
每一个子系统都可以被客户端直接调用，或者被外观角色调用，它处理由外观类传过来的请求；子系统并不知道外观的存在，对于子系统而言，
外观角色仅仅是另外一个客户端而已。  

```python
class SubSystemA:
    def methodA(self):
        pass
class SubSystemB:
    def methodB(self):
        pass

class Facade:
    def __init__(self):
        self.obj1 = SubSystemA()
        self.obj2 = SubSystemB()
    def method(self):
        self.obj1.methodA()
        self.obj2.methodB()

if __name__ == '__main__':
    Facade().method()
```
### 优点
 - 对客户端屏蔽了子系统组件，减少了客户端所需处理的对象数目，并使得子系统使用起来更加容易
 - 实现了子系统与客户端之间的松耦合关系，这使得子系统的变化不会影响到调用它的客户端，只需要调整外观类即可。
 - 一个子系统的修改对其他子系统没有任何影响，而且子系统内部变化也不会影响到外观对象。

### 缺点
 - 增加新的子系统可能需要修改外观类的源代码，违背了开闭原则。

### 适用场景
 - 当要为访问一系列复杂的子系统提供一个简单入口时可以使用外观模式。
 - 客户端程序与多个子系统之间存在很大的依赖性。引入外观类可以将子系统与客户端解耦，从而提高子系统的独立性和可移植性。

## 3.6 享元模式
享元模式通过共享技术实现相同或相似对象的重用，在逻辑上每一个出现的字符都有一个对象与之对应，然而在物理上它们却共享同一个享元对象，
这个对象可以出现在一个字符串的不同地方，相同的字符对象都指向同一个实例，在享元模式中，存储这些共享实例对象的地方称为享元池(Flyweight Pool)。
我们可以针对每一个不同的字符创建一个享元对象，将其放在享元池中，需要时再从享元池取出。  
享元模式以共享的方式高效地支持大量细粒度对象的重用，享元对象能做到共享的关键是区分了内部状态(Intrinsic State)和外部状态(Extrinsic State)。  
 - 内部状态是存储在享元对象内部并且不会随环境改变而改变的状态，内部状态可以共享。如字符的内容，不会随外部环境的变化而变化，无论在任何环境下字符“a”始终是“a”，都不会变成“b”。  
 - 外部状态是随环境改变而改变的、不可以共享的状态。享元对象的外部状态通常由客户端保存，并在享元对象被创建之后，需要使用的时候再传入到享元对象内部。一个外部状态与另一个外部状态之间是相互独立的。如字符的颜色，可以在不同的地方有不同的颜色，例如有的“a”是红色的，有的“a”是绿色的，字符的大小也是如此，有的“a”是五号字，有的“a”是四号字。而且字符的颜色和大小是两个独立的外部状态，它们可以独立变化，相互之间没有影响，客户端可以在使用时将外部状态注入享元对象中。  

享元模式(Flyweight Pattern)：运用共享技术有效地支持大量细粒度对象的复用。系统只使用少量的对象，而这些对象都很相似，状态变化很小，可以实现对象的多次复用。  

### 角色
 - 抽象享元类：通常是一个接口或抽象类，在抽象享元类中声明了具体享元类公共的方法，这些方法可以向外界提供享元对象的内部数据（内部状态），同时也可以通过这些方法来设置外部数据（外部状态）。  
 - 具体享元类：实现了抽象享元类，其实例称为享元对象；在具体享元类中为内部状态提供了存储空间。通常我们可以结合单例模式来设计具体享元类，为每一个具体享元类提供唯一的享元对象。
 - 非共享具体享元类：并不是所有的抽象享元类的子类都需要被共享，不能被共享的子类可设计为非共享具体享元类；当需要一个非共享具体享元类的对象时可以直接通过实例化创建。
 - 享元工厂类：用于创建并管理享元对象，它针对抽象享元类编程，将各种类型的具体享元对象存储在一个享元池中，享元池一般设计为一个存储“键值对”的集合（也可以是其他类型的集合），可以结合工厂模式进行设计；当用户请求一个具体享元对象时，享元工厂提供一个存储在享元池中已创建的实例或者创建一个新的实例（如果不存在的话），返回新创建的实例并将其存储在享元池中。

```python
import random
from abc import ABC, abstractmethod


class Shape(ABC):
    @abstractmethod
    def draw(self):
        pass


class Circle(Shape):
    def __init__(self, color, x=None, y=None):
        self.x = x
        self.y = y
        self.color = color

    def draw(self):
        print("Draw Circle %s %s %s" % (str(self.x), str(self.y), self.color))


class ShapeFactory:
    def __init__(self):
        self.circle_map = {}
    
    def get_circle(self, color):
        circle = self.circle_map.get(color)
        if not circle:
            circle = Circle(color)
            self.circle_map[color] = circle
        return circle


if __name__ == '__main__':
    colors = ['red', 'yellow', 'blue']  # 最多创建3个对象
    factory = ShapeFactory()
    for i in range(20):
        color = colors[random.randint(0, 2)]
        circle = factory.get_circle(color)
        circle.x = random.randint(-100, 100)
        circle.y = random.randint(-100, 100)
        circle.draw()
```
### 优点
 - 极大减少内存中对象的数量，使得相同或相似对象在内存中只保存一份，从而可以节约系统资源，提高系统性能。
 - 外部状态相对独立，而且不会影响其内部状态，从而使得享元对象可以在不同的环境中被共享。
### 缺点
 - 享元模式使得系统变得复杂，需要分离出内部状态和外部状态，这使得程序的逻辑复杂化。
### 适用场景
 - 一个系统有大量相同或者相似的对象，造成内存的大量耗费。
 - 对象的大部分状态都可以外部化，可以将这些外部状态传入对象中。
 - 在使用享元模式时需要维护一个存储享元对象的享元池，而这需要耗费一定的系统资源，因此，应当在需要多次重复使用享元对象时才值得使用享元模式。

## 3.7 代理模式
由于某些原因，客户端不想或不能直接访问一个对象，此时可以通过一个称之为“代理”的第三者来实现间接访问，该方案对应的设计模式被称为代理模式。  
代理模式：给某一个对象提供一个代理或占位符，并由代理对象来控制对原对象的访问。  

### 角色
 - 抽象主题角色：声明了真实主题和代理主题的共同接口，这样一来在任何使用真实主题的地方都可以使用代理主题，客户端通常需要针对抽象主题角色进行编程。
 - 代理主题角色：包含了对真实主题的引用，从而可以在任何时候操作真实主题对象；在代理主题角色中提供一个与真实主题角色相同的接口，
以便在任何时候都可以替代真实主题；代理主题角色还可以控制对真实主题的使用，负责在需要的时候创建和删除真实主题对象，并对真实主题对象的使用加以约束。
通常，在代理主题角色中，客户端在调用所引用的真实主题操作之前或之后还需要执行其他操作，而不仅仅是单纯调用真实主题对象中的操作。　
 - 真实主题角色：定义了代理角色所代表的真实对象，在真实主题角色中实现了真实的业务操作，客户端可以通过代理主题角色间接调用真实主题角色中定义的操作。  

我们将创建一个 Image 接口和实现 Image 接口的具体类。ProxyImage 是一个代理类，用于减少 RealImage 对象加载的内存占用。
```python
from abc import ABC, abstractmethod

class Image(ABC):
    @abstractmethod
    def display(self):
        pass

class RealImage(Image):
    
    def __init__(self, file_name=None):
        self.file_name = file_name
        
    def load_from_disk(self):
        print("Load %s" % self.file_name)
    
    def display(self):
        print("Display %s" % self.file_name)

class ProxyImage(Image):
    
    def __init__(self, file_name=None):
        self.real_image = None
        self.file_name = file_name
    
    def display(self):
        if not self.real_image:
            self.real_image = RealImage(self.file_name)
        self.real_image.display()

if __name__ == '__main__':
    image = ProxyImage("test.jpg")
    image.display()
    image.display()
```

### 优点
 - 你可以在客户端毫无察觉的情况下控制服务对象。
 - 如果客户端对服务对象的生命周期没有特殊要求， 你可以对生命周期进行管理。
 - 即使服务对象还未准备好或不存在， 代理也可以正常工作。
 - 开闭原则。你可以在不对服务或客户端做出修改的情况下创建新代理。
### 缺点
 - 由于在客户端和真实主题之间增加了代理对象，因此有些类型的代理模式可能会造成请求的处理速度变慢。
 - 代码可能会变得复杂， 因为需要新建许多类。
### 适用场景
 - 延迟初始化（虚拟代理）。如果你有一个偶尔使用的重量级服务对象，一直保持该对象运行会消耗系统资源时，可使用代理模式。你无需在程序启动时就创建该对象，可将对象的初始化延迟到真正有需要的时候。
 - 访问控制 （保护代理）。如果你只希望特定客户端使用服务对象，这里的对象可以是操作系统中非常重要的部分，而客户端则是各种已启动的程序（包括恶意程序），此时可使用代理模式。代理可仅在客户端凭据满足要求时将请求传递给服务对象。
 - 本地执行远程服务 （远程代理）。适用于服务对象位于远程服务器上的情形。在这种情形中， 代理通过网络传递客户端请求， 负责处理所有与网络相关的复杂细节。
 - 记录日志请求 （日志记录代理）。适用于当你需要保存对于服务对象的请求历史记录时。 代理可以在向服务传递请求前进行记录。
 - 缓存请求结果 （缓存代理）。适用于需要缓存客户请求结果并对缓存生命周期进行管理时， 特别是当返回结果的体积非常大时。
 - 智能引用。可在没有客户端使用某个重量级对象时立即销毁该对象。代理会将所有获取了指向服务对象或其结果的客户端记录在案。代理会时不时地遍历各个客户端，检查它们是否仍在运行。如果相应的客户端列表为空，代理就会销毁该服务对象，释放底层系统资源。

### 代理模式和装饰模式的区别
 - 两者都是对类的方法进行增强，但装饰器模式强调的是增强自身，在被装饰之后你能够够在被增强的类上使用增强后的方法。增强过后还是你，只不过能力变强了。而代理模式则强调要别人帮你去做一些本身与你业务没有太多关系的职责。代理模式是为了实现对象的控制，因为被代理的对象往往难以直接获得或者是其内部不想暴露出来。  
 - 装饰模式是以对客户端透明的方式扩展对象的功能，是继承方案的一个替代方案；代理模式则是给一个对象提供一个代理对象，并由代理对象来控制对原有对象的引用；
 - 装饰模式是为装饰的对象增强功能；而代理模式对代理的对象施加控制，但不对对象本身的功能进行增强；  

# 4 行为型模式
## 4.1 职责链模式
职责链可以是一条直线、一个环或者一个树形结构，最常见的职责链是直线型，即沿着一条单向的链来传递请求。
链上的每一个对象都是请求处理者，职责链模式可以将请求的处理者组织成一条链，并让请求沿着链传递，由链上的处理者对请求进行相应的处理，
客户端无须关心请求的处理细节以及请求的传递，只需将请求发送到链上即可，实现请求发送者和请求处理者解耦。  

职责链模式(Chain of Responsibility Pattern)：避免请求发送者与接收者耦合在一起，让多个对象都有可能接收请求，将这些对象连接成一条链，
并且沿着这条链传递请求，直到有对象处理它为止。  

### 角色
 - 抽象处理者：义了一个处理请求的接口，一般设计为抽象类，由于不同的具体处理者处理请求的方式不同，因此在其中定义了抽象请求处理方法。
因为每一个处理者的下家还是一个处理者，因此在抽象处理者中定义了一个抽象处理者类型的对象（如结构图中的successor），作为其对下家的引用。
通过该引用，处理者可以连成一条链。  
 - 具体处理者：抽象处理者的子类，可以处理用户请求，在具体处理者类中实现了抽象处理者中定义的抽象请求处理方法，在处理请求之前需要进行判断，
看是否有相应的处理权限，如果可以处理请求就处理它，否则将请求转发给后继者；在具体处理者中可以访问链中下一个对象，以便请求的转发。  

```python
from abc import ABC, abstractmethod

class Handler(ABC):
    
    @abstractmethod
    def set_next(self, handler):
        pass
    
    @abstractmethod
    def handle(self, request):
        pass

class AbstractHandler(Handler):
    
    _next_handler = None
    
    def set_next(self, handler):
        self._next_handler = handler    
        return handler
    
    @abstractmethod
    def handle(self, request):
        if self._next_handler:
            return self._next_handler.handle(request)
        return None

class MonkeyHandler(AbstractHandler):
    def handle(self, request):
        if request == "Banana":
            return "Monkey: I'll eat the %s" % request
        return super().handle(request)

class SquirrelHandler(AbstractHandler):
    def handle(self, request):
        if request == "Nut":
            return "Squirrel: I'll eat the %s" % request
        return super().handle(request)

class DogHandler(AbstractHandler):
    def handle(self, request):
        if request == "Meat":
            return "Dog: I'll eat the %s" % request
        return super().handle(request)

def client_code(handler: Handler) -> None:
    """
    The client code is usually suited to work with a single handler. In most
    cases, it is not even aware that the handler is part of a chain.
    """

    for food in ["Nut", "Banana", "Cup of coffee"]:
        print(f"\nClient: Who wants a {food}?")
        result = handler.handle(food)
        if result:
            print(f"  {result}", end="")
        else:
            print(f"  {food} was left untouched.", end="")
            
if __name__ == '__main__':
    monkey = MonkeyHandler()
    squirrel = SquirrelHandler()
    dog = DogHandler()
    
    monkey.set_next(squirrel).set_next(dog)
    
    # Chain: monkey -> squirrel -> dog
    client_code(monkey)
    # Chain: squirrel -> dog
    client_code(squirrel)
```

### 优点
 - 可以灵活控制请求处理的顺序。
 - 单一职责原则。你可对发起操作和执行操作的类进行解耦。
 - 开闭原则。 你可以在不更改现有代码的情况下在程序中新增处理者。

### 缺点
 - 部分请求可能未被处理。

### 适用场景
 - 有多个对象可以处理同一个请求，具体哪个对象处理该请求待运行时刻再确定，客户端只需将请求提交到链上，而无须关心请求的处理对象是谁以及它是如何处理的。
 - 可动态指定一组对象处理请求，客户端可以动态创建职责链来处理请求，还可以改变链中处理者之间的先后次序。
 - 当必须按顺序执行多个处理者时， 可以使用该模式。

## 4.2 命令模式
命令模式可以将请求发送者和接收者完全解耦，发送者与接收者之间没有直接引用关系，发送请求的对象只需要知道如何发送请求，而不必知道如何完成请求。  
### 角色
 - 抽象命令类：声明了用于执行请求的execute()等方法，通过这些方法可以调用请求接收者的相关操作。
 - 具体命令类：实现了在抽象命令类中声明的方法，它对应具体的接收者对象，将接收者对象的动作绑定其中。在实现execute()方法时，将调用接收者对象的相关操作(Action)。
 - 调用者：调用者即请求发送者，在程序运行时可以将一个具体命令对象注入其中，再调用具体命令对象的execute()方法，从而实现间接调用请求接收者的相关操作。  
 - 接收者：接收者执行与请求相关的操作，它具体实现对请求的业务处理。绝大部分命令只处理如何将请求传递到接收者的细节， 接收者自己会完成实际的工作。

命令模式的本质是对请求进行封装，一个请求对应于一个命令，将发出命令的责任和执行命令的责任分割开。  
```python
from abc import ABC, abstractmethod
class Command(ABC):
    @abstractmethod
    def execute(self):
        pass

class ConcreteCommand(Command):
    
    receiver = None
    
    def execute(self):
        self.receiver.action()

class Invoker:
    command = None
    
    def __init__(self, command=None):
        self.command = command
    
    def call(self):
        self.command.execute()
    

class Receiver:
    
    def action(self):
        # do something
        pass
```
每一个具体命令类(ConcreteCommand)对应一个请求的处理者（接收者Receiver），
通过向请求发送者(Invoker)注入不同的具体命令对象(ConcreteCommand)可以使得相同的发送者(Invoker)对应不同的接收者(接收者Receiver)，
从而实现“将一个请求封装为一个对象，用不同的请求对客户进行参数化”，客户端只需要将具体命令对象作为参数注入请求发送者，无须直接操作请求的接收者。  

有时候我们需要将多个请求排队，当一个请求发送者发送一个请求时，将不止一个请求接收者产生响应，这些请求接收者将逐个执行业务方法，完成对请求的处理。
此时，我们可以通过命令队列来实现。  
最常用、灵活性最好的一种方式是增加一个CommandQueue类，由该类来负责存储多个命令对象，而不同的命令对象可以对应不同的请求接收者。  
```python
class CommandQueue:
    
    commands = list()
    
    def addCommand(self, cmd):
        self.commands.append(cmd)
    
    def removeCommand(self, cmd):
        self.commands.remove(cmd)
    
    def execute(self):
        for cmd in self.commands:
            cmd.execute()

# 在增加了命令队列类CommandQueue以后，请求发送者类Invoker将针对CommandQueue编程
class Invoker:
    
    command_queue = None
    
    def __init__(self, command_queue=None):
        self.command_queue = command_queue
    
    def call(self):
        self.command_queue.execute()
```
命令队列与我们常说的“批处理”有点类似。批处理，顾名思义，可以对一组对象（命令）进行批量处理，当一个发送者发送请求后，
将有一系列接收者对请求作出响应，命令队列可以用于设计批处理应用程序，如果请求接收者的接收次序没有严格的先后次序，
我们还可以使用多线程技术来并发调用命令对象的execute()方法，从而提高程序的执行效率。  

在命令模式中，我们可以通过调用一个命令对象的execute()方法来实现对请求的处理，如果需要撤销(Undo)请求，可通过在命令类中增加一个逆向操作来实现。
即在Command抽象类加一个undo方法，ConcreteCommand实现这个方法。  

请求日志就是将请求的历史记录保存下来，通常以日志文件(Log File)的形式永久存储在计算机中。日志文件可以为系统提供一种恢复机制，
在请求日志文件中可以记录用户对系统的每一步操作，从而让系统能够顺利恢复到某一个特定的状态；请求日志也可以用于实现批处理，
在一个请求日志文件中可以存储一系列命令对象，例如一个命令队列。  
在实现请求日志时，我们可以将命令对象通过序列化写到日志文件中。（pickle in Python）  

宏命令(Macro Command)又称为组合命令，它是组合模式和命令模式联用的产物。宏命令是一个具体命令类，它拥有一个集合属性，
在该集合中包含了对其他命令对象的引用。通常宏命令不直接与请求接收者交互，而是通过它的成员来调用接收者的方法。当调用宏命令的execute()方法时，
将递归调用它所包含的每个成员命令的execute()方法，一个宏命令的成员可以是简单命令，还可以继续是宏命令。执行一个宏命令将触发多个具体命令的执行，
从而实现对命令的批处理。  

### 优点
 - 单一职责原则。 你可以解耦触发和执行操作的类。
 - 开闭原则。 你可以在不修改已有客户端代码的情况下在程序中创建新的命令。
 - 为请求的撤销(Undo)和恢复(Redo)操作提供了一种设计和实现方案。
 - 可以比较容易地设计一个命令队列或宏命令（组合命令）。

### 缺点
 - 使用命令模式可能会导致某些系统有过多的具体命令类。

### 适用场景
 - 需要通过操作来参数化对象，客户端只需要将具体命令对象作为参数注入请求发送者，无须直接操作请求的接收者。
 - 系统需要支持命令的撤销(Undo)操作和恢复(Redo)操作。
 - 系统需要将一组操作组合在一起形成宏命令。

## 4.3 解释器模式
在某些情况下，为了更好地描述某一些特定类型的问题，我们可以创建一种新的语言，这种语言拥有自己的表达式和结构，即文法规则，
这些问题的实例将对应为该语言中的句子。此时，可以使用解释器模式来设计这种新的语言。  
解释器模式(Interpreter Pattern)：定义一个语言的文法，并且建立一个解释器来解释该语言中的句子，这里的“语言”是指使用规定格式和语法的代码。
解释器模式是一种类行为型模式。  
### 角色
 - 抽象表达式：声明了抽象的解释操作，它是所有终结符表达式和非终结符表达式的公共父类。
 - 终结符表达式：实现了与文法中的终结符相关联的解释操作，在句子中的每一个终结符都是该类的一个实例。
 - 非终结符表达式：实现了文法中非终结符的解释操作，由于在非终结符表达式中可以包含终结符表达式，也可以继续包含非终结符表达式，因此其解释操作一般通过递归的方式来完成。
 - 环境类：又称为上下文类，它用于存储解释器之外的一些全局信息，通常它临时存储了需要解释的语句。

```python
from abc import ABC, abstractmethod

class AbstractExpression(ABC):
    @abstractmethod
    def interpret(self, context):
        pass

class TerminalExpression(AbstractExpression):
    def interpret(self, context):
        # do sth.
        pass
    
# 非终结符表达式，其代码相对比较复杂，因为可以通过非终结符将表达式组合成更加复杂的结构，对于包含两个操作元素的非终结符表达式类
class NonterminalExpression(AbstractExpression):
    
    def __init__(self, left=None, right=None):
        self.left = left
        self.right = right
    
    def interpret(self, context):
        # 递归调用每一个组成部分的interpret()方法
        # 在递归调用时指定组成部分的连接方式，即非终结符的功能
        pass

class Context:
    map = None  # 存储一系列公共信息
    def assign(self, key, value):
        # 往环境类中设值
        pass
    
    def lookup(self, key):
        # 获取存储在环境类中的值
        pass
```
### 优点
 - 易于改变和扩展文法。
 - 增加新的解释表达式较为方便。如果用户需要增加新的解释表达式只需要对应增加一个新的终结符表达式或非终结符表达式类，原有表达式类代码无须修改，符合“开闭原则”。
### 缺点
 - 对于复杂文法难以维护。在解释器模式中，每一条规则至少需要定义一个类，因此如果一个语言包含太多文法规则，类的个数将会急剧增加，导致系统难以管理和维护。
 - 执行效率较低。由于在解释器模式中使用了大量的循环和递归调用，因此在解释较为复杂的句子时其速度很慢，而且代码的调试过程也比较麻烦。
### 适用场景
 - 可以将一个需要解释执行的语言中的句子表示为一个抽象语法树。
 - 一些重复出现的问题可以用一种简单的语言来进行表达。
 - 执行效率不是关键问题。【注：高效的解释器通常不是通过直接解释抽象语法树来实现的，而是需要将它们转换成其他形式，使用解释器模式的执行效率并不高。】

## 4.4 迭代器模式
在软件开发中，存在大量类似电视机一样的类，它们可以存储多个成员对象（元素），这些类通常称为聚合类(Aggregate Classes)，
对应的对象称为聚合对象。为了更加方便地操作这些聚合对象，同时可以很灵活地为聚合对象增加不同的遍历方法，我们也需要类似电视机遥控器一样的角色，
可以访问一个聚合对象中的元素但又不需要暴露它的内部结构。  

若聚合类的职责过重，它既负责存储和管理数据，又负责遍历数据，违反了“单一职责原则”，
将聚合类中负责遍历数据的方法提取出来，封装到专门的类中，实现数据存储和数据遍历分离，无须暴露聚合类的内部属性即可对其进行操作，
而这正是迭代器模式的意图所在。  

迭代器模式(Iterator Pattern)：提供一种方法来访问聚合对象，而不用暴露这个对象的内部表示，其别名为游标(Cursor)。  

### 角色
 - 抽象迭代器：定义了访问和遍历元素的接口，声明了用于遍历数据元素的方法，例如：用于获取第一个元素的first()方法，用于访问下一个元素的next()方法，用于判断是否还有下一个元素的hasNext()方法，用于获取当前元素的currentItem()方法等，在具体迭代器中将实现这些方法。
 - 具体迭代器：实现了抽象迭代器接口，完成对聚合对象的遍历，同时在具体迭代器中通过游标来记录在聚合对象中所处的当前位置，在具体实现时，游标通常是一个表示位置的非负整数。
 - 抽象聚合类：用于存储和管理元素对象，声明一个createIterator()方法用于创建一个迭代器对象，充当抽象迭代器工厂角色。
 - 具体聚合类：实现了在抽象聚合类中声明的createIterator()方法，该方法返回一个与该具体聚合类对应的具体迭代器ConcreteIterator实例。

```python
from __future__ import annotations
from collections.abc import Iterable, Iterator
from typing import Any, List


"""
To create an iterator in Python, there are two abstract classes from the built-
in `collections` module - Iterable,Iterator. We need to implement the
`__iter__()` method in the iterated object (collection), and the `__next__ ()`
method in theiterator.
"""


class AlphabeticalOrderIterator(Iterator):
    """
    Concrete Iterators implement various traversal algorithms. These classes
    store the current traversal position at all times.
    """

    """
    `_position` attribute stores the current traversal position. An iterator may
    have a lot of other fields for storing iteration state, especially when it
    is supposed to work with a particular kind of collection.
    """
    _position: int = None

    """
    This attribute indicates the traversal direction.
    """
    _reverse: bool = False

    def __init__(self, collection: WordsCollection, reverse: bool = False) -> None:
        self._collection = collection
        self._reverse = reverse
        self._position = -1 if reverse else 0

    def __next__(self):
        """
        The __next__() method must return the next item in the sequence. On
        reaching the end, and in subsequent calls, it must raise StopIteration.
        """
        try:
            value = self._collection[self._position]
            self._position += -1 if self._reverse else 1
        except IndexError:
            raise StopIteration()

        return value


class WordsCollection(Iterable):
    """
    Concrete Collections provide one or several methods for retrieving fresh
    iterator instances, compatible with the collection class.
    """

    def __init__(self, collection: List[Any] = []) -> None:
        self._collection = collection

    def __iter__(self) -> AlphabeticalOrderIterator:
        """
        The __iter__() method returns the iterator object itself, by default we
        return the iterator in ascending order.
        """
        return AlphabeticalOrderIterator(self._collection)

    def get_reverse_iterator(self) -> AlphabeticalOrderIterator:
        return AlphabeticalOrderIterator(self._collection, True)

    def add_item(self, item: Any):
        self._collection.append(item)


if __name__ == "__main__":
    # The client code may or may not know about the Concrete Iterator or
    # Collection classes, depending on the level of indirection you want to keep
    # in your program.
    collection = WordsCollection()
    collection.add_item("First")
    collection.add_item("Second")
    collection.add_item("Third")

    print("Straight traversal:")
    print("\n".join(collection))
    print("")

    print("Reverse traversal:")
    print("\n".join(collection.get_reverse_iterator()), end="")
```

### 优点
 - 支持以不同的方式遍历一个聚合对象，在同一个聚合对象上可以定义多种遍历方式。
 - 迭代器简化了聚合类。由于引入了迭代器，在原有的聚合对象中不需要再自行提供数据遍历等方法，这样可以简化聚合类的设计。
 - 在迭代器模式中，由于引入了抽象层，增加新的聚合类和迭代器类都很方便，无须修改原有代码，满足“开闭原则”的要求。
### 缺点
 - 由于迭代器模式将存储数据和遍历数据的职责分离，增加新的聚合类需要对应增加新的迭代器类，类的个数成对增加，这在一定程度上增加了系统的复杂性。
### 适用场景
 - 访问一个聚合对象的内容而无须暴露它的内部表示。将聚合对象的访问与内部数据的存储分离，使得访问聚合对象时无须了解其内部实现细节。
 - 需要为一个聚合对象提供多种遍历方式。
 
## 4.5 中介者模式
对象之间存在大量的多对多联系，将导致系统非常复杂，这些对象既会影响别的对象，也会被别的对象所影响，这些对象称为同事对象，
它们之间通过彼此的相互作用实现系统的行为。在网状结构中，几乎每个对象都需要与其他对象发生相互作用，
而这种相互作用表现为一个对象与另外一个对象的直接耦合，这将导致一个过度耦合的系统。  

中介者模式可以使对象之间的关系数量急剧减少，通过引入中介者对象，可以将系统的网状结构变成以中介者为中心的星形结构。  

如果在一个系统中对象之间存在多对多的相互关系，我们可以将对象之间的一些交互行为从各个对象中分离出来，并集中封装在一个中介者对象中，
并由该中介者进行统一协调，这样对象之间多对多的复杂关系就转化为相对简单的一对多关系。通过引入中介者来简化对象之间的复杂交互，
中介者模式是“迪米特法则”的一个典型应用。  

中介者模式(Mediator Pattern)：用一个中介对象（中介者）来封装一系列的对象交互，中介者使各对象不需要显式地相互引用，从而使其耦合松散，
而且可以独立地改变它们之间的交互。  

### 角色
 - 抽象中介者：该接口用于与各同事对象之间进行通信。
 - 具体中介者：抽象中介者的子类，通过协调各个同事对象来实现协作行为，它维持了对各个同事对象的引用。
 - 抽象同事类：定义各个同事类公有的方法，并声明了一些抽象方法来供子类实现，同时它维持了一个对抽象中介者类的引用，其子类可以通过该引用来与中介者通信。
 - 具体同事类：抽象同事类的子类；每一个同事对象在需要和其他同事对象通信时，先与中介者通信，通过中介者来间接完成与其他同事类的通信；在具体同事类中实现了在抽象同事类中声明的抽象方法。

```python
from abc import ABC,abstractmethod
class Mediator(ABC):
    
    colleagues = []
    
    def register(self, colleague):
        self.colleagues.append(colleague)
    
    @abstractmethod
    def operation(self):
        pass

class ConcreteMediator(Mediator):
    
    def operation(self):
        pass
        # 调用同事类的方法，并加入一些代码对调用进行控制
        # self.colleagues[0].method()

class Colleague(ABC):
    
    def __init__(self, mediator=None):    
        self.mediator = mediator
    
    @abstractmethod
    def method1(self):
        # 声明自身方法，处理自己的行为
        pass
    
    def method2(self):
        # 定义依赖方法，与中介者进行通信
        self.mediator.operation()

class ConcreteColleague(Colleague):
    
    def method1(self):
        pass
        # 实现自身方法
```
Component充当抽象同事类，Button、ListBox和TextBox充当具体同事类，Mediator充当抽象中介者类，ConcreteMediator充当具体中介者类，
ConcreteMediator维持了对具体同事类的引用。  
```python
from abc import ABC,abstractmethod
class Mediator(ABC):
    @abstractmethod
    def operation(self, component):
        pass

class ConcreteMediator(Mediator):
    
    def __init__(self, button, list_box, text_box):
        self.button = button
        self.list_box = list_box
        self.text_box = text_box
    
    def operation(self, component):
        if component == self.button:
            self.text_box.update()  # 单击按钮，提交文本框内容
        elif component == self.list_box:
            self.list_box.select()  # 在列表框中选中用户
            self.text_box.set_text() # 将选中的用户更新到文本框

class Component(ABC):

    def __init__(self, mediator=None):    
        self.mediator = mediator
    
    def changed(self):
        # 转发调用
        self.mediator.operation(self)

class Button(Component):
    pass

class ListBox(Component):
    def select(self):
        print("SELECT User Jack")

class TextBox(Component):
    def update(self):
        print("Update textbox content")
    
    def set_text(self):
        print("Set text")

if __name__ == '__main__':
    bt = Button()
    lb = ListBox()
    tb = TextBox()
    
    mediator = ConcreteMediator(bt, lb, tb)
    bt.mediator = mediator
    lb.mediator = mediator
    tb.mediator = mediator

    bt.changed()
    lb.changed()
```
### 优点
 - 简化了对象之间的交互，将各同事对象解耦。

### 缺点
 - 在具体中介者类中包含了大量同事之间的交互细节，可能会导致具体中介者类非常复杂，使得系统难以维护。

### 适用场景
 - 对象之间存在复杂的引用关系，系统结构混乱且难以理解。
 - 一个对象由于引用了其他很多对象并且直接和这些对象通信，导致难以复用该对象。
 - 想通过一个中间类来封装多个类中的行为，而又不想生成太多的子类。
 
## 4.6 备忘录模式
备忘录模式提供了一种状态恢复的实现机制，使得用户可以方便地回到一个特定的历史步骤，当新的状态无效或者存在问题时，可以使用暂时存储起来的备忘录将状态复原，当前很多软件都提供了撤销(Undo)操作，其中就使用了备忘录模式。  

备忘录模式(Memento Pattern)：在不破坏封装的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态，这样可以在以后将对象恢复到原先保存的状态。它是一种对象行为型模式，其别名为Token。  

### 角色
 - 原发器：一个普通类，可以创建一个备忘录，并存储它的当前内部状态，也可以使用备忘录来恢复其内部状态，一般将需要保存内部状态的类设计为原发器。
 - 备忘录：存储原发器的内部状态，根据原发器来决定保存哪些内部状态。
 - 负责人：负责人又称为管理者，它负责保存备忘录，但是不能对备忘录的内容进行操作或检查。

```python
from abc import ABC, abstractmethod
class Originator:
    
    def __init__(self):
        self.state = None

    def createMemento(self):
        return Memento(self)
    
    def restoreMemento(self, m):
        self.state = m.state
    
    def setState(self, state):
        self.state = state

    def getState(self):
        return self.state

class Memento:
    
    def __init__(self, originator):
        self.state = originator.getState()

    def setState(self, state):
        self.state = state

    def getState(self):
        return self.state

class Caretaker:
    
    def __init__(self):
        self.memento = None

    def getMemento(self):
        return self.memento
    
    def setMemento(self, memento):
        self.memento = memento
```
在设计备忘录类时需要考虑其封装性，除了Originator类，不允许其他类来调用备忘录类Memento的构造函数与相关方法。  
对于负责人类Caretaker，它用于保存备忘录对象，并提供getMemento()方法用于向客户端返回一个备忘录对象，原发器通过使用这个备忘录对象可以回到某个历史状态。  

可悔棋的象棋系统：
```python
class Chess:
    
    def __init__(self, label, x, y):
        self.label = label 
        self.x = x
        self.y = y
    
    def save(self):
        return Memento(self.label, self.x, self.y)
    
    def restore(self, memento):
        self.label = memento.label
        self.x = memento.x
        self.y = memento.y
        
class Memento:
    
    def __init__(self, label, x, y):
        self.label = label 
        self.x = x
        self.y = y

class Caretaker:
    
    def __init__(self):
        self.__memento = None
    
    def saveMemento(self, memento):
        self.__memento = memento
        
    def getMemento(self):
        return self.__memento


if __name__ == '__main__':
    caretaker = Caretaker()
    chess = Chess("车", 1, 1)
    caretaker.saveMemento(chess.save())
    chess.x = 2
    caretaker.saveMemento(chess.save())
    chess.y = 2
    # 悔棋
    chess.restore(caretaker.getMemento())
```

如何实现多次撤销呢？那就是在负责人类中定义一个集合来存储多个备忘录，每个备忘录负责保存一个历史状态，
在撤销时可以对备忘录集合进行逆向遍历，回到一个指定的历史状态，而且还可以对备忘录集合进行正向遍历，
实现重做(Redo)操作，即取消撤销，让对象状态得到恢复。  

```python
class Caretaker:
    
    def __init__(self):
        self.__mementolist = list()
    
    def getMemento(self, i):
        return self.__mementolist[i]
    
    def saveMemento(self, memento):
        self.__mementolist.append(memento)
```

### 优点
 - 提供了一种状态恢复的实现机制，使得用户可以方便地回到一个特定的历史步骤，当新的状态无效或者存在问题时，可以使用暂时存储起来的备忘录将状态复原。

### 缺点
 - 资源消耗过大，如果需要保存的原发器类的成员变量太多，就不可避免需要占用大量的存储空间，每保存一次对象的状态都需要消耗一定的系统资源。

### 适用场景
 - 保存一个对象在某一个时刻的全部状态或部分状态，这样以后需要时它能够恢复到先前的状态，实现撤销操作。
 
## 4.7 观察者模式
用于建立一种对象与对象之间的依赖关系，一个对象发生改变时将自动通知其他对象，其他对象将相应作出反应。  
在观察者模式中，发生改变的对象称为观察目标，而被通知的对象称为观察者，一个观察目标可以对应多个观察者，而且这些观察者之间可以没有任何相互联系，可以根据需要增加和删除观察者，使得系统更易于扩展。  

### 角色
 - 目标：又称为主题，它是指被观察的对象。在目标中定义了一个观察者集合，一个观察目标可以接受任意数量的观察者来观察，它提供一系列方法来增加和删除观察者对象，同时它定义了通知方法notify()。目标类可以是接口，也可以是抽象类或具体类。  
 - 具体目标：目标类的子类，通常它包含有经常发生改变的数据，当它的状态发生改变时，向它的各个观察者发出通知；同时它还实现了在目标类中定义的抽象业务逻辑方法（如果有的话）。
 - 观察者：观察者将对观察目标的改变做出反应，观察者一般定义为接口，该接口声明了更新数据的方法update()。  
 - 具体观察者：在具体观察者中维护一个指向具体目标对象的引用，它存储具体观察者的有关状态，这些状态需要和具体目标的状态保持一致；它实现了在抽象观察者Observer中定义的update()方法。
```python
from abc import ABC, abstractmethod
class Subject(ABC):
    
    observers = []

    def attach(self, observer):
        self.observers.append(observer)

    def detach(self, observer):
        self.observers.remove(observer)
    
    @abstractmethod
    def notify(self):
        pass

class ConcreteSubject(Subject):
    
    def notify(self):
        for ob in self.observers:
            ob.update()

class Observer(ABC):
    
    @abstractmethod
    def update(self):
        pass

class ConcreteObserver(Observer):

    def update(self):
        # 具体响应代码
        pass
```
在有些更加复杂的情况下，具体观察者类ConcreteObserver的update()方法在执行时需要使用到具体目标类ConcreteSubject中的状态（属性），因此在ConcreteObserver与ConcreteSubject之间有时候还存在关联或依赖关系，在ConcreteObserver中定义一个ConcreteSubject实例，通过该实例获取存储在ConcreteSubject中的状态。 
在当前流行的MVC(Model-View-Controller)架构中也应用了观察者模式，MVC是一种架构模式，它包含三个角色：模型(Model)，视图(View)和控制器(Controller)。其中模型可对应于观察者模式中的观察目标，而视图对应于观察者，控制器可充当两者之间的中介者。当模型层的数据发生改变时，视图层将自动改变其显示内容。  

### 优点
 - 实现表示层和数据逻辑层的分离，定义了稳定的消息更新传递机制，并抽象了更新接口，使得可以有各种各样不同的表示层充当具体观察者角色。
 - 观察目标只需要维持一个抽象观察者的集合，无须了解其具体观察者。
 - 观察目标会向所有已注册的观察者对象发送通知，简化了一对多系统设计的难度。
 - 满足“开闭原则”的要求，增加新的具体观察者无须修改原有系统代码。

### 缺点
 - 如果一个观察目标对象有很多直接和间接观察者，将所有的观察者都通知到会花费很多时间。
 - 观察者模式没有相应的机制让观察者知道所观察的目标对象是怎么发生变化的，而仅仅只是知道观察目标发生了变化。

### 适用场景
 - 一个对象的改变将导致一个或多个其他对象也发生改变，而并不知道具体有多少对象将发生改变，也不知道这些对象是谁。
 - 需要在系统中创建一个触发链，A对象的行为将影响B对象，B对象的行为将影响C对象……，可以使用观察者模式创建一种链式触发机制。
 
## 4.7 状态模式
状态模式用于解决系统中复杂对象的状态转换以及不同状态下行为的封装问题。当系统中某个对象存在多个状态，这些状态之间可以进行转换，而且对象在不同状态下行为不相同时可以使用状态模式。

### 角色
 - 环境类：又称为上下文类，它是拥有多种状态的对象。由于环境类的状态存在多样性且在不同状态下对象的行为有所不同，因此将状态独立出去形成单独的状态类。在环境类中维护一个抽象状态类State的实例，这个实例定义当前状态，在具体实现时，它是一个State子类的对象。
 - 抽象状态类：定义一个接口以封装与环境类的一个特定状态相关的行为，在抽象状态类中声明了各种不同状态对应的方法。
 - 具体状态类：抽象状态类的子类，每一个子类实现一个与环境类的一个状态相关的行为，每一个具体状态类对应环境的一个具体状态，不同的具体状态类其行为有所不同。

```python
from __future__ import annotations
from abc import ABC, abstractmethod


class Context:
    """
    The Context defines the interface of interest to clients. It also maintains
    a reference to an instance of a State subclass, which represents the current
    state of the Context.
    """

    _state = None
    """
    A reference to the current state of the Context.
    """

    def __init__(self, state: State) -> None:
        self.transition_to(state)

    def transition_to(self, state: State):
        """
        The Context allows changing the State object at runtime.
        """

        print(f"Context: Transition to {type(state).__name__}")
        self._state = state
        self._state.setContext(self)

    """
    The Context delegates part of its behavior to the current State object.
    """

    def request1(self):
        self._state.handle1()

    def request2(self):
        self._state.handle2()


class State(ABC):
    """
    The base State class declares methods that all Concrete State should
    implement and also provides a backreference to the Context object,
    associated with the State. This backreference can be used by States to
    transition the Context to another State.
    """
    
    _context = None

    @property
    def context(self) -> Context:
        return self._context

    def setContext(self, context: Context) -> None:
        self._context = context

    @abstractmethod
    def handle1(self) -> None:
        pass

    @abstractmethod
    def handle2(self) -> None:
        pass


"""
Concrete States implement various behaviors, associated with a state of the
Context.
"""


class ConcreteStateA(State):
    def handle1(self) -> None:
        print("ConcreteStateA handles request1.")
        print("ConcreteStateA wants to change the state of the context.")
        self.context.transition_to(ConcreteStateB())

    def handle2(self) -> None:
        print("ConcreteStateA handles request2.")


class ConcreteStateB(State):
    def handle1(self) -> None:
        print("ConcreteStateB handles request1.")

    def handle2(self) -> None:
        print("ConcreteStateB handles request2.")
        print("ConcreteStateB wants to change the state of the context.")
        self.context.transition_to(ConcreteStateA())


if __name__ == "__main__":
    # The client code.

    context = Context(ConcreteStateA())
    context.request1()
    context.request2()
```
环境类实际上是真正拥有状态的对象，我们只是将环境类中与状态有关的代码提取出来封装到专门的状态类中。  
在状态模式的使用过程中，一个对象的状态之间还可以进行相互转换，通常有两种实现状态转换的方式：
 - 统一由环境类来负责状态之间的转换，在环境类的业务方法中通过对某些属性值的判断实现状态转换
 - 由具体状态类来负责状态之间的转换，可以在具体状态类的业务方法中判断环境类的某些属性值再根据情况为环境类设置新的状态对象，实现状态转换

### 优点
 - 单一职责原则。将与特定状态相关的代码放在单独的类中。
 - 开闭原则。无需修改已有状态类和上下文就能引入新状态。

### 缺点
 - 增加系统中类和对象的个数。

### 适用场景
 - 如果对象需要根据自身当前状态进行不同行为， 同时状态的数量非常多且与状态相关的代码会频繁变更的话， 可使用状态模式。
 - 如果某个类需要根据成员变量的当前值改变自身行为， 从而需要使用大量的条件语句时， 可使用该模式。



