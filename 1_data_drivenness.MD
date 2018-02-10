**if-case hell? Make it data-driven!**

Kennen sie das? Sie möchten __Input mappen__ aber enden mit 8000-`if`-cases?

```js
if(Input.GetKeyDown(KeyCode.Space))
    jump();
if(Input.GetKey(KeyCode.W))
    move(0.0, 1.0);
if(Input.GetKey(KeyCode.S))
    move(0.0, -1.0);
if(Input.GetKey(KeyCode.A))
    move(-1.0, 0.0);
if(Input.GetKey(KeyCode.D))
    move(1.0, 0.0);
if(Input.GetKeyDown(KeyCode.E))
    use();
if(Input.GetKeyDown(KeyCode.I))
    openUI(UI.Inventory);
```
Das muss nicht sein! Probieren sie jetzt: __Data-Driven__-ness!
```js
var KeyState =
    {
        "Down": Input.GetKeyDown,
        "Hold": Input.GetKey
    };
var mappings = [
    ["Down", KeyCode.Space, function(){ jump();               }],
    ["Hold", KeyCode.W,     function(){ move(1.0, 0.0);       }],
    ["Hold", KeyCode.S,     function(){ move(-1.0, 0.0);      }],
    ["Hold", KeyCode.A,     function(){ move(0.0, -1.0);      }],
    ["Hold", KeyCode.D,     function(){ move(0.0, 1.0);       }],
    ["Down", KeyCode.E,     function(){ use();                }],
    ["Down", KeyCode.I,     function(){ openUI(UI.Inventory); }],
];

for (mappingIndex in mappings)
{
    mapping = mappings[mappingIndex];
    if (KeyState[mapping[0]](mapping[1]))
        mapping[2]();
}
```

Schwarze Magie: Nahezu jede Sprache unterstützt __Lambda__ und die Möglichkeit __Funktionen als Parameter__ zu übergeben. Dadurch können wir eine Variable erstellen, die eine Funktion enthält und "die Variable aufrufen", anstatt einem direkten Funktionsaufruf.
