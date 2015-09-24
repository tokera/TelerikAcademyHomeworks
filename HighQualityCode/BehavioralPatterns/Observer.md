#**Observer Pattern**


----------
##**Същност**
Представя функционалност за информиране на дадени обекти, че в друг обект е настъпила определена промяна. Обектите, които се интересуват от конкретната промяна в друг обект го заявяват и от там нататък се създава връзка между обекта и всички обекти, които се интересуват от него, така че когато въпросният обект промени състоянието си, всички да бъдат информирани.
##**Структура**

![enter image description here](https://github.com/tokera/TelerikAcademyHomeworks/blob/master/HighQualityCode/BehavioralPatterns/images/observer.jpg)

##**Демо**
```cs
static class Program
{
    static void Main()
    {
        var subject = new ConcreteSubject();
        subject.Attach(new ConcreteObserver(subject,"Observer 1"));
        subject.Attach(new ConcreteObserver(subject,"Observer 2"));
        subject.Attach(new ConcreteObserver(subject,"Observer 3"));
        subject.SetState("STATE");
    }
}

public abstract class SubjectBase
{
    private ArrayList _observers = new ArrayList();

    public void Attach(ObserverBase o)
    {
        _observers.Add(o);
    }

    public void Detach(ObserverBase o)
    {
        _observers.Remove(o);
    }

    public void Notify()
    {
        foreach (ObserverBase o in _observers)
        {
            o.Update();
        }
    }
}

public class ConcreteSubject : SubjectBase
{
    private string _state;

    public string GetState()
    {
        return _state;
    }
 
    public void SetState(string newState)
    {
        _state = newState;
        Notify();
    }
}

public abstract class ObserverBase
{
    public abstract void Update();
}


public class ConcreteObserver : ObserverBase
{
    private ConcreteSubject _subject;
    private string _name;

    public ConcreteObserver(ConcreteSubject subject, string name)
    {
        _subject = subject;
        _name = name;
    }

    public override void Update()
    {
        string subjectState = _subject.GetState();
        Console.WriteLine(_name + ": " +subjectState);
    }
}
```