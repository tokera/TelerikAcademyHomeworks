#**Chain of Responsibility pattern**


----------
##**Същност**
Дефинира верига от класове, всеки от които, има възможост да обработва определени заявки. Заявката се подава по веригата и първия, който има възможност я обработва и прекъсва веригата. 
Опростява взаимовръзката на обектите - всеки обект пази референция към следващия. 

##**Структура**

![enter image description here](https://github.com/tokera/TelerikAcademyHomeworks/blob/master/HighQualityCode/BehavioralPatterns/images/chain_of_responsibility.jpg)

##**Демо**
```cs
static class Program
{
    static void Main()
    {
        HandlerBase handlerA = new ConcreteHandlerA();
        HandlerBase handlerB = new ConcreteHandlerB();
        handlerA.SetSuccessor(handlerB);
        handlerA.HandleRequest(1);
        handlerB.HandleRequest(11);
    }
}
 
public abstract class HandlerBase
{
    protected HandlerBase _successor;

    public abstract void HandleRequest(int request);

    public void SetSuccessor(HandlerBase successor)
    {
        _successor = successor;
    }
}

public class ConcreteHandlerA : HandlerBase
{
    public override void HandleRequest(int request)
    {
        if (request == 1)
            Console.WriteLine("Handled by ConcreteHandlerA");
        else if (_successor != null)
            _successor.HandleRequest(request);
    }
}


public class ConcreteHandlerB : HandlerBase
{
    public override void HandleRequest(int request)
    {
        if (request > 10)
            Console.WriteLine("Handled by ConcreteHandlerB");
        else if (_successor != null)
            _successor.HandleRequest(request);
    }
}
```