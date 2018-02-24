**Pooling**

Kennen sie das? Sie brauchen unbedingt mehr als 10000 neue Objekte pro Frame, aber irgendwie mag das die Framerate nicht?

Das muss nicht sein! Probieren sie __Pooling.__

Pooling leitet sich sprachlich vom englischen _(to) pool_ (zusammenlegen, vereinigen) ab und bezeichnet das Sammeln von vielen Instanzen vor der Benutzung einzelner. 

Bahnhof? Sagen wir... wir bauen ein Shoot'em'up. __Mushihimesama__ in Unity (C#), weil wer will schon einfach anfangen und weniger als 8000 Bullets auf 480x640 wäre Screen estate-Verschwendung.

Wir sitzen am Boss, der alle 0.2 Sekunden 50 Kuegeln feuert. Das Ganze sieht also in etwa so aus:

```cs
// Ein Objekt das 1:1 aussieht und sich verhält wie alle Kugeln sollen
Transform bulletPrefab = Resources.Load("bullet.prefab") as Transform;

// Pause in Sekunden zwischen Schüssen
float bulletDelay = 0.2f;

// Sobald unser Objekt bereit ist und das Spiel los geht...
void Start()
{
    // ...schießen wir pro 0.2 Sekunde Kugeln.
    InvokeRepeating("Fire", bulletDelay, 0.0f);
}

void Fire()
{
    for (int i = 0; i < 500; i++;)
    ‎{
    ‎    // Wir instanzieren ein Objekt...
    ‎    Instantiate(
    ‎        bulletPrefab, // ...basierend auf unserer Vorlage...
    ‎        tranansform.position, // ...an der Position des Bosses...
            Quaternion.FromEuler(0, 0, π / 500 * i * Mathf.Rad2Deg) // ...im Uhrzeigersinn verteilt gedreht.
        );
    ‎}
}
```

Pro Sekunde erstellen wir jetzt also 2500 Objekte. Wenn wir 3 Frames haben, bin ich glücklich. Durch das konsequente Neu-Erstellen von GameObjekten, allokiert die Engine neuen Speicher, wenn wir eine gewisse Anzahl an Objekten ueberschreiten - und Speicher allkoieren ist teuer.

Stattdessen allokieren wir einen großen Block an GameObjekten direkt zu Begin und nehmen uns Objekte aus dieser Liste:
```cs
// Ein Objekt das 1:1 aussieht und sich verhält wie alle Kugeln sollen
Transform bulletPrefab = Resources.Load("bullet.prefab") as Transform;

// Pause in Sekunden zwischen Schüssen
float bulletDelay = 0.2f;

// Wieviele Objekte wir vorallokieren wollen
const int poolSize = 100000;

// Pool an Objekten
Transform[] gameObjectPool = new Transform[poolSize];

// Liste an Indeces von verfuegbaren Objekten
List<int> availableGameObjectMap = new List<int>(poolSize);

// Sobald unser Objekt bereit ist und das Spiel los geht...
void Start()
{
    // Erstellen wir 100.000 Objekte (~=c.a. 40 Sekunden)...
    for (int i = 0; i < poolSize; i++)
    {
    ‎    // Wir instanzieren ein Objekt...
    ‎    Instantiate(
    ‎        bulletPrefab, // ...basierend auf unserer Vorlage...
    ‎        new Vector2(-10000, -10000), // ...weit ausserhalb des Screens...
            Quternion.identity // ..."ohne" Rotation.
        );
        availableGameObjectMap.Add(i);
    }
}

    // ...und schießen pro 0.2 Sekunde unsere Kugeln
    InvokeRepeating("Fire", bulletDelay, 0.0f);
}

void Fire()
{
    for (int i = 0; i < 500; i++;)
    ‎{
        int gameObjectPoolIndex = vailableGameObjectMap.pop();
    ‎    // Wir nehmen ein bereits erstelltes Objekt...
    ‎    gameObjectPool[gameObjectPoolIndex].position = tranansform.position; // ...an die Position des Bosses verschieben...
        gameObjectPool[gameObjectPoolIndex].rotation = Quaternion.FromEuler(0, 0, Mathf.PI / 500 * i * Mathf.Rad2Deg) // ...im Uhrzeigersinn verteilt gedreht..
        );
    ‎}
}
```
Da die Objekte bereits existieren und lediglich modifiziert werden, verschieben wir die Zeit des Erstellens an den Anfang (Und unter anderem darum gibt es Ladezeiten...) und brauchen dies nicht während der Laufzeit des Spiels zu erledigen.
