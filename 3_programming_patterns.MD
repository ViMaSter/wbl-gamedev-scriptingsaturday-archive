**Programming patterns**

Kennen sie das? Sie müssen den Scripting Saturday füllen, wissen aber nicht wie?

Das muss nicht sein! Probieren sie: __Programming patterns__. (Ich bin heute mal Meta. So ohne Code. Boo-hoo, I know.)

Eine der - meiner Meinung nach - coolsten Eigenschaften am Programmieren ist, dass sich Software schneller ändert, als man lernt. Die Eigenheiten einer Sprache zu kennen, wirkt am Anfang wie das Ziel. Wer das Featureset einer Sprache kennt, kann in dieser alles bauen. Und das ist bedingt richtig: Es ist unwahrscheinlich, dass man an ein unlösbares Problem stößt, wenn einem alle Features einer Sprache bekannt ist. Viel interessanter ist jedoch, dass man Lösungsmuster beibehält und verfeinert - und das über Sprachen hinweg. Muster; Programming patterns.

In bspw. C++, C#, PHP oder JS, lösen sich die meisten Probleme ähnlich. Sie gehören zur Gruppe der __General propose languages__ - "Allzweck-Sprachen" - und haben damit ein gleich- oder sehr ähnlich-großes Einsatzfeld. Dabei beziehe ich mich nicht darauf, dass beispielsweise die Twitch __API__ immer über __HTTP-Requests__ angesprochen wird, sondern darum, dass der Ablauf "HTTP-Request beschreiben, ausführen, abwarten, auswerten" in jeder dieser Sprachen ähnlich aufbaubar ist.

Es geht darum Code zu strukturieren, nicht um die Sprachen-spezifische Implementation; ein Muster zu erkennen und den Lösungsansatz abstrakt genug zu halten, dass er in vielen Sprachen und Probleme anwendbar ist. Die Implementation ist dann das Kleinste der Probleme.

Selbstverständlich trifft das nicht auf alle Sprachen zu - __Haskell__ oder frühere Versionen von PHP werden bspw. als "__Funktionale Sprachen__" bezeichnet - und einige Patterns lassen sich dann nicht mehr ganz so einfach übertragen.

In den kommenden Wochen gibt's das ganze dann mit Praxisbeispielen; in der Zwischenzeit:
http://gameprogrammingpatterns.com [free!] (en)  
Elements of Reusable Object-Oriented Software: 0-321-33487-6 [nicht free. : ( ] (en)
