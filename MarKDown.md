[markdown] (http://texwelt.de/wissen/markdown_help/)


Markdown-Syntax

Dieses Dokument beschreibt einige der wichtigsten Teile der Markdown für Autoren. Es gibt viel mehr Syntax, als hier erwähnt wird. Die vollständige Syntax-Dokumentation erhalten Sie unter Dokumentationsübersicht zu John Grubers Markdown SyntaxSeite
Kopfzeile
Unterstreichen von Text mit Gleichheitszeichen für Top-Level-Kopfzeilen. Zweiten Ebene Kopfzeilen verwende Bindestriche, um zu unterstreichen.
Dies ist ein H1
============= 	
Dies ist ein H1
Dies ist ein H2
------------- 	
Dies ist ein H2
Eine Empfehlung wäre, Du könntest der Kopfzeile stattdessen ein Hash-Symbol (#) voranstellen. Die Zahl der Hash Symbole zeigt die Reihenfolge der Kopfzeile an. Beispielsweise gibt ein einzelner Hash einer Kopfzeile als erstes an, während zwei die zweite Kopfzeile angibt:
# Dies ist ein H1 	
Dies ist ein H1
## Dies ist ein H2 	
Dies ist ein H2
### Dies ist eine H3 	
Dies ist eine H3
Was Du auswählst, ist eine Frage des Stils. Je nachdem, was Du denkst, was im Textdokument besser aussieht. In beiden Fällen sieht das endgültige, vollständig formatierte, Dokument gleich aus.
Absätze
Absätze werden durch Leerzeilen umgeben.
Dies ist der erste Absatz.

Dies ist der zweite Absatz.
Links
Es sind zwei Teile an jeder Link Verbindung. der erste ist der eigentliche Text, der dem Benutzer angezeigt wird und er muss in eckigen Klammern stehen. die zweite ist die Adresse der Seite, die Du verknüpfen möchtest und auch in Klammern stehen muss.
[Link-text](http://beispiel.com/) 	Link-text
Formatierung
Zum indizieren, von Fett formatiertem Text setze den Text in zwei Sterne (*)oder zwei Unterstrich (_) Symbole:
**Das ist Fett** 	Das ist Fett
__Das ist auch Fett__ 	Das ist auch Fett
Zum Festlegen von kursiven Text setze den Text in einem einzelnen Stern (*) oder Unterstrich (_):
*Dies ist kursiv* 	Dies ist kursiv
_Dies ist auch kursiv_ 	Dies ist auch kursiv
Zum Festlegen von kursivem und fettem Text setze den Text in drei Sterne (*) oder ein Unterstrich (_) Symbole:
***Das ist Fett und kursiv*** 	Das ist Fett und kursiv
___Das ist auch Fett und kursiv___ 	Das ist auch Fett und kursiv
Blockquoten
Um einen eingerückten Bereich zu erstellen verwenden die rechtwinklige Klammer (>) Zeichen vor jede Zeile die in der Blockquote aufgenommen werden soll.
> Dies ist Teil einer Blockquote.
> Dies ist in der gleichen Blockquote. 	

Dies ist Teil einer Blockquote.
Dies ist in der gleichen Blockquote.
Anstatt es vor jeder Zeile zu setzen damit es in das Block-Angebot aufgenommen wird kannst Du es am Anfang und am Ende des Zitats mit einem Zeilenumbruch setzen.
> Dies ist Teil einer Blockquote.
Die Blockquote wird fortgesetzt, auch wenn es nicht in eckigen Klammern steht.

Die Leerzeile beendet das Blockzitat. 	

Dies ist Teil einer Blockquote.
Die Blockquote wird fortgesetzt, auch wenn es nicht in eckigen Klammern steht.

Die Leerzeile beendet das Blockzitat.
Lists
Wenn Du eine nummerierte Markdown Liste erstellen möchtest, setze eine Zahl vor jedes Element in der Liste, gefolgt von einem Zeit und Ort. Die Nummer, die Du verwendest, spielt tatsächlich keine Rolle.
1. Element 1
2. Element 2
3. Element 3 	

    Element 1
    Element 2
    Element 3

Um eine Liste mit Aufzählungszeichen zu erstellen, versetze jedes Element in der Liste mit einem Stern (*) Symbole.
* Ein Listenelement
* Ein weiterer Punkt der Liste
* Ein dritter Listenpunkt 	

    Ein Listenelement
    Ein weiterer Punkt der Liste
    Ein dritter Listenpunkt

Viel mehr
Es gibt viel mehr in der Markdown-Syntax als hier erwähnt wird. Aber für kreative Schreiber, Dies deckt viele Möglichkeiten auf. Viel mehr über Markdown als Du jemals wirklich wissen möchtest, rufen die Markdown-Seite auf, wo alles begann.
