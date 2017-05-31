---
layout: page
title: Mail Signatur
permalink: "docfunc/de/df/mailsignature"
language: de
---

Über die Dokumentfunktion 'Mailsignatur' wird nicht der Inhalt der Signatur selber definiert, sondern wann sie zur Verwendung kommen soll und ob sie Zusätze wie z.B. einen Disclaimer oder eine Kampagne haben soll. Sie wird jeweils den Vorlagen mit dem Typ 'Mail Signature' angehängt. Die Reihenfolge in der Signatur lautet immer: Signatur, Kampagne, Disclaimer. Nachfolgend werden die Konfigurierbaren Teile erläutert:


{:.table .table-striped}
Tag | Beschreibung
---------|----------
**Domains**         |   Hier kann definiert werden, bei welchen Email Domains die Signatur ausgewählt werden soll. Ein Asterisk bedeutet, dass die Signatur bei allen Domains genommen wird. Die Domains müssen in folgendem Format eingegeben werden: `internaldomain.com`. Bei mehreren Domains müssen sie durch einen Strichpunkt (;) getrennt werden.
**Accounts**        |   Über den Account Tag kann eingestellt werden, bei welchen Account Typen die Signatur verwendet werden darf.
**IsDefault**       |   Mit dem IsDefault Tag kann konfiguriert werden, ob die Sigantur standardmässig bei einer neuen Mail kommen soll oder nicht.
**IsDefaultReply**  |   Der IsDefaultReply Tag bewirkt dasselbe wie der IsDefault Tag, allerdings bei Antworten.
**HasDisclaimer**   |   Durch den HasDisclaimer Tag kann gesteuert werden, ob es in der Signatur einen Disclaimer geben soll. Dieser wird in einer eigenen Vorlage mit dem Typ 'Mail Disclaimer' definiert.
**HasCampaign**     |   Gleich wie beim Disclaimer kann hier definiert werden, ob eine allfällige Kampagne angezogen werden soll. Diese wird wie der Disclaimer in einer eigenen Vorlage definiert.