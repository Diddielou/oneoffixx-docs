---
layout: default
title: Architektur
permalink: "/de/architecture/"
---

## System�bersicht

Folgende System�bersicht zeigt schematisch welche Kommunikationspfade OneOffixx unterst�tzt. 

-- IMG --

F�r die Schnittstellenbeschreibung stehen zwei Schnittstellen im Fokus:

* Die Fachapplikaton kann OneOffixx mit unterschiedlichen Methoden aufrufen. Siehe dazu Kapitel "2.3.1"

* Die Fachapplikaton ruft den OneOffixx Document Creation Server auf. Die XML Konfiguration wird �ber die REST API �bergeben. 

## Document Engine

Die Document Engine ist das Herzst�ck der OneOffixx Applikation. Sie kommt sowohl im Server als auch im Client zum Einsatz und besteht aus drei Komponenten, dem Producer, der Documentfunction-Pipeline und dem Communication Service.

-- IMG --

Der Producer erstellt eine Vorlage aus einer Reihe von verschiedenen Vorlagen, die in einer Vererbungshierarchie gegliedert sind. Jede Vorlage bzw. Vorlagentyp bringt einen Teil der spezifischen Merkmale des Enddokumentes mit. Zum Beispiel liefert das �Style� Dokument alle Style Merkmale des Hauptdokumentes mit. Die verschiedenen Vorlagentypen k�nnen so beliebig kombiniert und jederzeit ausgetauscht oder aktualisiert werden. Dadurch k�nnen Redundanzen im Vorlagenbau vermieden werden. Die Dokumente werden immer zur Laufzeit neu generiert.

Die Dokumentenpipeline enth�lt ein vorlagenspezifisches Set von Funktionen, die als PlugIns realisiert sind und beim Starten von OneOffixx geladen werden. Welche Dokumentfunktionen in welcher Reihenfolge in einer Vorlage verwendet werden, wird in OneOffixx im Vorlagenbearbeitungsmodus vom Vorlagenbauer festgelegt. Jede Dokumentfunktion unterst�tzt eine Reihe von Kommandos, welche von OneOffixx zu einem beliebigen Zeitpunkt aufgerufen werden.

Dokumentfunktionen enthalten f�r sich geschlossene Prozeduren, die auf das Dokument, Schnittstellen etc. angewendet werden.

Der Service ist f�r die Verbindung zu den Zielsystemen wie Word oder ein CRM verantwortlich. Er speichert die Vorlage und startet das gew�nschte Programm. Im Fall von Office kommuniziert dieser mit dem Addin und reicht Dokumenteninhalte an das Addin weiter.

Die OneOffixx Schnittstelle erlaubt es in alle drei Komponenten direkt einzugreifen und Inputdaten zu liefern und damit die Anwendung steuern. �ber die Schnittstelle werden Daten und Kommandos an OneOffixx �bergeben, keine Formateigenschaften. 


