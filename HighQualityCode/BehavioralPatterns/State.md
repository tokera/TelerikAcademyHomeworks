#**State Pattern**


----------
##**Същност**
Изменя поведението на даден обект, когато неговото състояние се промени. Енкапсулира логиката за всяко състояние (чрез отделен клас). Улеснява добавянето на нови състояния. Позволява промяна на поведението на даден обект по време на изпълнение на програмата, чрез промяна на неговото състояние. 

##**Структура**

![enter image description here](https://github.com/tokera/TelerikAcademyHomeworks/blob/master/HighQualityCode/BehavioralPatterns\images\state.jpg)

##**Демо**
```cs
static class Program
{
    static void Main()
    {
        var context = new Context(new ConcreteStateA());
        context.Request();
        context.Request();
        context.Request();
        context.Request();
    }
}

public class Context
{
    private StateBase _state;

    public Context(StateBase state)
    {
        _state = state;
        State = _state;
    }

    public void Request()
    {
        _state.Handle(this);
    }

    public StateBase State
    {
        set
        {
            _state = value;
            Console.WriteLine("Current state: {0}",_state.GetType());
        }
    }
}

public abstract class StateBase
{
    public abstract void Handle(Context context);
}

class ConcreteStateA : StateBase
{
    public override void Handle(Context context)
    {
        context.State = new ConcreteStateB();
    }
}

class ConcreteStateB : StateBase
{
    public override void Handle(Context context)
    {
        context.State = new ConcreteStateA();
    }
}
```