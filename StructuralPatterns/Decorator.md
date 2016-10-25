# Decorator

**Decorator** представлява **Structural Patterns**, един от трите типа **Design Pattern** (шаблон).

*  __Дефиниция:__
    * __Decorator Pattern__ представлява шаблон, който се използва в обектно-ориентираното програмиране.
    * __Шаблонът__ ни позволява динамично да разширяваме функционалността на опеределен клас или група класове 
    по времето на изпълнение на програмата (Runtime) без да променя интерфейса.
    * __Decorator__ осигурява възможност да добавяме нова функционалност или да променим съществуваща такава.
    * Всички компоненти и класове наследяват един общ интерфейс.
    * __Decorator Pattern__ е подходящ, когато се следва **Single responsibility principle**.
    
* __Цел__:
    * __Шаблонът__ се ползва с цел динамичното разширяване на функционалността на опеределен клас или група класове 
    по времето на изпълнение на програмата (Runtime) без да променя интерфейса.
    * __Decorator Pattern__ улеснява модификацията и нанасянето на глобални промени в съществуващата йерархия от класове.
    
* __Компоненти:__
    * __Component__ (IComponent): представлява общия интерфейс на обектите, към които може динамично да се добавят допълнителни функционалности.
    * __ConcreteComponent__: представлява конкретния обект към който ще се добавя нова функционалност или се модифицира налична такава.
    * __Decorator__: пази референция към компонент обекта. Декоратор класа пази в себе си инстанция на оригиналния обект,
    като по този начин вместо с наследяване имаме достъп чрез инстанцията до функционалноста на обекта.
    * __ConcreteDecorator__: добавя функционалност към обекта.
    
* __Употреба__:
    * __Decorator Pattern__ се използва за разширяване на функционалноста на потребителския интерфейс и базовия клас.
    
* __Диаграма__:

 ![StructuralPatterns](images/decorator.jpg) 
 
* __Имплементация__:
 
~~~c#
using System;

  class MainApp
  {
    static void Main()
    {
      // Create ConcreteComponent and two Decorators 
      ConcreteComponent c = new ConcreteComponent();
      ConcreteDecoratorA d1 = new ConcreteDecoratorA();
      ConcreteDecoratorB d2 = new ConcreteDecoratorB();

      // Link decorators 
      d1.SetComponent(c);
      d2.SetComponent(d1);

      d2.Operation();

      // Wait for user 
      Console.Read();
    }
  }

  // "Component" 
  abstract class Component
  {
    public abstract void Operation();
  }

  // "ConcreteComponent" 
  class ConcreteComponent : Component
  {
    public override void Operation()
    {
      Console.WriteLine("ConcreteComponent.Operation()");
    }
  }

  // "Decorator" 
  abstract class Decorator : Component
  {
    protected Component component;

    public void SetComponent(Component component)
    {
      this.component = component;
    }

    public override void Operation()
    {
      if (component != null)
      {
        component.Operation();
      }
    }
  }

  // "ConcreteDecoratorA" 
  class ConcreteDecoratorA : Decorator
  {
    private string addedState;

    public override void Operation()
    {
      base.Operation();
      addedState = "New State";
      Console.WriteLine("ConcreteDecoratorA.Operation()");
    }
  }

  // "ConcreteDecoratorB" 
  class ConcreteDecoratorB : Decorator
  {
    public override void Operation()
    {
      base.Operation();
      AddedBehavior();
      Console.WriteLine("ConcreteDecoratorB.Operation()");
    }

    void AddedBehavior()
    {
    }
  }
  ~~~

 Link [on WebSite](http://www.dofactory.com/net/design-patterns).
 
