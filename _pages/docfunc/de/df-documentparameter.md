---
layout: page
title: Dokumentenparameter
permalink: "docfunc/de/df/documentparameter"
language: de
---

In der Dokumentfunktion ‘Dokument Parameter’ kann die Eingabemaske konfiguriert werden, die beim Anwählen einer Vorlage erscheint. Die Konfiguration kann grob in drei Teile unterteilt werden: oben bei den ‘DataNodes’ werden die Nodes definiert, auf die in der ‘View’ im unteren Teil zugegriffen wird. In der View wird das Aussehen des Dokumentparameters festgelegt. Im DataSources-Part können Datenbank Abfragen definiert werden, und die Werte aus der Abfrage auf die unter DataNodes definierten CustomElements geschrieben werden.

Grundgerüst mit Verwendung von Views:
```xml
<Configuration>	<!-- Dies ist der Root Node der Konfiguration -->
	<!-- Zwingende Komponente, ohne DataNodes kann keine View aufgebaut werden	-->
	<CustomContentSection>
		<DataNodes>
			<!-- CustomDataNodes werden hier Definiert -->
		</DataNodes>
	</CustomContentSection>
	<!-- Zwingende Komponente, ohne View gibt es keinen Dialog -->
	<Views>
		<View>
			<!-- Hier wird das Aussehen des Dialoges Definiert -->
		</view>
	</Views>
	<!-- Optionale Komponente -->
	<DataSources>
		<SqlDataSource>
		
		</SqlDataSource>
	</DataSources>
</Configuration>
```

Grundgerüst ohne Verwendung von Views:
```xml
<Configuration>	<!-- Dies ist der Root Node der Konfiguration -->
	<!-- Zwingende Komponente, ohne DataNodes kann keine View aufgebaut werden	-->
	<CustomContentSection>
		<DataNodes>
			<!-- CustomDataNodes werden hier Definiert -->
		</DataNodes>
	</CustomContentSection>	
	<!-- Optionale Komponente -->
	<DataSources>
		<SqlDataSource>
		
		</SqlDataSource>
	</DataSources>
</Configuration>
```

Am Ende dieser Seite befinden sich einige Beispiele, um die Verwendung der DataNodes mit und ohne Views zu veranschaulichen.

__Attribute von CustomContentSection__  

Beispiel:
```xml
<CustomContentSection xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Dokument-Parameter" WindowWidth="750" WindowHeight="750">
```

{:.table .table-striped}
|  __Name__  |  __Beschreibung__  |
|  ----  | ----  |
|   Name (Fenstername)        |    Über das Attribut "Name" kann der Name des Dokument-Parameter-Dialog-Fensters definiert werden.  |  
| WindowWidth (Fensterbreite) |  Über das Attribut "WindowWidth" kann die Fensterbreite in Pixel definiert werden. 1200 Pixel sollten nicht überschritten werden, da unter dieser Auflösung die einwandfreie Darstellung von OneOffixx möglich sein sollte. |
| WindowHeight (Fensterhöhe)  |  Über das Attribut "WindowHeight" kann die Fensterhöhe in Pixel definiert werden. 1200 Pixel sollten nicht überschritten werden, da unter dieser Auflösung die einwandfreie Darstellung von OneOffixx möglich sein sollte. Der Wert für WindowHeigth muss zwingend gesetzt sein. (Gilt für Verwendung mit und Ohne Views) |

## Die DataNodes und deren Attribute

  In diesem Abschnitt geht es um die Konfiguration zwischen `<DataNodes>` und `</DataNodes>`.
  Jedes CustomDataNode definiert ein Dokument-Parameter-Feld, auf das im Editor, in Skripts
  oder über Extended Bindings zugegriffen werden kann.
  Für jedes Feld in den Views (siehe 4. Views) muss für die Weiterverwendung der Eingabe ein
  CustomDataNode angelegt werden.

__CustomDataNode-Basisattribute (gelten für Verwendung mit und ohne Views)__  

