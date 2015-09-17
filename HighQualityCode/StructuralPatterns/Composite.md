#**Composite pattern**


----------
##**Същност**
Позволява да се обединяват различни типове обекти в дървовидни структури. Също така дава възможност да се третират еднакво отделни обекти или групи от обекти. Улеснява добавянето на нови видове компоненти. Използва се при работата с различни обекти, когато има нужда разликите между тях да бъдат игнорирани и да бъдат третирани еднакво.

##**Структура**

![enter image description here](https://github.com/tokera/TelerikAcademyHomeworks/blob/master/HighQualityCode/StructuralPatterns/images/Composite.jpg)

##**Демо**
```cs
static class Program
{
    static void Main()
    {
        var root = new Composite("root");
        root.AddChild(new Leaf("Leaf 1"));
        root.AddChild(new Leaf("Leaf 2"));

        var comp = new Composite("Composite C");
        comp.AddChild(new Leaf("Leaf C.1"));
        comp.AddChild(new Leaf("Leaf C.2"));

        root.AddChild(comp);
        root.AddChild(new Leaf("Leaf 3"));

        var leaf = new Leaf("Leaf 4");
        root.AddChild(leaf);
        root.RemoveChild(leaf);

        root.Display(1);
    }
}

public abstract class Component
{
    protected readonly string name;

    protected Component(string name)
    {
        this.name = name;
    }

    public abstract void Operation();
    public abstract void Display(int depth);
}

class Composite : Component
{
    private readonly List<Component> _children = new List<Component>();

    public Composite(string name)
        : base(name)
    {
    }

    public void AddChild(Component component)
    {
        _children.Add(component);
    }

    public void RemoveChild(Component component)
    {
        _children.Remove(component);
    }

    public override void Display(int depth)
    {
        Console.WriteLine(new String('-', depth) + name);

        foreach (Component component in _children)
        {
            component.Display(depth + 2);
        }
    }
    public override void Operation()
    {
        string message = string.Format("Composite with {0} child(ren).", _children.Count);
        Console.WriteLine(message);
    }
}

public class Leaf : Component
{
    public Leaf(string name)
        : base(name)
    {
    }

    public override void Operation()
    {
        Console.WriteLine("Leaf.");
    }

    public override void Display(int depth)
    {
        Console.WriteLine(new String('-', depth) + name);
    }
}
```