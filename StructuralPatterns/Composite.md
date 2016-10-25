# Composite

**Composite** представлява **Structural Patterns**, един от трите типа **Design Pattern** (шаблон).

*  __Дефиниция:__
    * __Composite Pattern__ представлява шаблон, който се използва в обектно-ориентираното програмиране.
    * __Шаблонът__ ни позволява да създаваме йерархия от класове. Възможно е да комбинираме различни обекти в една дървовидна структура. Осигурява се възможност да третираме обектите по един и същ начин независимо от вида им - прости или композитни. Композитните обекти представляват сложно-съставни обекти, които имат възможност да съдържат други композитни или прости обекти.
    * __Composite__ design pattern се използва за създаване на йерархични модели на обекта. 
Посредством дървовидната стуктура от обекти, всеки един от индивидуалните обекти и групи могат да се достъпват свободно.
	
* __Цел__
    * __Composite Pattern__ се използва с цел да композира обектите, да създава йерархия от класове и да ги обединява в дървовидна структура. Позволява да третираме простите обкети (листата) и композитните обекти по един и същи начин.

* __Компоненти:__
    * __Component__: представлява абстракцията на всички компоненти и различните видове обекти. __IComponent__ е интерфейс или абстрактен клас, който дефинира методите изпълняващи се както Leaf и Composite класовете.
    * __Leaf__: представлява т.н прости обекти в йерархията и тяхната имплементация в Component интерфейса. 
    * __Composite__: представлява композитната имплементация на Component-a т.е. композитните обекти, който могат да имат наследници. Композитните обекти представляват сложно-съставни обекти, които имат възможност да съдържат други композитни или прости обекти. Методите, които поддържа са следните:
        * __AddComponent__: добавя нов елемент
        * __Operation__: е общ метод, който може да бъде имплементиран от всички елементи в дървото
        * __GetChild__: връща всички наследници
        * __RemoveComponent__: премахва елемент
        
* __Употреба__:
    * Windows.Forms.Control
    * System.Web.UI.Control
    * System.Xml.XmlNode
    
* __Диаграма__:

 ![StructuralPatterns](images/Composite.jpg) 
 
* __Имплементация__:
 
~~~c#
namespace CompositePattern
{
    using System;
    using System.Collections.Generic;
    using System.Linq;
    //Client
    class Program
    {
        static void Main(string[] args)
        {
            // initialize variables
            var compositeGraphic = new CompositeGraphic();
            var compositeGraphic1 = new CompositeGraphic();
            var compositeGraphic2 = new CompositeGraphic();

            //Add 1 Graphic to compositeGraphic1
            compositeGraphic1.Add(new Ellipse());

            //Add 2 Graphic to compositeGraphic2
            compositeGraphic2.AddRange(new Ellipse(), 
                new Ellipse());

            /*Add 1 Graphic, compositeGraphic1, and 
              compositeGraphic2 to compositeGraphic */
            compositeGraphic.AddRange(new Ellipse(), 
                compositeGraphic1, 
                compositeGraphic2);

            /*Prints the complete graphic 
            (four times the string "Ellipse").*/
            compositeGraphic.Print();
            Console.ReadLine();
        }
    }
    //Component
    public interface IGraphic
    {
        void Print();
    }
    //Leaf
    public class Ellipse : IGraphic
    {
        //Prints the graphic
    	public void Print()
        {
            Console.WriteLine("Ellipse");
        }
    }
    //Composite
    public class CompositeGraphic : IGraphic
    {
        //Collection of Graphics.
        private readonly List<IGraphic> graphics;

        //Constructor 
        public CompositeGraphic()
        {
            //initialize generic Collection(Composition)
            graphics = new List<IGraphic>();
        }
        //Adds the graphic to the composition
        public void Add(IGraphic graphic)
        {
            graphics.Add(graphic);
        }
        //Adds multiple graphics to the composition
        public void AddRange(params IGraphic[] graphic)
        {
            graphics.AddRange(graphic);
        }
        //Removes the graphic from the composition
        public void Delete(IGraphic graphic)
        {
            graphics.Remove(graphic);
        }
        //Prints the graphic.
        public void Print()
        {
            foreach (var childGraphic in graphics)
            {
                childGraphic.Print();
            }
        }
    }
}

~~~

######Пример:

~~~c#
public interface IComposite
    {
        void CompositeMethod();
    }

    public class LeafComposite :IComposite 
    {

        #region IComposite Members

        public void CompositeMethod()
        {
            //To Do something
        }

        #endregion
    }

    /// Elements from IComposite can be separated from others 
    public class NormalComposite : IComposite
    {

        #region IComposite Members

        public void CompositeMethod()
        {
            //To Do Something
        }

        #endregion

        public void DoSomethingMore()
        {
            //Do Something more .
        }
    }
~~~

Link [on WebSite](http://www.dofactory.com/net/design-patterns).
