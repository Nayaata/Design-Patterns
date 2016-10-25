#State

**State**  представлява **Behavioral Patterns**, един от трите типа **Design Pattern** (шаблони).

* __Дефиниция__:
    *	__State__ pattern е дизайн модел, който осигурява промени в поведението на даден обект в зависимост от текущото състояние. Заместването на класове в рамките на определен контекст динамично променя типа по време на изпълнение на програмата.
    *	__State Pattern__ при промяна на състоянието на даден обект, се изменя  и неговото поведение. 
    *	При ползване на шаблона се наблюдава промяна в състоянието на обекта от друга страна това осигурява  **separation of concerns**, което значително улеснява тестването на кода.
    *	 __State__  енкапсулира логиката за всяко състояние с помощта на отделени класове. Т.е. логиката на състоянието е енкапсулирана в самото състояние.
    *	При употреба на шаблона се наблюдава силен __coupling__.
    
* __Цел__:
  State Pattern се използва с цел промяна в поведението на даден обект според състоянието. Всяко едно състояние се имплементират като отделнен обект.
Можем да създаваме методи във всяко отделно състояние.

* __Приложение:__
  State Pattern се прилага в случаи, когато поведението на даден обект трябва да се промени динамично, в зависимост от неговото състояние.
  
* __Компоненти:__
    - __Context__: дефинира интерфейса и пази инстанция на подкласа на State, който имплементира състоянието.
    - __State__: дефинира интерфейс на поведението, в съответствие с определено състояние на Context.
    -	__ConcreteState__:имплементира се поведение на всеки клас, свързано с едно състояние на Context.

* __Диаграма__:

 ![BehavioralPatterns](images/state.png)
 
 * __Имплементация__:
 
~~~c#
using System;
 
namespace DoFactory.GangOfFour.State.Structural
{
  /// <summary>
  /// MainApp startup class for Structural
  /// State Design Pattern.
  /// </summary>
  class MainApp
  {
    /// <summary>
    /// Entry point into console application.
    /// </summary>
    static void Main()
    {
      // Setup context in a state
      Context c = new Context(new ConcreteStateA());
 
      // Issue requests, which toggles state
      c.Request();
      c.Request();
      c.Request();
      c.Request();
 
      // Wait for user
      Console.ReadKey();
    }
  }
 
  /// <summary>
  /// The 'State' abstract class
  /// </summary>
  abstract class State
  {
    public abstract void Handle(Context context);
  }
 
  /// <summary>
  /// A 'ConcreteState' class
  /// </summary>
  class ConcreteStateA : State
  {
    public override void Handle(Context context)
    {
      context.State = new ConcreteStateB();
    }
  }
 
  /// <summary>
  /// A 'ConcreteState' class
  /// </summary>
  class ConcreteStateB : State
  {
    public override void Handle(Context context)
    {
      context.State = new ConcreteStateA();
    }
  }
 
  /// <summary>
  /// The 'Context' class
  /// </summary>
  class Context
  {
    private State _state;
 
    // Constructor
    public Context(State state)
    {
      this.State = state;
    }
 
    // Gets or sets the state
    public State State
    {
      get { return _state; }
      set
      {
        _state = value;
        Console.WriteLine("State: " +
          _state.GetType().Name);
      }
    }
 
    public void Request()
    {
      _state.Handle(this);
    }
  }
}
~~~

Link [on WebSite](https://msdn.microsoft.com/en-us/library/orm-9780596527730-01-04.aspx).
