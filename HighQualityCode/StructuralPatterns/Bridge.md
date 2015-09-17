#**Bridge pattern**


----------
##**Същност**
Bridge pattern-ът е много ценен, понеже позволява отделянето на абстракцията от нейната имплементация. Използва се, когато даден клас и дейностите, които той извършва се променят често.

##**Структура**

 - **Abstraction:** интерфейс на абстракцията.
 - **RefinedAbstraction:** добавя функционалност върху абстракцията, но не съдържа имплементационни детайли. 
 - **Implementor:** интерфейс, който предоставя предварителни операции, които всички плъгини трябва да имплементират.
 - **ConcreteImplementor:** класовете, които ще бъдат използвани избирателно като плъгини.

![enter image description here](https://github.com/tokera/TelerikAcademyHomeworks/blob/master/HighQualityCode/StructuralPatterns/images/Bridge.jpg)

##**Демо**
```cs
static class Program
{
    static void Main()
    {
        Abstraction abstraction = new RefinedAbstraction
	        {
	             Implementor = new ConcreteImplementorA();
	        }

        abstraction.Operation();
    }
}

abstract class Implementor
{
    public abstract void Operation();
}

class Abstraction
{
    protected Implementor implementor;

    public Implementor Implementor
    {
        set { implementor = value; }
    }

    public virtual void Operation()
    {
        implementor.Operation();
    }
}

class RefinedAbstraction : Abstraction
{
    public override void Operation()
    {
        implementor.Operation();
    }
}

class ConcreteImplementorA : Implementor
{
    public override void Operation()
    {
        Console.WriteLine("ConcreteImplementor's Operation");
    }
}
```