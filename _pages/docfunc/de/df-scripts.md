---
layout: page
title: Skripte
permalink: "docfunc/de/df/scripts"
language: de
---

Die Skripte dienen vor Allem der Vereinfachung der Dokumente. Über sie können viele Informationen z.B. von den Empfängern oder Profildaten in ein Content-Control hineingepackt werden, anstatt die Felder einzeln ins Dokument einzufügen. Es besteht auch die Möglichkeit viel verwendete Skripte global abzulegen. In die Skripte können auch verschiedene Logiken eingebaut werden.

Jedes Skript wird vom Tag 'CustomDataNode' umarmt. Für alle Skripte muss eine Id angegeben werden. Diese ist frei wählbar, muss aber eindeutig sein. Um ein Skript über mehrere Zeilen zu machen muss mit den 'Line' Tags gearbeitet werden. Mit den 'Text' Tags kann ein fixer Text ausgegeben werden.


```xml 
<CustomDataNode id="Beispiel">
    <Line>
        <Text>Erste Zeile</Text>
    </Line>
    <Line>
        <Text>Zweite Zeile</Text>
    </Line>
</CustomDataNode>
```

Über die 'Element' Tags können Daten aus dem Profil oder externen Quellen angezogen werden. Damit die Daten aus dem Profil angezogen werden können wird die Feld-Id benötigt. Diese kann unter den Benutzereinstellungen gefunden werden.

![x]({{ site.baseurl }}/assets/content-images/docfunc/de/fieldid.png)

Damit ein Skript die Daten aus dem Profil anziehen kann muss vor die Feld-Id 'Profile.' geschrieben werden. Mit den Skripten es gibt die Möglichkeit die angezogenen Daten weiter zu verarbeiten oder zu ergänzen. Ein häufig verwendetes Attribut ist der 'separator'. Damit kann definiert werden, was die Trennung zum allfällig nachfolgenden Text sein soll. Folgt kein Text, so wird der definierte Separator nicht ausgegeben.


```xml
<CustomDataNode id="Beispiel">
    <Line>
        <Element id="Profile.User.Salutation" separator=" " />
        <Element id="Profile.User.FirstName" />
    </Line>
    <Line>
        <Element id="Profile.Org.Title" />
    </Line>
</CustomDataNode>
```

Mit 'Condition' Tags können Bedingungen in die Skripte eingebaut werden. Es gibt 'when' und 'notwhen' Bedingungen. Für 'oder'- Verknüpfungen kann das '|'- Zeichen verwendet werden. Für 'und'- Verknüpfungen ist es das '+'- Zeichen.


```xml
<CustomDataNode id="Beispiel">
    <Line>
        <Element id="Profile.User.Salutation" separator=" " />
        <Condition when="ShowFirstName = 'true' + DontShowFirstName = 'false'">
            <Element id="Profile.User.FirstName" />
        </Condition>
    </Line>
    <Condition notwhen="ShowTitle = 'false'">
        <Line>
            <Element id="Profile.Org.Title" />
        </Line>
    </Condition>
</CustomDataNode>
```

Via dem 'Snippet' Tag können OneOffixx Textbausteine angezogen werden. Dabei gilt es zu beachten, dass keine anderen daten-anziehenden Tags wie z.B. 'Element' im selben Skript verwendet werden dürfen. Dem 'CustomDataNode' Tag um das Snippet-Skript kann das Attribut 'update' gegeben werden. Es kann mit 'true oder 'false' angegeben werden, ob sich das Skirpt aktualisieren und bei geänderten Eingaben einen anderen Textbaustein anziehen darf.

```xml
<CustomDataNode id="BeispielSnippetSkript" update="true">
    <Condition when="RedCircle = 'true'">
        <Snippet id="05da9095-de60-4b78-bcd8-692639e8d377" />
    </Condition>
    <Condition notwhen="RedCircle = 'true' | BlueCircle = 'false'">
        <Snippet id="5bc2d759-431f-41e0-a18c-d577b240e612" />
    </Condition>
</CustomDataNode>
```