{:.table .table-striped}  
|  __Name__                     		 |  __Beschreibung__  |
|    ----								 |        ----        |
| Type (xsi:type)						 | __TextNode__<br>Wird in Word zu einem Nur-Text-Inhaltssteuerelement (Plain Text Content Control), für ein- oder mehrzeilige Text-Eingabe, Überprüfung via Regex möglich<br><br>__CheckBoxNode__<br>Wird in Word zu einem Kontrollkästchensteuerelement (Check Box Content Control), für ja/nein-Auswahl<br><br>__DateTimeNode__<br>Wird in Word zu einem Datumsauswahl-Inhaltssteuerelement (Date Picker Content Control), für Datumsfeld mit Kalenderauswahl<br><br>__ComboBoxNode__ <br> Wird in Word zu einem Kombinationsfeld-Inhaltssteuerelement (Combo Box Content Control), für die Auswahl zwischen vorgegebenen Werten (beliebige Eingaben in Word zulässig)<br><br>__LabelNode__ <br> Überschrift im Dokument-Parameter-Dialog wenn Views nicht verwendet werden, nicht für die Verwendung im Editor, in Skripts und in Extended Bindings geeignet <br><br> __*RadioButton*__ <br>Es gibt keinen RadioButton-Typ. Der Grund ist, dass es in Word keine RadioButton-Inhaltssteuerelemente gibt. Trotzdem benötigen RadioButtons ein CustomDataNode, damit die Auswahl in der View gespeichert werden kann für die Verwendung im Editor, in Skripts und in Extended Bindings. <br><br> __Mögliche CustomDataNode-Typen für das Speichern der Auswahl von RadioButtons:__ <br><br>__Als Textnode__ <br> In diesem Fall wird der Value des in der View ausgewählten RadioButtons im TextNode gespeichert. Dies ist für Dokument-Parameter geeignet, die nicht in Word eingefügt werden sondern nur für den Zugriff via Skript oder Extended Binding erstellt wurden. Falls ein RadioButton vorausgewählt sein soll muss der Value des entsprechenden RadioButtons als Standard-Text konfiguriert werden, also: <br> `<CustomDataNode xsi:type="TextNode" Id="DocParam.RadioButtonGender" LCID="2055">ValueDesEntsprechendenRadioButtons</CustomDataNode>`{:.language-xml} <br><br> __Als ComboBoxNode__ <br> In diesem Fall wird der ComboBoxNode-Eintrag ausgewählt, bei dem der Key genau dem Value des RadioButtons entspricht. Dies ist auch für Dokument-Parameter geeignet, welche in Word eingefügt werden, da die Anzeige im Dokument über den Value des ComboBoxNode-Eintrags gesteuert wird. Falls ein RadioButton vorausgewählt sein soll muss der Value des entsprechenden RadioButtons im SelectedValue-Attribut der ComboBoxNode konfiguriert werden, also: <br> `<CustomDataNode xsi:type="ComboBoxNode" Id="DocParam.RadioButtonGender" LCID="2055" SelectedValue="ValueDesEntsprechendenRadioButtons">...</CustomDataNode>`{:.language-xml} <br><br> Wie die RadioButtons dann in der View definiert werden, wird im entsprechenden Kapitel beschrieben.  |  
|  Label (Beschriftung)        			 |  Beschriftung des Elements im Quick Check-Panel, wenn es sich um einen Tracked-Dokument-Parameter handelt.  |
|  Required (benötigtes Feld)  			 |   Attribut nur für Elemente des Typs Textfelder zulässig. Definiert ob das Feld leer gelassen werden kann (Required="false" oder nicht gesetzt) oder ob das Feld ausgefüllt werden muss (Required="true"). Wird von der Validierung (Regex-Attribut) übersteuert, falls eine gesetzt wird.  |  
|  Regex (Validierung)         			 |  Attribut nur für Elemente des Typs Textfelder zulässig. Erlaubt es einen Regex (.NET Syntax) zu definieren, welcher im eingegeben Text min. einen Match finden muss. Achtung: Falls der ganze Text 'gematcht' werden soll oder nur genau ein 'Match' vorhanden sein muss, muss dies vom Regex-Ausdruck definiert werden.<br><br>__Beispiele__<br>Regex="[0-9]+" erzwingt, dass min. ein Zeichen des Eingabetexts eine Ziffer sein muss. "Hallo 205" ist so z. B. eine gültige Eingabe. <br><br> Regex="^[0-9]+$" erzwingt, dass alle Zeichen des Eingabetexts Ziffern sein müssen (und dass min. 1 Ziffer vorhanden sein muss). (^ matcht den Anfang des Eingabetextes und $ das Ende)  | 
|    ValidationMessage (Fehlermeldung)   |  Attribut nur für Elemente des Typs Textfelder zulässig. Falls Required="true" oder ein Validierungs-Regex gesetzt wurde, erlaubt ValidationMessage eine benutzerdefinierte Fehlermeldung anzuzeigen, falls die Validierung fehlschlägt. Falls ValidationMessage nicht gesetzt ist, wird im Fehlerfall eine Standardmeldung angezeigt.  |
| Tracked (Überwachung mit "Quick Check")|	 Die OneOffixx-Funktion Quick Check (Inhaltssteuerelemente prüfen) wird mit dem Attribut Tracked aktiviert. Ist der Wert auf true gesetzt, wird dem Benutzer im separaten Panel das Feld angezeigt. Sofern der Inhalt des Elementes leer ist, wird das Feld im Panel rot und nach Bearbeitung grün angezeigt.	 |
|   Id (Identifikation)					 |  Textuelle ID, welche eindeutig sein muss. Diese wird im Editormodus angezeigt und danach für die Verwendung im Editor, in Skripts oder in Extended Bindings benötigt. Die Id darf keine Leerzeichen enthalten. |
| SelectedValue (Ausgewählter Eintrag)   |  Attribut nur für Elemente des Typs Kombinationsfeld (ComboBoxNode) zulässig. Über diese Option wird bestimmt, welcher Eintrag in der Liste standardmässig selektiert werden soll. |
| IsChecked (Standard-Selektion)		 |   Attribut nur für Elemente des Typs Kontrollkästchen (CheckBoxNode) zulässig. Über diese Option wird bestimmt, ob die Checkbox standardmässig selektiert oder unselektiert sein soll.  |
|  Locked (Sperrung)  					 |  Hat keine Wirkung. War ursprünglich dafür vorgesehen, dass das Inhaltssteuerelements (Content Control) in Word nicht gelöscht werden kann.  |
|    ReadOnly (nur Leserecht) 			 |	 Hat keine Wirkung. War ursprünglich dafür vorgesehen, dass das der Inhalt des Inhaltssteuerelements (Content Control) in Word nicht bearbeitet werden kann.

