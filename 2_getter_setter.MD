**Getter und Setter**

Kennen sie das? Objekte und Scripte die ineinandergreifen und keine Ahnung wer welche Information woher bekommt? Das muss nicht sein! Probieren sie jetzt: Getter und Setter!

Beispiel: Eine Variable aus einem Script soll woanders benutzt werden. Nicht direkt darauf zugreifen, sondern stattdessen eine Methode aufrufen, die diesen Wert zurück gibt.

Gibt es lediglich diese __Getter__-Methode, ist garantiert, dass der Wert nur innerhalb des selben Scripts geändert werden kann. Lediglich das Auslesen ist nun möglich. Weniger Kopfschmerzen beim nachvollziehen von Änderungen:

```csharp
class GameObject
{
    private string Name;
    public GameObject(string name)
    {
        this.Name = name;
    }
    
    public string GetName()
    {
        return this.Name;
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        GameObject go = new GameObject("Player Object");
        Console.WriteLine(go.GetName());
    }
}
```

Schwarze Magie: C# unterstützt __Accessibility Levels__; Objekte können "unsichtbar" gemacht werden. So ist `GameObject.Name` nicht zulässig, da `Name` als `private` markiert ist. Lediglich Code in der Klasse selbst (wie `GetName()`) kann darauf zugreifen.  
Modifizierungen hinter einem `Setter` verstecken macht ebenfalls Sinn: Möchte man bspw. eine Überprüfung einbauen, dass der Name keine Zahl enthält, gibt es garantiert lediglich eine Stelle im Code, die ausgeführt wird; `SetName()`. Nun einfach in `SetName()` einen `if`-case einbauen und jede Umbenennung wird valide oder schlicht nicht ausgeführt, da sie durch `SetName()` laufen muss.