{:.table .table-striped}
Typ | Beschreibung
------- | -------
__Script__ | Via "Script" können dynamische Binding-Elemente (Scripts) in Vorlagen verwendet werden. Das Element Script kann beliebig viele solcher Elemente (CustomDataNodes) zur Verfügung stellen
engine | Engine die für die Scriptinterpretation resp. -umsetzung zur Anwenung kommt (es steht aktuell nur "XSL" zur Verfügung)
version | Scriptengine-Version die zur Anwendung kommt (Aktuell = 2, Standard = 1). Die Angabe dieser Version können auf Ebene 'CustomDataNode' übersteuert werden. Die Angabe der Version ist in Bezug auf die Abwärtskompatibilität wichtig
__CustomDataNode__ | Via "CustomDataNode" kann ein neues Binding-Element generiert werden in welchem der eigentliche Scriptinhalt definiert wird
id | ID des neuen Binding-Elements welches erzeugt werden soll (muss eindeutig sein). Für eine bessere Übersichtlichkeit im Vorlagen-Editor, können durch Punkte in der ID, Ordner erzeugt werden
version | Scriptengine-Version die zur Anwendung kommt (Aktuell = 2, Standard = 1). Die Angabe der Version auf Ebene 'CustomDataNode' übersteuert eine allfällige Versionsdekleration auf Ebene 'Script'
bookmarkname | Textmarke (Bookmark) in welchen die entsprechenden Bausteinen (Snippets) eingefügt resp. plaziert werden sollen. Wird nur berücksichtigt im Zusammenhang mit Bausteinen (siehe Snippet)
update | Beim Einfügen von Bausteinen via Scripts (Snippets), kann über update definiert werden, ob die jeweiligen Bausteine nur initial aktuell eingefügt werden, oder im offenen Dokument aktualisiert werden sollen (Standard = false). Wird nur berücksichtigt im Zusammenhang mit Bausteinen (siehe Snippet)
__Line__ | Via "Line" kann ein Zeilenumbruch generiert werden. Diese wird nur ausgegeben sofern auch ein Inhalt vorhanden ist (Ausnahme siehe Attribut 'fixoutput')
textbefore | Text welcher immer wenn die Zeile angezeigt wird, vorgängig erscheint (Achtung: Dokumentsprachunabhängig - alternativ "Text"-Funktion verwenden)
textafter | Text welcher immer wenn die Zeile angezeigt wird, nachgestellt erscheinet (Achtung: Dokumentsprachunabhängig - alternativ "Text"-Funktion verwenden)
fixoutput | Sofern "fixoutput" auf "true" gesetzt wird, wird die Linie auch ausgegeben wenn kein Inhalt vorhanden ist
__Element__ | Via "Element" können Texte aus dem OO-Binding angezogen werden. Diese werde nur ausgegeben sofern auch ein Inhalt vorhanden ist.
id | ID des Binding-Elements welches verwendet werden soll
separator | Trennzeichen zum nächsten Element oder Text der nur angezeigt wird, sofern achfolgend noch weitere Element einen Inhalt liefern
textbefore | Text welcher immer wenn das Element angezeigt wird, vorgängig erscheint (Achtung: Dokumentsprachunabhängig - alternativ "Text"-Funktion verwenden)
textafter | Text welcher immer wenn das Element angezeigt wird, nachgestellt erscheinet (Achtung: Dokumentsprachunabhängig - alternativ "Text"-Funktion verwenden)
linePrefix | Prefix Zeichen für jede Zeile einer Liste resp. eines mehrzeiligen Text-Elements
showEmptyStartLines | Übernimmt alle vorhandenen vorangestellten Leerzeilen (erlaubte Werte: "true", "false" [Default])
showEmptyEndLines | Übernimmt alle vorhandenen nachgestellten Leerzeilen (erlaubte Werte: "true", "false" [Default])
checkBoxActivatedSymbol | Definition des Zeichens, welches bei einer angewählten Checkbox ausgegeben werden soll
checkBoxDeactivatedSymbol | Definition des Zeichens, welches bei einer nicht angewählten Checkbox ausgegeben werden soll
when | Siehe Condition-Attribute
notwhen | Siehe Condition-Attribute
Funktionen |
fSubstring | Sofern nur ein Teil des Textes ausgegeben werden soll. Schema -> fSubstring([Startzeichen],[Anzahl Zeichen])
fSubstringBefore | Sofern nur der Anfang (vor einem bestimmten Zeichen) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird der ganze Text ausgegeben. Schema -> fSubstringBefore([Zeichenkette])
fSubstringBeforeOrEmpty | Sofern nur der Anfang (vor einem bestimmten Zeichen) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird kein Text ausgegeben. Schema -> fSubstringBeforeOrEmpty([Zeichenkette])
fSubstringAfter | Sofern nur das Ende (nach einem bestimmten Zeichen) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird der ganze Text ausgegeben. Schema -> fSubstringAfter([Zeichenkette])
fSubstringAfterOrEmpty | Sofern nur das Ende (nach einem bestimmten Zeichen) des Textes ausgegeben werden soll. Ist das Trennzeichen nicht vorhanden wird kein Text ausgegeben. Schema -> fSubstringAfterOrEmpty([Zeichenkette])
fCase | Sofern der Textes gross ("upper") oder klein ("lower") geschrieben werden soll. Schema -> fCase([upper/lower])
fReplace | Sofern ein Teil des Textes ersetzt werden soll. Schema -> fReplace([bestehende Zeichenkette],[neue Zeichenkette])
fTrim |  Sofern nur eine maximale Anzahl an Zeichen ausgegeben werden soll. Schema -> fTrim([maximale Anzahl Zeichen],[Modus],[Platzhalter]). [Modus] -> Ort an welchem bei Überlänge der Text abgeschnitten werden soll - erlaubte Werte "left","right" und "middle". [Platzhalter] -> Platzhaltertext der eingefügt wird, sofern eine Überlänge erreicht ist (bspw. "...")
fTrimURL | Sofern nur ein Teil einer URL oder eines Filepfads ausgegeben werden soll (siehe auch fTrim). Schema -> fTrim([Art],[Modus],[Anzahl Ordner]) [Art] -> File oder Folder, wobei File den Dateinamenselektiert und Folder den Pfad ohne Dateinamen. Aus diesem Grund stehen die nachfolgenden Optionen "Modus" und "Anzahl Ordern" nur bei "Folder" zur Verfügung. [Modus] -> Ort von welchem aus die Anzahl gewünschter Ordner angezeigt werden sollen - erlaubte Werte "left" und "right" [Anzahl Ordner] -> Anzahl der Ordner die Angezeigt werden soll