__CustomDataNode-Zusatzattribute bei Nichtverwendung von Views__

{:.table .table-striped}  
|  __Name__                     		 	 					|  __Beschreibung__  |
|    ----								 	 					|        ----        |
| Row (Zeile) 			  					 					|  Zeile, in welcher das Element im Dokument-Parameter-Dialog angezeigt werden soll. |
| Column (Spalte)   	  				 	 					| Spalte, in welcher das Element im Dokument-Parameter-Dialog angezeigt werden soll (Startpunkt). Es sind mit der Label-Spalte 4 Spalten vorhanden. |
| ColumnSpan (Länge)      					 					|  Länge resp. Anzahl Spalten über welche sich das Element erstrecken soll.  |
|  Label (Beschriftung)   					 					| Beschriftung des Elements im Dokument-Parameter-Dialog, gilt auch für Überschriften des Typs LabelNode. Sofern mehrere Elemente in einer Zeile dargestellt werden, wird die Beschriftung des ersten Elements übernommen. Die Beschriftung erscheint immer in der Spalte ganz links. Wenn Tracked auf true gesetzt ist fungiert das Label zusätzlich als Beschriftung des Elements im Quick Check-Panel. |
|  Visible (Sichtbarkeit) 	 				 					| Wenn die Sichtbarkeit auf false gesetzt ist, wird der Dokument-Parameter im Dialog nicht angezeigt. |
|  Tooltip (Hinweis)      					 					| Hinweis, welcher angezeigt wird, wenn der Benutzer mit der Maus darüber fährt. Wird von ValidationMessage überschrieben, falls diese gesetzt ist (bei Textfeldern). |
|  IsInputEnabled (Beschriftung editierbar)  					| Attribut nur für Elemente des Typs Kontrollkästchen (CheckBoxNode) zulässig. Wenn diese Option auf true gesetzt ist, werden im Dokument-Parameter-Dialog Kontrollkästchen angezeigt, bei welchen der User die Beschriftung editieren resp. frei wählen kann.  |
|  MultiLine (Mehrzeiligkeit)				 					| Attribut nur für Elemente des Typs Textfelder (TextNode) zulässig. Erstellt mehrzeilige Textfelder wenn auf true gesetzt. |
| MultilineRows (Anzahl angezeigter Zeilen bei Mehrzeiligkeit)	| Attribut nur für Elemente des Typs Textfelder (TextNode inkl. Multiline="true") zulässig. Definiert die Anzahl angezeigter Zeilen in mehrzeiligen Textfelder (standardmässig auf 3). |
| IsSearchEnabled (Suche für Kombinationsfelder aktivieren)	 	| Attribut nur für Elemente des Typs Kombinationsfeld (ComboBoxNode) zulässig. Über diese Option wird bestimmt ob Mittels Tastatureingabe im Kombinationsfeld nach vorhandenen Einträgen gesucht werden kann. |
| IsEditable (bei Kombinationsfeld beliebige Eingabe zulassen)  | Attribut nur für Elemente des Typs Kombinationsfeld (ComboBoxNode) zulässig. Über diese Option wird bestimmt, ob der Benutzer eine beliebige Eingabe tätigen kann. Wenn dieses Attribut nicht auf true gesetzt ist kann der Benutzer nur zwischen den vorhandenen Einträgen auswählen. |


## Views  

__Grundaufbau__  

- Es kann n View Elemente geben.  
- Eine View kann n Row Elemente haben.  
- Ein View hat 4 Spalten (Columns).  

```xml
<Views IsDebug="false">
  <View Id="main" Label="Startseite">
    <Row />
    <Row />
    ...
    <Button Type="Submit" Label="OK" />
    <Button Type="Cancel" Label="Abbrechen" />
  </View>
</Views>
```

Spezial-IDs:
View mit "main" ==> Start-Ansicht
Button Type="Submit" ==> Dokument-Parameter-Dialog verlassen, weiter im Prozess
Button Type="Cancel" ==> Dokument-Parameter-Dialog verlassen, Abbruch des Prozesses