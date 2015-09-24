#**Mediator Pattern**


----------
##**Същност**
Опростява комуникацията между класовете. Създава се обект, посредник за обмен на информация между множество обекти. Вместо всеки един от тях да се грижи да предава информацията, един посредник го прави. Резултатът е, че обектите знаят само за посредника, а не за всички останали обекти.

##**Структура**

![enter image description here](https://github.com/tokera/TelerikAcademyHomeworks/blob/master/HighQualityCode/BehavioralPatterns\images\mediator.jpg)

##**Демо**
```cs
static class Program
{
    static void Main()
    {
        var m = new ConcreteMediator();

        var c1 = new ConcreteColleague1(m);
        var c2 = new ConcreteColleague2(m);

        m.Colleague1 = c1;
        m.Colleague2 = c2;

        c1.Send("How are you?");
        c2.Send("Fine, thanks");
    }
}
public abstract class ColleagueBase
{
    protected MediatorBase _mediator;

    public ColleagueBase(MediatorBase mediator)
    {
        _mediator = mediator;
    }
}

public abstract class MediatorBase
{
    public abstract void SendMessage(ColleagueBase caller, string message);
}

class ConcreteMediator : MediatorBase
{
    private ConcreteColleague1 _colleague1;
    private ConcreteColleague2 _colleague2;

    public ConcreteColleague1 Colleague1
    {
        set { _colleague1 = value; }
    }

    public ConcreteColleague2 Colleague2
    {
        set { _colleague2 = value; }
    }

   
    public override void SendMessage(ColleagueBase caller, string message)
    {
        if (caller == _colleague1)
        {
            _colleague2.Notify(message);
        }
        else
        {
            _colleague1.Notify(message);
        }
    }
}
 
class ConcreteColleague1 : ColleagueBase
{
    public ConcreteColleague1(MediatorBase mediator)
        : base(mediator)
    {
    }

    public void Send(string message)
    {
        _mediator.SendMessage(this,message);
    }

    public void Notify(string message)
    {
        Console.WriteLine("Colleague1 gets message: " + message);
    }
}

class ConcreteColleague2 : ColleagueBase
{
    public ConcreteColleague2(MediatorBase mediator)
        : base(mediator)
    {
    }

    public void Send(string message)
    {
        _mediator.SendMessage(this, message);
    }

    public void Notify(string message)
    {
        Console.WriteLine("Colleague2 gets message: "+ message);
    }
}
```