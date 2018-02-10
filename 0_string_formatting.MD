**String formatting**

Kennen sie das? Sie möchten Text ausgeben, aber enden damit:
```js
console.log("Player ID: " + playerID + "Name: " + name + "X,Y: " + position.x + "," + position.y);
```
Das muss nicht sein! Probieren sie jetzt:
```csharp
String.Format("PlayerID: {0} Name: {1} X,Y: {2}", playerID, name, position);
```
__`String.Format()`__, __`printf()`__ und ähnliche Methoden einer Sprache erlaubt Platzhalter in einem String; je nach Sprache werden Typen wie `Vector2` oder `Transform` sogar automatisch zu Strings umgewandelt oder die Platzhalter können sogar benannt werden!

Schwarze Magie: Objekte vom Typen __`varargs`__ erlauben "unendlich" Argumente zu einer Funktion.  
Anstatt `console.log(string format, string arg1, string arg2, string arg3, string arg4, [...]);`
sieht die __Funktionssignatur__ so aus:
`console.log(string format, string... arguments);`  
`arguments` kann in der Funktion dann wie ein Array behandelt werden, da `string...` ein __varargs__-Typ von Strings ist; es hat eine Länge und kann mit __Index-Operatoren__ ausgelesen/überschrieben werden.
