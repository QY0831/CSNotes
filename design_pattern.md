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


