---
layout: default
title: Connect
permalink: "/de/connect/"
---

�OneOffixx Connect� ist die Low Level XML Spezifikation der OneOffixx XML Schnittstellen. Sie greift direkt auf die OneOffixx API bzw. auf die Dokumentgenerierungspipeline zu. Aus Gr�nden der Versionssicherheit sollten die Fachapplikationen nicht direkt auf diesem Layer aufsetzen. Die Entwicklung von OneOffixx beh�lt sich vor, diese Spezifikation jederzeit zu �ndern bzw. zu erweitern. F�r Fachapplikationen existiert ein dar�ber liegender Layer, der es erm�glicht, die Versionskompatibilit�t zu gew�hrleisten. OneOffixx �bernimmt automatisch die Transformation von einem Layer in den n�chsten.

## Aufruf

OneOffixx Connect kann sowohl von der Client-Applikation als auch �ber auf dem Server verarbeitet werden. Das Format ist hierbei gleich, wobei einige Operation nur auf auf dem Client selbst ausf�hrbar sind, z.B. das Starten eines Wordprozesses. 

### Connect Verarbeitung auf dem Client

Die Fachapplikation ruft OneOffixx �ber einer der folgenden Methoden auf:

* Via Prozess �c:\\program�\OneOffixx.exe /connect XYZDatei.xml
* Via Protokollhandler oneoffixx:connector=�XYZDatei.xml�
* Via Shell. File Association *.ooconnect, *oocx, *oock

ACHTUNG: OneOffixx l�scht nach der Verarbeitung automatisch das Connect File. Wird das zus�tzliche Argument /keepConnector �bergeben kann dieses Verhalten unterdr�ckt werden. Wird via Shell aufgerufen, dann muss in diesem Fall die Endung oock verwendet werden.

### Connect Verarbeitung auf dem Server

Im Falle der serverseitigen Verarbeitung wird ein extra API Benutzer ben�tigt, welcher in der Server Konfiguration hinterlegt werden muss.
Zur Kommunikation zwischen Aufrufer und der serverseitigen REST-Schnittstelle wird das HTTP Protokoll verwenden. Die Authentifizierung des Clients erfolgt durch HTTP Basic Authentifizierung, daher wird empfohlen die Kommunikation zwischen Client und Server durch SSL abzusichern.
Um OneOffixx Connect auf dem Server zu verarbeiten muss vorher ein �client� auf der OneOffixx Server Seite konfiguriert werden. �ber diese �client�-Konfiguration wird auch der Name und das Passwort f�r die Authentifizierung festgelegt.
Das Connect-XML muss als HTTP POST samt dem �Authorization�-Header gesendet werden. Bei einer erfolgreichen Verarbeitung wird das erzeugte Dokument zur�ck gegeben.
Beispiel: 

HTTP POST �https://{server}/api/V1/connect�

Headers: 
Authorization Basic dXNlcm5hbWU6cGFzc3dvcmQ=

Im Body das OneOffixxConnect XML hinterlegen.

* Der Basic Authentication-Header ist im Beispiel �username:password� als Base64 encodiert.

## Ergebnis

Das Ergebnis eines OneOffixx Connect Aufrufs wird auch als XML-File an der gleichen Stelle wie das Input-XML abgelegt. Der Filename hat die folgende Form:

result_<Name Inputfile>_<Zeitstempel>.xml

Standardm�ssig wird das File nur bei einem Fehler erstellt. 

Mit dem Argument /CreateConnectorResult, wird das File immer erzeugt, mit dem Argument /CreateConnectorResultOnError false wird die Funktionalit�t ganz deaktiviert.

Alternativ k�nnen die Parameter im Dokument ge�ndert werden (siehe Kapitel 3.4)

Das Fehlerfile hat das folgende Format:

    <?xml version="1.0" encoding="utf-16"?>
    <OneOffixxConnectResult xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Result><!-- Success oder Error --></Result>
      <Message><!-- Exception bei einem Fehler --></Message>
      <Details>
        <InputFile><!-- Pfad zum Input-File --></InputFile>
        <Input><!-- Input-File --></Input>
        <Connect><!-- Connect-File --></Connect>
        <InterfaceType><!-- Interface-Typ f�r Tranformation (z. Bsp. Klib) --></InterfaceType>
        <InterfaceVersion><!-- Interface-Version --></InterfaceVersion>
        <InterfaceConfiguration><!-- Interface-Konfiguration (Transformation) --></InterfaceConfiguration>
      </Details>
    </OneOffixxConnectResult>
