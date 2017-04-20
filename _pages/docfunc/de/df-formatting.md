---
layout: page
title: Formatierung
permalink: "docfunc/de/df/formatting"
language: de
---

Die Formatierung ist normalerweise nur der Stylevorlage angehängt. Hier konfiguriert man die Knöpfe unter ‘Formatierung’ im OneOffixx Ribbon. Jedem Knopf kann ein Style zugeordnet werden. Zusätzlich zu den vordefinierten Knöpfen kann man eine beliebige Anzahl weiterer Styles hinterlegen, die über ein Dropdown ausgewählt werden können.

Die Knöpfe sind im Ribbon aktiviert, sobald die Dokumentfunktion der Vorlage angehängt wird.
![x]({{ site.baseurl }}/assets/content-images/docfunc/de/ribbonformatting.png)

Der Aufbau der Konfiguration ist wie folgt:
```xml

<DocumentFunction>

    <!-- Parametrierung der Überschriften -->
    <Group name="{Gruppenname}" maxListLevels="{Maximale Einrückung}">
        <Label lcid="{LCID}">Übersetzter Gruppenname</Label>
        <Definition type="{Type}" level="{Level Einrückung}" style="{Wordstyle}">
            <Label lcid="{LCID}">Übersetzter Stylename</Label>
        </Definition>
    </Group>

<DocumentFunction>
```

{Gruppename} | Beschreibung
------- | -------
Headings | Überschriften
Indents | Einrückungen / Tabulatoren
NumberingStyles  |  Aufzählungen
NumberingBehaviors | Verhalten bei Aufzählungen
Styles | Setzen von Styleinformationen. Wenn kein Style angegeben ist, werden die Inlinestyle verwendet.
CustomStyles | Kundenspezifische Auflistung von Style


__level__ entspricht der Tabulatorenanzahl vom linken Rand. __maxListLevels__ definiert ab wieviele Tabulatoren wieder zum Anfang gesprungen werden soll.
__style__ entspricht dem globalen Word Stylenamen.

Alle Elemente können in eine andere Sprache übersetzt werden. Dafür wird das XML Element __Label__ verwendet. Die LCID gibt die localisierung ID an im Falle. Das bedeutet, wenn die UI in der deutschen Sprache angezeigt wird, muss die LCID der deutschen Sprache entsprechen (z.Bsp 1033). 

```xml
<DocumentFunction>

    <!-- Experimental (immer false)-->
    <EnableHotkeys>false</EnableHotkeys>

    <!-- Parametrierung der Überschriften -->
    <Group name="Headings">
        <Definition type="Heading" level="1" style="Überschrift 1"/>
        <Definition type="Heading" level="2" style="Überschrift 2"/>
        <Definition type="Heading" level="3" style="Überschrift 3"/>
        <Definition type="Heading" level="4" style="Überschrift 4"/>
    </Group>

    <!-- Parametrierung der Tabulatoren -->
    <Group name="Indents" maxListLevels="4">
    </Group>

    <!-- Parametrierung der Listen, Aufzählungen und Nummerierungen -->
    <Group name="NumberingStyles">
        <Definition type="Numeric" tabPosition="1" style="List_Numeric" />
        <Definition type="Alphabetic" tabPosition="1" style="List_Alphabetic" />
        <Definition type="Bullet" tabPosition="1" style="List_Bullet" />
        <Definition type="Line" tabPosition="1" style="List_Line" />
    </Group>

    <!-- Parametrierung der Nummerierungs-Optionen -->
    <Group name="NumberingBehaviors">
        <Definition type="Increment" style="List_Numeric"/>
        <Definition type="Decrement"/>
        <!--<Definition type="RestartMain"/>
        <Definition type="RestartSub"/>-->
        <Definition type="ResetChapter" style="Überschrift 1"/>
        <Definition type="ResetList" style="List_Numeric"/>
    </Group>

    <!-- Parametrierung der weiteren Formatierungs-Optionen -->
    <Group name="Styles">
        <Definition type="Standard" style="Standard"/>
        <Definition type="Bold" style="Fett"/>
        <Definition type="Italic" style=""/>
        <Definition type="Underline" style=""/>
    </Group>

    <!-- Parametrierung der weiteren kundenspezifischen Formatierungs-Optionen -->
    <Category id="CustomStyles">
                <Label lcid="1042">div. Formatierungen</Label>
                <Definition type="Intensiv" style="Intensiv">
                    <Label lcid="1042">Hervorgehoben</Label>
                </Definition>
                <Definition type="Bold" style="Fett">
                    <Label lcid="1042">Fett</Label>
                </Definition>
          </Category> 
    </Group>
    

</DocumentFunction>
```