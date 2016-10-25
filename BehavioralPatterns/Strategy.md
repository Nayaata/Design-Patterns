#Strategy

**Strategy** представлява **Behavioral Patterns**, един от трите типа **Design Pattern** (шаблони).

* __Дефиниция__:
    * __Strategy__ енкапсулира група свързани алгоритми и ги прави лесно заменяеми.
    *	__Шаблонът__ позволява на всеки един  алгоритъм да варира, независимо от класа,  който го използва.
    *	__Strategy Pattern__  се прилага в случаи, че са използвани switch или if-else конструкции.
    *	__Шаблонът__ осигурява лесната замяна на даден алгоритъм с друг, когато алгоритмите работят с еднакви данни, следователно клиента има опция да избира с кой точно да работи.
    *	__Strategy__ е средство за постигане на дадена цел по различни начини. Входните и изходните данни са еднакви. С избора си на стратегия решаваме по какъв начин ще се достигне дадения резултат.
    *	__Шаблонът__ спомага за добре конструиране на логика за извършване на определено действие, подобряване на абстракцията, снткапсулация и по-лесна заменяемост при необходимост.
    *	Преимуществото на __Strategy__ - по време на изпълнение на кода има опция да избираме, кой алгоритъм искаме да приложим. Възможно е динамично заменяне.
    *	Енкапсулиране на логиката - дефинираме всяка една различна логика в отделен клас, като в последствие избираме кой от тях да ползваме.

* __Цел__:
    Шаблонът се ползва с цел да се дефинират различни алгоритми, решаващи еднакъв проблем,  по различни начини. Тези алгоритми са взаимно заменяеми, 
  с цел динамично да се променя поведението на класа по време на изпълнение на програмата.
  
  * __Употреби:__
    Strategy Pattern се прилага кс цел създаване абстракция на алгоритъм. Имплементиаме интерфейс, в който входните и изходните данни на всеки един метод се описват подробно.
    В класа, в който прилагаме шаблона следваме принципите на абстракция и спазваме DIP - SOLID принципите. Strategy прилагаме в случаи на използвани switch или if-else конструкции в дадена логика.

* __Компоненти:__
    - __Strategy__: дефинира един общ за групата алгоритми интерфейс. 
    - __ConcreteStrategy__: имплементира алгоритъма, като използва интерфейса
    - __Context__: е в съответствие с ConcreteStrategy обект. Контекст пази референция към Strategy обекта.
    Съществува опция за дефиниране на интерфейс, който осигурява достъпа до данните.
    
* __Диаграма__:

  ![BehavioralPatterns](images/strategy.png)
  
* __Имплементация__:
 
~~~c#
using System;
 
namespace DoFactory.GangOfFour.Strategy.Structural
{
  /// <summary>
  /// MainApp startup class for Structural
  /// Strategy Design Pattern.
  /// </summary>
  class MainApp
  {
    /// <summary>
    /// Entry point into console application.
    /// </summary>
    static void Main()
    {
      Context context;
 
      // Three contexts following different strategies
      context = new Context(new ConcreteStrategyA());
      context.ContextInterface();
 
      context = new Context(new ConcreteStrategyB());
      context.ContextInterface();
 
      context = new Context(new ConcreteStrategyC());
      context.ContextInterface();
 
      // Wait for user
      Console.ReadKey();
    }
  }
 
  /// <summary>
  /// The 'Strategy' abstract class
  /// </summary>
  abstract class Strategy
  {
    public abstract void AlgorithmInterface();
  }
 
  /// <summary>
  /// A 'ConcreteStrategy' class
  /// </summary>
  class ConcreteStrategyA : Strategy
  {
    public override void AlgorithmInterface()
    {
      Console.WriteLine(
        "Called ConcreteStrategyA.AlgorithmInterface()");
    }
  }
 
  /// <summary>
  /// A 'ConcreteStrategy' class
  /// </summary>
  class ConcreteStrategyB : Strategy
  {
    public override void AlgorithmInterface()
    {
      Console.WriteLine(
        "Called ConcreteStrategyB.AlgorithmInterface()");
    }
  }
 
  /// <summary>
  /// A 'ConcreteStrategy' class
  /// </summary>
  class ConcreteStrategyC : Strategy
  {
    public override void AlgorithmInterface()
    {
      Console.WriteLine(
        "Called ConcreteStrategyC.AlgorithmInterface()");
    }
  }
 
  /// <summary>
  /// The 'Context' class
  /// </summary>
  class Context
  {
    private Strategy _strategy;
 
    // Constructor
    public Context(Strategy strategy)
    {
      this._strategy = strategy;
    }
 
    public void ContextInterface()
    {
      _strategy.AlgorithmInterface();
    }
  }
}

~~~

Link [on WebSite](https://msdn.microsoft.com/en-us/library/orm-9780596527730-01-04.aspx).
